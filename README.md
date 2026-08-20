# Geniqua Logistics — 網站部署包

版本：2026-08-20 ‧ 單一檔案靜態網站，無建置流程、無相依套件。

## 內容

| 檔案 | 用途 |
|---|---|
| `index.html` | 全站。十二個分頁、雙語、五項試算工具、所有插圖皆內嵌於此檔 |
| `.nojekyll` | 停用 GitHub Pages 的 Jekyll 處理，避免底線開頭之路徑被略過 |

## 部署至 GitHub Pages

### 方式一：網頁上傳

1. 進入 `https://github.com/sandyliu3056/Geniqua`
2. 點選 **Add file → Upload files**
3. 將 `index.html` 與 `.nojekyll` 一併拖入，Commit changes
4. 進入 **Settings → Pages**，Source 選 `Deploy from a branch`，Branch 選 `main`、目錄 `/ (root)`，儲存
5. 約一至二分鐘後可於 `https://sandyliu3056.github.io/Geniqua/` 開啟

> 儲存庫中若仍有 `index (82).html`，請一併刪除。該檔為早期版本，檔名含空格與括號，會佔用索引。

### 方式二：命令列

```bash
git clone https://github.com/sandyliu3056/Geniqua.git
cd Geniqua
cp /path/to/index.html .
touch .nojekyll
git add index.html .nojekyll
git commit -m "Deploy Geniqua Logistics site"
git push origin main
```

## 分頁與網址

採 hash 路由，全部分頁由 `index.html` 處理，GitHub Pages 無須任何重寫規則，亦不需要 `404.html`。

```
#/home          首頁              #/brokerage     報關服務
#/mission       經營理念          #/calculators   快遞試算
#/services      服務項目          #/oceanvolume   海運材積試算
#/ocean         海運承攬          #/promotions    優惠方案
#/inland        內陸運輸          #/contact       聯絡我們
#/warehouse     倉儲與配送
#/ecommerce     電商訂單代發貨
```

## 維護重點

開啟 `index.html`，於 `<script>` 區段內：

**`var RULES`（檔案上方）** — 三家承運人的材積除數、附加費門檻、最低計費重量，以及貨櫃規格、棧板尺寸、各倉營業時間。計算函式不含任何寫死數值，調整費率規則只需改這一段。

**`var DICT`** — 全站介面文字，`en` 與 `zh` 兩份。

**`var PAGES`** — 各分頁的標題與內文區塊。優惠方案的三張卡片位於 `PAGES.promotions.blocks`。

**`var FAQS` / `var FACILITIES`** — 常見問題與設施規格清單。

## 注意事項

本檔未使用 Service Worker，因此無 `sw.js` 的 BUILD 字串需要遞增；更新後以強制重新整理（Ctrl/Cmd + Shift + R）即可看到新版。

行動裝置若已加入主畫面，更新圖示需先刪除捷徑、清除 Safari 網站資料後重新加入。

字型由 Google Fonts 載入（Archivo、Noto Sans TC）；離線或無法連線時自動退回系統字型，版面不受影響。

插圖中的車輛與航機採通用塗裝，未複製任何承運人之商標或商業外觀。UPS、FedEx、USPS 之品牌色僅出現在實際指名該承運人之處（詢價表單的承運人偏好、試算工具的承運人切換、貨況查詢結果）。

試算結果為規劃用途之估算值，頁面已載明實際計費以合約條款及承運人核算後之帳單為準。

# 逐年報酬試算

輸入股票代號與投入日期，自動抓歷史股價，算出從投入那天起每一個年度的報酬率、累積報酬與年化報酬（CAGR）。

- 美股個股與 ETF（AAPL、NVDA、VOO、QQQ…）透過 [Twelve Data](https://twelvedata.com) API 自動抓價
- 「總報酬」會把每次除息的股利再投入；也可切換成只看股價漲跌
- 台股在 Twelve Data 需付費方案；免費方案可用「手動匯入」上傳 Yahoo Finance 或證交所的 CSV
- 紅漲綠跌、支援深色模式與手機版

線上使用：https://ts701105-cell.github.io/stock-annual-returns/

## 使用前準備

1. 到 <https://twelvedata.com/register> 免費註冊，在 **API Keys** 頁面複製金鑰。
2. 打開網頁，展開「Twelve Data API 金鑰」，貼上後按「儲存」。

金鑰只存在你自己瀏覽器的 localStorage，**不會寫進程式碼，也不會上傳到 GitHub**。每位使用者都要用自己的金鑰。

免費方案限制：每分鐘 8 次、每天 800 次查詢；每次計算用 2 次（股價＋股利）。

## 放到 GitHub Pages

1. 在 GitHub 建立一個新的 repository（例如 stock-annual-returns），設為 Public。
2. 把 index.html 和 README.md 上傳到 repository 根目錄。
3. 到 repository 的 **Settings → Pages**，Source 選 **Deploy from a branch**，Branch 選 main、資料夾選 / (root)，按 Save。
4. 約一分鐘後，網址會是 https://<你的帳號>.github.io/stock-annual-returns/。

整個網站只有一個 index.html，不需要任何建置步驟。

## 計算方式

- 以投入日當天（遇假日取下一個交易日）的收盤價買進。
- 第一年：投入日 → 該年最後交易日；之後每年：前一年最後收盤價 → 當年最後收盤價；最新一年算到資料最後一天。
- 總報酬：每次除息時，以除息前一日收盤價把股利再投入。股價已做分割調整。
- 投入超過 19 年時改用週收盤價（API 單次最多 5000 筆）。

本工具僅供試算參考，不構成投資建議。

## v2 版（免金鑰）

v2 版位於 https://ts701105-cell.github.io/stock-annual-returns/v2/ ，不需要 API 金鑰。支援台股與 ETF（數字代號，已處理除息與分割）以及美股。資料來自 FinMind，同一個網路每小時有查詢次數上限。

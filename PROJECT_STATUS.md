# PROJECT STATUS

> Claude Code 與 Codex 共用交接紀錄。開始工作前先讀本檔；完成修改後同步更新本檔與 `CHANGELOG.md`。

## 目前狀態

- 版本：v0.4.0
- 最後更新：2026-06-09
- 最後執行者：Codex
- 專案形式：單一 `index.html`，純原生 HTML/CSS/JavaScript
- AI 模型：`gemini-2.5-flash`
- 本地預覽：`python3 -m http.server 5500`
- Git 狀態：目前資料夾不是 Git repository

## 本次完成

- API Key 改用 `x-goog-api-key` header 傳送。
- API Key 改為勾選後才記住，並可一鍵清除。
- 修正 API Key 安全說明。
- 新增案例建議與完整架構的 JSON Schema。
- 新增七段架構、三個 LCD、三級引薦與必要欄位的前端驗證。
- 新增 60／90 秒 API 逾時處理。
- 修正全域 `event`、狀態訊息 HTML 注入與剪貼簿失敗問題。
- 補強流程圖、API 教學開關、Tab 與表單 label 的基本無障礙操作。
- 同步 `prompts/bni-structure.md` 與 `index.html` 的 Prompt A/B 格式。

## 已驗證

- `index.html` 內嵌 JavaScript 語法檢查通過。
- 本地頁面可正常載入。
- 390px 手機寬度無水平溢出。
- 無效 API Key 能顯示錯誤，請求完成後按鈕會恢復。
- API Key 清除、選擇記住與頁面重載後還原已通過；測試 Key 已清除。
- lightbox 的 Enter／Escape 操作與 API 教學開關狀態同步已通過。
- 流程圖目前可由外部圖床載入。
- 瀏覽器 console 無 JavaScript 錯誤。

## 尚未驗證

- 尚未使用有效 Gemini API Key 測試 Prompt A 的真實成功回傳。
- 尚未使用有效 Gemini API Key 測試完整七段架構及 PPT 提示詞的真實成功回傳。
- `responseJsonSchema` 已依 Gemini REST API 規格加入，但仍需用有效 Key 做端到端確認。

## 待處理

- [ ] 將流程圖改為專案內本地圖片，移除 ibb.co 外部依賴。
- [ ] 評估是否支援 10 分鐘以外的簡報長度。
- [ ] 評估匯出 PDF／Word。
- [ ] 決定章員共用裝置的 API Key 管理方式；目前建議不要勾選「記住」。
- [ ] 建立 Git repository 或確認既有版本控制位置。

## Prompt 同步規則

- `prompts/bni-structure.md` 是人類可讀的 prompt 規格來源。
- 為維持單檔離線工具，執行用 prompt 內嵌於 `index.html`。
- 修改 Prompt A 時同步更新 `suggestLCD()`、`suggestionSchema`、`validateSuggestions()`。
- 修改 Prompt B 時同步更新 `buildPrompt()`、`outlineSchema`、`validateOutline()`、渲染與 PPT prompt。

## 每次交接必做

1. 更新本檔的版本、日期、最後執行者與完成事項。
2. 把使用者可感知的變更寫入 `CHANGELOG.md`。
3. 記錄實際執行過的驗證，以及因缺少 API Key 或環境限制而未驗證的項目。
4. 不要把真實 API Key、客戶資料或測試個資寫入任何專案檔案。

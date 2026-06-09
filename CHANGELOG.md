# CHANGELOG

## [0.5.0] — 2026-06-09

### 新增
- 輸出改為三步驟流程：步驟一（確認架構）→ 步驟二（投影片預覽）→ 步驟三（PPT 提示詞）
- 步驟一：所有段落欄位（話術、要點）皆可直接編輯；LCD A-E 各有勾選框，只有勾選的項目才帶入步驟二
- LCD E（成功案例故事）勾選後，步驟二產生獨立故事投影片（情境/挑戰/解法/結果四格）
- 步驟二：每張投影片為 contenteditable 卡片，可直接點擊修改文字
- 步驟三：PPT 提示詞根據步驟二最終編輯內容動態產出，非固定架構
- 頂部步驟指示器（1→2→3，已完成為藍色，當前為紅色）

### 修改
- 移除舊有的「架構預覽 / PPT 提示詞」雙 Tab 設計
- `editState` 為 AI 產出 JSON 的可變狀態物件（含 LCD checks 布林值）
- `slideState` 為由 editState + 勾選狀態推導出的投影片陣列
- PPT 提示詞由 `buildPptPromptFromSlides()` 從 slideState 建構，反映使用者最終編輯

### 驗證
- JavaScript 語法檢查通過

---

## [0.4.0] — 2026-06-09

### 修正
- Gemini API Key 改由 `x-goog-api-key` header 傳送，不再放在 URL query string
- API Key 改為使用者勾選後才存入 localStorage，並新增清除已儲存 Key 功能
- 修正安全說明，明確告知 Key 會傳送至 Google Gemini API
- 新增 Gemini `responseJsonSchema`，限制案例建議與七段架構的 JSON 格式
- 新增前端結構驗證，攔截段落數量、LCD 數量、三級引薦或必要欄位不完整的回傳
- 新增 API 請求逾時：案例建議 60 秒、完整架構 90 秒
- 修正 API Key 顯示按鈕依賴非標準全域 `event` 的相容性問題
- 狀態訊息改用 `textContent`/DOM 節點產生，避免 API 錯誤文字被當成 HTML
- 複製 PPT 提示詞加入失敗提示與舊瀏覽器 fallback
- 流程圖 lightbox 支援 Enter、空白鍵開啟與 Escape 關閉
- Tab、API 教學開關及表單 label 補上基本無障礙屬性

### 修改
- AI 建議案例的 thinkingBudget 從 8192 降為 1024，完整架構維持 8192
- Prompt A 統一使用物件陣列格式：`id`、`title`、`service`、`clientType`
- Prompt A 補入姓名與補充背景；Prompt B 文件補入三級引薦提示變數
- 明確定義 `prompts/bni-structure.md` 與 `index.html` 內嵌 prompt 的同步規則

### 文件
- 新增 `PROJECT_STATUS.md`，作為 Claude Code 與 Codex 的共用進度／交接紀錄
- 更新 `AGENTS.md` 與 `CLAUDE.md`，要求每次修改後同步維護交接與版本紀錄

### 驗證
- JavaScript 語法檢查通過
- 本地桌面與 390px 手機版基本操作回歸通過
- 無效 API Key 錯誤處理、按鈕恢復、Key 儲存控制、lightbox 鍵盤操作與 API 教學開關通過
- 瀏覽器 console 無 JavaScript 錯誤
- 尚未使用有效 Gemini API Key 驗證真實成功回傳

---

## [0.3.0] — 2026-06-09

### 新增
- UI 全面換色：BNI 紅（`#E31837`）+ 富聯淺藍（`#4AAFE8`）+ 白底，取代原暗色主題
- 頂部 topbar：顯示「BNI 富聯分會 / FEATURE PRESENTATION TOOL」
- Hero 區塊：紅色漸層標題 + 三個識別 badge
- 流程圖區：載入富聯簡報大綱流程圖（`https://i.ibb.co/dsF1z6wh/IMG-1996.jpg`），高度上限 420px，點擊可 lightbox 放大
- 輸入表單分區：藍色 accent（API 設定、LCD）/ 紅色 accent（簡報資訊、三級引薦）視覺區分
- 三級引薦輸入改為橫排三欄，各有顏色標籤（紫/綠/藍）

### 修改
- Lightbox 功能：點擊流程圖可全螢幕放大，再次點擊關閉
- 流程圖下方加「點擊圖片可放大查看」提示文字

---

## [0.2.0] — 2026-06-09

### 新增
- API Key 教學區塊（可展開/收合）
  - 五步驟圖文說明
  - 直連「前往 Google AI Studio」按鈕（`https://aistudio.google.com/apikey`）
  - 底部安全說明：Key 僅存 localStorage，不傳後端
- Gemini API Key 自動儲存至 localStorage，下次開啟自動帶入

### 修改
- 展開箭頭動畫（旋轉 90 度）
- 教學區塊配色改為藍色系（與 API 設定卡一致）

---

## [0.1.0] — 2026-06-09

### 建立
- 單一 `index.html` 工具，純原生 HTML/CSS/JS，無外部框架
- 串接 Gemini 2.5 Flash API（思考模式 thinkingBudget: 8192）
- 輸入欄位：姓名、行業、本週主題（必填）、目標客戶、補充背景
- LCD 案例輸入：三個文字欄 + 「AI 建議案例」按鈕（Prompt A）
- 三級引薦提示輸入：夢幻 / 理想 / 一般（選填）
- 主產出按鈕：「產出架構 + PPT 提示詞」（Prompt B）
- 輸出 Tab 1：七段式架構預覽（含 LCD A-E 展開、三級引薦分層）
- 輸出 Tab 2：PPT 製作提示詞（可一鍵複製，貼入 ChatGPT / Gemini）

### 結構文件
- `CLAUDE.md`：專案說明、七段架構規格、互動流程、開發原則
- `prompts/bni-structure.md`：Prompt A（LCD 建議）+ Prompt B（完整架構）模板
- `.claude/skills/bni-presenter.md`：Claude Code slash command，三步驟互動產出架構
- `.claude/launch.json`：本地預覽伺服器（python3 http.server 5500）

---

## 目前已知問題 / 待處理

- [ ] 流程圖來源為外部圖床（ibb.co），建議未來改為本地圖片
- [ ] 輸出的七段架構目前無法直接匯出 PDF 或 Word
- [ ] 尚未支援 10 分鐘以外的時間長度
- [ ] 尚未測試章員共用情境下的 API Key 管理方案

## 技術規格

| 項目 | 規格 |
|------|------|
| 框架 | 純原生 HTML/CSS/JS |
| AI | Gemini 2.5 Flash（`gemini-2.5-flash`） |
| 思考模式 | 案例建議 `1024`；完整架構 `8192` |
| 輸出格式 | JSON Schema + 前端結構驗證 |
| API Key 傳送 | `x-goog-api-key` request header |
| API Key 儲存 | 使用者可選；`localStorage`（key: `bni_gemini_key`） |
| 本地伺服器 | `python3 -m http.server 5500` |
| 流程圖 | `https://i.ibb.co/dsF1z6wh/IMG-1996.jpg` |

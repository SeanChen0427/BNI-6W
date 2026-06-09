# BNI 富聯分會 主題簡報架構產生器

> 開始工作前先讀取 `PROJECT_STATUS.md`；完成任何修改後，必須同步更新 `PROJECT_STATUS.md` 與 `CHANGELOG.md`，供 Claude Code 與 Codex 交接。

## 專案目的

協助 BNI 富聯分會成員（主題簡報者）快速產出符合富聯標準的七段式簡報架構，包含三個 LCD 成功案例展開、三級引薦規劃與話術建議。

## 工具形式

- 單一 `index.html`，本地直接開啟，無需後端
- 呼叫 Gemini API（使用者自填 API Key，可選擇是否存於 localStorage）
- 模型：`gemini-2.5-flash`，案例建議 thinkingBudget 1024，完整架構 thinkingBudget 8192

---

## BNI 富聯簡報標準結構（總時長 10 分鐘）

| # | 段落 | 時間 | 說明 |
|---|------|------|------|
| 1 | 標題與說明 | 30 秒 | 說明今日標題與分享重點 |
| 2 | 介紹自己 | 30 秒 | 專長、獨特處、專業經歷 |
| 3 | 介紹公司 | 30 秒 | 公司特色、與同業差異、代表性客戶 |
| 4 | 三個成功案例（LCD×3） | 6 分鐘（各 2 分） | 每個 LCD 展開 A-E 五面向 |
| 5 | 開啟對話 | 1 分鐘 | 具體對談方式與行動指示 |
| 6 | 三級引薦 | 1 分鐘 | 夢幻 / 理想 / 一般三層引薦對象 |
| 7 | 結語 | 30 秒 | 重申重點 |

### LCD 成功案例結構（A-E）

每個 LCD 案例包含以下五個面向：

- **A. 產品或服務**：本案例展示的服務或產品項目
- **B. 對客戶的效益或解決的問題**：客戶獲得的具體效益
- **C. 交易引薦對象**：此類型案例適合引薦給誰
- **D. 業務人脈圈**：相關的上下游業務夥伴或生態系
- **E. 成功案例**：實際故事，含稀好事與細節，說給成員聽

### 三級引薦結構

- **夢幻引薦**（Biggest Target）：最想要、最大的潛在客戶
- **理想引薦**（Higher Value）：高價值、符合核心業務的客戶
- **一般引薦**（Low Level Entry）：門檻低、容易轉介的入門客戶

---

## 工具互動流程（兩階段）

**第一階段：收集基本資訊**
- 簡報者姓名、行業/職業
- 本週主題（必填）
- 目標客戶輪廓（選填）
- 補充背景（選填）

**第二階段：AI 建議三個 LCD 案例**
- AI 根據行業與主題，建議三個適合的服務/場景方向作為 LCD1/LCD2/LCD3
- 使用者可確認、修改、或自行輸入案例方向
- 確認後 AI 展開完整七段架構

---

## 檔案結構

```
index.html              # 主工具介面（兩階段互動）
PROJECT_STATUS.md       # Claude Code / Codex 共用進度與交接紀錄
prompts/
  bni-structure.md      # 核心 prompt 模板（含兩個 prompt：建議案例 + 展開架構）
.claude/
  launch.json           # 本地預覽伺服器設定（python3 http.server 5500）
  skills/
    bni-presenter.md    # Claude Code slash command skill
```

## 開發原則

- 禁止引入外部框架（純原生 HTML/CSS/JS）
- API Key 只傳送至 Google Gemini API；僅在使用者勾選後存入 localStorage
- `prompts/bni-structure.md` 是 prompt 規格來源；因單檔離線需求，執行副本內嵌於 HTML，修改時必須同步
- 輸出格式鎖定 JSON，方便前端結構化渲染
- Gemini 請求使用 JSON Schema，前端渲染前必須再次驗證結構
- 兩階段流程：Step 1 建議案例 → Step 2 展開完整架構
- 每次修改後更新 `PROJECT_STATUS.md` 與 `CHANGELOG.md`

## 目前版本

**v0.4.0**（2026-06-09）— 詳細紀錄見 `CHANGELOG.md`

- UI 採 BNI 紅 + 富聯淺藍 + 白底配色
- 頁面頂部嵌入富聯流程圖（可 lightbox 放大）
- API Key 取得教學（五步驟 + 直連 Google AI Studio）
- 七段架構 + PPT 提示詞雙 Tab 輸出
- API Key 可選擇記住並可一鍵清除
- JSON Schema、回傳驗證與 API 逾時處理

## 待確認事項

- [ ] 流程圖建議改為本地檔案（目前使用外部圖床 ibb.co）
- [ ] 是否需要支援 10 分鐘以外的時間長度
- [ ] 是否需要直接匯出 PDF / Word
- [ ] 章員共用情境的 API Key 管理方案

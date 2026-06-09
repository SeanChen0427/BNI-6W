# BNI 富聯分會 主題簡報架構產生 — 核心 Prompt 模板

總時長 10 分鐘，七段式結構，LCD×3 成功案例，三級引薦。

---

## Prompt A：建議三個 LCD 案例方向

使用時機：使用者填入基本資訊後，先讓 AI 建議三個案例方向。

```
你是 BNI 富聯分會的教育協調委員，熟悉 BNI Feature Presentation 的 LCD 案例結構。

簡報者資訊如下：
---
姓名：{{name}}
行業 / 職業：{{industry}}
本週主題：{{topic}}
目標客戶輪廓：{{targetClient}}
補充背景：{{extra}}
---

請根據以上資訊，建議三個適合作為本次簡報 LCD 成功案例的方向。

每個案例方向包含：
- 案例名稱（短標題，5-10 字）
- 對應的產品或服務項目
- 適合展示的客戶類型

請用繁體中文回覆，格式為 JSON：
{
  "suggestions": [
    {
      "id": 1,
      "title": "案例方向短標題",
      "service": "對應產品或服務",
      "clientType": "適合的客戶類型"
    },
    {
      "id": 2,
      ...
    },
    {
      "id": 3,
      ...
    }
  ]
}

只回傳 JSON，不要加任何額外說明文字。
```

---

## Prompt B：展開完整七段架構

使用時機：使用者確認三個 LCD 案例方向後，展開完整架構。

```
你是 BNI 富聯分會的教育協調委員，熟悉 BNI Feature Presentation 的標準流程。

簡報者資訊：
---
姓名：{{name}}
行業 / 職業：{{industry}}
本週主題：{{topic}}
目標客戶輪廓：{{targetClient}}
補充背景：{{extra}}
---

三個 LCD 成功案例方向（已由簡報者確認）：
LCD1：{{lcd1}}
LCD2：{{lcd2}}
LCD3：{{lcd3}}

三級引薦提示（未填項目由 AI 建議）：
夢幻引薦：{{refDream}}
理想引薦：{{refIdeal}}
一般引薦：{{refGeneral}}

---

請產出完整的 BNI 富聯分會七段式主題簡報架構，總時長 10 分鐘。

結構規格：
1. 標題與說明（30秒）：說明今日標題與分享重點
2. 介紹自己（30秒）：專長、獨特處、專業經歷
3. 介紹公司（30秒）：公司特色、與同業差異、代表性客戶
4. 三個成功案例（6分鐘，每個LCD各2分鐘），每個 LCD 包含：
   A. 產品或服務
   B. 對客戶的效益或解決的問題
   C. 交易引薦對象
   D. 業務人脈圈
   E. 成功案例（含稀好事，說故事細節）
5. 開啟對話（1分鐘）：如何開啟具體對談，給予行動指示
6. 三級引薦（1分鐘）：
   - 夢幻引薦（Biggest Target）
   - 理想引薦（Higher Value）
   - 一般引薦（Low Level Entry）
7. 結語（30秒）：重申重點

每個段落需提供：
- 3-5 個具體內容要點
- 一條可直接使用的話術範例句（自然、口語）

請用繁體中文回覆，格式為 JSON：
{
  "meta": {
    "name": "{{name}}",
    "industry": "{{industry}}",
    "topic": "{{topic}}",
    "totalTime": "10分鐘"
  },
  "sections": [
    {
      "number": 1,
      "name": "標題與說明",
      "time": "30秒",
      "points": ["要點1", "要點2"],
      "starter": "話術範例句"
    },
    {
      "number": 2,
      "name": "介紹自己",
      "time": "30秒",
      "points": [...],
      "starter": "..."
    },
    {
      "number": 3,
      "name": "介紹公司",
      "time": "30秒",
      "points": [...],
      "starter": "..."
    },
    {
      "number": 4,
      "name": "三個成功案例",
      "time": "6分鐘",
      "lcd": [
        {
          "id": 1,
          "title": "LCD1 標題",
          "time": "2分鐘",
          "A": "產品或服務說明",
          "B": "對客戶的效益或解決的問題",
          "C": "交易引薦對象",
          "D": "業務人脈圈",
          "E": "成功案例故事（含稀好事細節）"
        },
        { "id": 2, ... },
        { "id": 3, ... }
      ],
      "starter": "..."
    },
    {
      "number": 5,
      "name": "開啟對話",
      "time": "1分鐘",
      "points": [...],
      "starter": "..."
    },
    {
      "number": 6,
      "name": "三級引薦",
      "time": "1分鐘",
      "referrals": {
        "dream": "夢幻引薦具體描述",
        "ideal": "理想引薦具體描述",
        "general": "一般引薦具體描述"
      },
      "starter": "..."
    },
    {
      "number": 7,
      "name": "結語",
      "time": "30秒",
      "points": [...],
      "starter": "..."
    }
  ]
}

只回傳 JSON，不要加任何額外說明文字。
```

---

## 變數說明

| 變數 | 必填 | 說明 |
|------|------|------|
| `{{name}}` | 否 | 簡報者姓名 |
| `{{industry}}` | 否 | 行業或職業 |
| `{{topic}}` | 是 | 本週主題 |
| `{{targetClient}}` | 否 | 目標客戶輪廓 |
| `{{extra}}` | 否 | 補充背景 |
| `{{lcd1/2/3}}` | 是（第二階段） | 確認後的 LCD 案例方向 |
| `{{refDream/refIdeal/refGeneral}}` | 否 | 使用者指定的三級引薦方向 |

---

## 實作同步規則

- 本檔案是 prompt 規格的主要文件。
- 因工具需維持單一 `index.html` 並支援本地直接開啟，執行時使用的 prompt 會內嵌在 `index.html`。
- 修改本檔案的 Prompt A 或 Prompt B 時，必須在同一次工作同步更新 `index.html` 的 `suggestLCD()` 或 `buildPrompt()`。
- JSON 欄位若有異動，也必須同步更新 `suggestionSchema`、`outlineSchema`、驗證函式與前端渲染函式。

---

## 調整建議

- 若 E（成功案例故事）太通用：在 extra 補上「請讓案例故事有具體數字（金額/時間/百分比）」
- 若三級引薦不夠具體：在 targetClient 填入更細的客戶描述
- 若要強化主題連貫性：在 extra 補上「請讓每個 LCD 案例都呼應本週主題 {{topic}}」

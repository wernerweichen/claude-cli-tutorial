## 什麼是 `CLAUDE.md`？

一個純文字 Markdown 檔案，Claude 會在**每次對話開始時自動讀取**。

- 放置於專案根目錄（或 `~/.claude/CLAUDE.md` 作為使用者層級預設值）
- 作為持久化指示——不需要每次對話都重新說明你的專案
- 把它想成給 AI 協作夥伴的**簡報文件**

```bash
your-project/
└── CLAUDE.md   ← 每次對話自動載入
```

---

## Claude 的查找順序

Claude 依優先順序從多個位置讀取 `.md` 檔案：

```
~/.claude/CLAUDE.md            ← 使用者層級（始終載入）
your-project/CLAUDE.md         ← 專案根目錄（始終載入）
your-project/src/CLAUDE.md     ← 當 Claude 在 src/ 工作時載入
```

在衝突情況下，較具體的檔案優先於較通用的檔案。

---

## 應該放入 `CLAUDE.md` 的內容

```markdown
## 專案概述
管理使用者訂閱的 REST API。Node.js + PostgreSQL。

## 技術棧
- 執行環境：Node.js 20
- 資料庫：PostgreSQL 15（使用 `pg` 函式庫）
- 測試框架：Jest

## 重要指令
- `npm test`          執行所有測試
- `npm run lint`      ESLint + Prettier
- `npm run migrate`   執行資料庫遷移

## 程式慣例
- 資料庫欄位用 snake_case，JS 程式用 camelCase
- 所有 API 端點回傳 `{ data, error }` 格式
- 先寫測試，再實作功能
```

---

## 不應放入的內容

| 不要放這些 | 原因 |
|-----------|------|
| API 金鑰、機密資訊 | 安全風險——檔案會被提交至版本庫 |
| 大量資料 | 每次對話都浪費情境視窗 |
| 複製貼上的程式碼 | 程式碼已可直接閱讀，無需重複 |
| 對話歷史 | `CLAUDE.md` 是指示，不是記錄 |
| 「請友善且簡潔」 | 個性提示詞浪費情境空間 |

**簡單原則：** Claude 能從程式碼庫中讀取的內容，就不要在 `CLAUDE.md` 中重複。

---

## 記憶系統

Claude Code 支援 `memory/` 目錄，用於跨對話持久儲存筆記：

```
~/.claude/projects/<project-hash>/memory/
├── user_profile.md        ← 你是誰、你的工作方式
├── feedback_testing.md    ← Claude 應記住的修正與偏好
└── project_context.md     ← 持續進行的決策與目標
```

告訴 Claude 記住某件事：

> *「記住我們一律使用整合測試，不用 mock。」*

Claude 會寫入記憶檔案，並在 `MEMORY.md` 中建立索引。

---

## 撰寫有效的情境說明

**具體且命令式：**

```markdown
# 模糊（不好）
操作資料庫時要小心。

# 具體（好）
絕不刪除資料表。始終使用 `db/migrations/` 中的遷移腳本。
任何 schema 變更前先執行 `npm run migrate:dry`。
```

**使用標題**，讓 Claude 能快速定位各個段落。

**保持更新**——過時的指示比沒有指示更糟。

---

## 多個 `.md` 檔案

對大型專案，可依功能區域拆分情境：

```
your-project/
├── CLAUDE.md              ← 全專案：技術棧、指令、慣例
├── src/api/CLAUDE.md      ← API 專屬：驗證模式、端點格式
└── src/db/CLAUDE.md       ← 資料庫專屬：schema 說明、遷移規則
```

Claude 在子目錄工作時，會載入最近的 `.md` 檔案。

---

## 改善前後對比

**改善前（模糊）：**
```markdown
這是一個網頁應用程式。請遵循良好實踐。
操作資料庫時要謹慎。
```

**改善後（有效）：**
```markdown
## 技術棧
Next.js 14、Prisma ORM、PostgreSQL、Jest

## 指令
- `npm test`                   執行測試
- `npx prisma migrate dev`     套用遷移

## 規則
- 絕不使用 `prisma.$executeRaw`——請使用型別化查詢
- 所有 API 路由在操作資料庫前必須用 Zod 驗證輸入
```

---

## 常見錯誤

| 錯誤 | 修正方式 |
|------|---------|
| 空白的 `CLAUDE.md` | 至少加入：技術棧、重要指令、程式慣例 |
| 從不更新 | 大型重構後應審視——過時的情境會誤導 Claude |
| 過長（500 行以上） | 拆分至子目錄檔案；刪除多餘條目 |
| 檔案中放了機密 | 使用 `.env`；在 `CLAUDE.md` 中只放環境變數的*名稱*，不放值 |
| 長篇散文段落 | 改用簡短、命令式的條列項目 |

Note: 「改善前後對比」那張投影片最能引起共鳴——給它多一點時間。

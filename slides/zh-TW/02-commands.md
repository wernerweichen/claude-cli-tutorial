## 開始一個對話

```bash
# 在當前目錄開啟互動式對話
claude

# 附帶起始提示詞
claude "解釋 auth 模組的功能"

# 指定模型
claude --model claude-opus-4-8

# 輸出結果後退出（非互動式）
claude -p "摘要這個檔案" < README.md
```

---

## 斜線指令

| 指令 | 功能說明 |
|------|---------|
| `/help` | 列出所有可用指令與技能 |
| `/clear` | 清除對話歷史 |
| `/compact` | 壓縮情境以節省 token |
| `/config` | 開啟設定（模型、主題、權限） |
| `/cost` | 顯示本次對話的 token 使用量 |
| `/memory` | 檢視並編輯記憶檔案 |
| `/status` | 顯示當前模型與情境資訊 |

---

## `!` 前綴用法

在不離開 Claude 的情況下執行 Shell 指令：

```
> !ls -la
> !git status
> !npm test
```

輸出會顯示在終端機中。Claude **不會**看到這些輸出，除非你貼上來。

若要讓 Claude 看到指令輸出，請描述你執行的內容：

```
> 我執行了 `npm test`，得到以下結果：[貼上輸出]
```

---

## 非互動模式：`-p` 旗標

在腳本與管道中使用 Claude：

```bash
# 摘要一個檔案
claude -p "摘要這段內容" < notes.txt

# 生成並輸出至檔案
claude -p "為 Node.js 專案撰寫 .gitignore" > .gitignore

# 與其他工具串接
git diff | claude -p "為這次 diff 撰寫 commit 訊息"
```

`-p` 收到一次回應後即退出，不開啟互動式對話。

---

## `--model` 旗標

為本次對話切換模型：

```bash
# 使用 Opus 進行複雜推理
claude --model claude-opus-4-8

# 使用 Haiku 處理快速、低成本的任務
claude --model claude-haiku-4-5-20251001

# 預設為 Sonnet（速度與能力的平衡點）
claude  # 使用 claude-sonnet-4-6
```

目前的模型 ID：
- Opus 4.8：`claude-opus-4-8`
- Sonnet 4.6：`claude-sonnet-4-6`
- Haiku 4.5：`claude-haiku-4-5-20251001`

---

## 權限模式

控制 Claude 在無需提示的情況下可執行的操作：

| 模式 | Claude 可以... |
|------|--------------|
| 預設 | 讀取檔案；寫入或執行指令前會詢問 |
| 逐工具授權 | 在 `settings.json` 中預先核准特定工具 |
| `--dangerously-skip-permissions` | 無需提示，執行任何操作 |

在 `.claude/settings.json` 中設定逐工具權限：

```json
{
  "permissions": {
    "allow": ["Bash(git *)", "Read", "Edit"]
  }
}
```

---

## 鍵盤快捷鍵

| 快捷鍵 | 功能 |
|--------|------|
| `Ctrl+C` | 取消當前回應 |
| `↑` | 叫回上一個提示詞 |
| `Ctrl+L` | 清除畫面（保留歷史） |
| `Shift+Enter` | 換行而不送出 |
| `Ctrl+R` | 搜尋指令歷史 |
| `/` 開頭 | 觸發斜線指令 |
| `!` 開頭 | 內嵌執行 Shell 指令 |

---

## 對話管理

**情境視窗：** Claude 的情境視窗有限。當它快滿時：
- Claude 會自動壓縮舊訊息
- 可在填滿前手動執行 `/compact`
- 使用 `/clear` 完全重新開始（將失去所有歷史）

**恢復對話：**

```bash
# 恢復上一個對話
claude --continue

# 開啟互動式對話選擇器
claude --resume

# 透過 ID 恢復特定對話
claude --resume <session-id>
```

---

## 快速參考卡

```
claude                    開啟互動式對話
claude -p "..."           單次非互動式執行
claude --model <id>       選擇模型
claude --continue         恢復上一個對話

/help   /clear   /compact   /config   /cost

!<指令>       內嵌執行 Shell 指令
Ctrl+C        取消回應
↑             叫回上一個提示詞
Shift+Enter   換行而不送出
```

Note: 在問答環節保留這張投影片——對聽眾來說是很實用的速查表。

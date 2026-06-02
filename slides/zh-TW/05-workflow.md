## `settings.json` 中的鉤子

鉤子讓你可以在 Claude 生命週期的特定時間點**自動執行 Shell 指令**。

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          { "type": "command", "command": "npm run lint --silent" }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          { "type": "command", "command": "echo 'Session complete'" }
        ]
      }
    ]
  }
}
```

---

## 鉤子事件類型

| 事件 | 觸發時機 |
|------|---------|
| `PreToolUse` | 在 Claude 呼叫任何工具之前 |
| `PostToolUse` | 在 Claude 呼叫工具之後 |
| `Stop` | 當 Claude 完成一次回應時 |
| `Notification` | 當 Claude 發送通知時 |

**`matcher`** 依工具名稱過濾（支援 `|` 指定多個）：
- `"Edit"` — 僅限檔案編輯
- `"Bash"` — 僅限 Shell 指令
- `"Edit|Write"` — 兩者皆可

---

## 範例：每次編輯後自動執行 Lint

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npm run lint --silent 2>/dev/null || true"
          }
        ]
      }
    ]
  }
}
```

Claude 編輯檔案 → ESLint 自動執行 → 下次 Claude 讀取檔案時，看到的是整潔的程式碼。

---

## 工作流程的價值

**立即生效（設定一次，永久運作）：**
- 每次檔案編輯後自動執行 lint/format
- 程式碼變更後自動執行測試
- Claude 完成長時間任務時發送桌面通知

**團隊價值：**
- 將 `.claude/settings.json` 提交至版本庫
- 每位成員都使用相同的鉤子與權限設定
- 新人上手：`git clone` → `claude` → 立即投入生產

Note: 共用 `settings.json` 這個概念最能引起技術主管的共鳴——就像是 AI 行為的 `.editorconfig`。

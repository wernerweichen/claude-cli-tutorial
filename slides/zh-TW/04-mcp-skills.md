## MCP — 模型情境協定

一種將 Claude 連接至**外部工具與資料來源**的協定。

- MCP 伺服器提供工具（Claude 可呼叫的函式）
- 範例：檔案系統存取、網路搜尋、資料庫、GitHub、Slack
- 在 `settings.json` 中設定 Claude 要連接的伺服器

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/your/path"]
    }
  }
}
```

---

## 新增 MCP 伺服器

1. 尋找或建立 MCP 伺服器套件
2. 在 `.claude/settings.json` 的 `mcpServers` 下新增設定
3. 重新啟動 Claude CLI——它會自動連接

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<your-token>"
      }
    }
  }
}
```

Claude 現在可以在對話中直接呼叫 GitHub API 工具。

---

## 技能（Skills）

**技能**是由斜線指令觸發的具名可重用工作流程。

- 透過外掛安裝：`/plugin install <名稱>`
- 以 `/skill-name` 或 `/skill-name 參數` 呼叫
- 給予 Claude 一組結構化的指示來遵循

```
/superpowers:brainstorming    引導式設計對話
/superpowers:writing-plans    從規格書產生實作計畫
/code-review                  審查當前 diff 的錯誤
/superpowers:systematic-debugging  結構化根本原因分析
```

技能將臨時提示轉變為**可重複、可靠的流程**。

---

## 代理（Agents）

Claude 可以生成**子代理**——並行或隔離工作的獨立 Claude 實例。

```
主要 Claude 對話
├── 子代理 A → 研究 auth 模組
├── 子代理 B → 為 API 撰寫測試
└── 子代理 C → 更新文件
```

- 每個子代理有自己的情境視窗
- 結果回傳至主對話
- 用於並行化工作或隔離高干擾的研究任務

---

## 成果物（Artifacts）

**成果物**是 Claude 在對話中寫入磁碟的檔案。

- 原始碼、設定檔、文件、腳本——任何 Claude 建立的檔案
- 透過 `Write` 和 `Edit` 工具建立
- 對話結束後仍然存在——它們是專案中的真實檔案

```bash
# 請 Claude 搭建專案後：
your-project/
├── src/index.ts            ← 成果物
├── tests/index.test.ts     ← 成果物
└── tsconfig.json           ← 成果物
```

審視成果物的方式應與審視同事的 PR 相同。

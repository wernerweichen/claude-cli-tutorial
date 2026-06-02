## Superpowers 外掛

一個為 Claude CLI 增添**結構化工程工作流程**技能的外掛。

沒有它：Claude 是個能力強但形式自由的協作者。

有了它：Claude 遵循有主見、可重複的流程——就像有位從不跳過步驟的資深工程師與你結對。

```bash
/plugin install superpowers@claude-plugins-official
/reload-plugins
```

---

## 安裝 Superpowers

```bash
# 步驟一：安裝外掛
/plugin install superpowers@claude-plugins-official

# 步驟二：套用變更（每次安裝後必須執行）
/reload-plugins

# 驗證已載入——應可看到 superpowers:* 技能列表
/help
```

外掛安裝至 `~/.claude/plugins/`，並在所有對話中持久生效。

---

## 核心技能流程

大多數工程工作遵循以下路徑：

```
/superpowers:brainstorming
    ↓  產生設計規格書
/superpowers:writing-plans
    ↓  產生逐任務實作計畫
/superpowers:subagent-driven-development
    ↓  搭配任務間審查執行計畫
/superpowers:verification-before-completion
    ↓  宣告完成前進行驗證
```

每個技能都是結構化對話——提問、建立成果物，再交棒給下一個技能。

---

## 呼叫技能

```bash
# 開始發想新功能
/superpowers:brainstorming I want to add user authentication

# 審查當前 diff 的錯誤
/code-review

# 深度多代理審查（雲端執行，需計費）
/code-review ultra

# 以結構化根本原因分析除錯失敗的測試
/superpowers:systematic-debugging
```

技能接受自然語言參數。它們讀取情境、提出釐清問題，並引導你完成整個流程。

---

## 為何重要

| 沒有 Superpowers | 有了 Superpowers |
|----------------|----------------|
| 形式自由的提示 | 結構化、可重複的流程 |
| 每次重新說明情境 | 規格書＋計畫＋記憶跨對話持久化 |
| 容易略過步驟 | 檢查清單確保完整性 |
| Claude 猜測你的意圖 | 發想階段在寫程式前先釐清需求 |

**最終收益：** 減少修正 AI 錯誤的時間，把更多精力放在真正的問題上。

Note: 這裡適合暫停讓聽眾提問——很多人會問「它能做 X 嗎？」之類關於特定技能的問題。

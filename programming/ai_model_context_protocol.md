## Model Context Protocol (MCP) 詳細說明

### 什麼是 MCP？

Model Context Protocol（MCP）是一個由 Anthropic 等推動的開放標準協定，目的是讓大型語言模型（如 GPT、Claude）能夠安全且標準化地連接到外部資料來源與工具系統，打破資訊孤島，提升 AI 回應的相關性與準確度[1][3][4]。

#### MCP 結合了三個核心概念：

- Model（模型）：指 AI 模型本身
- Context（脈絡）：指提供給模型的外部資料或上下文
- Protocol（協定）：指一套通用標準，讓模型與資料來源互通有無[3]。

---

### MCP 如何運作？

MCP 透過 JSON-RPC 2.0 訊息格式建立連線，包含三個主要角色：

- Host（主機）：啟動連線的 LLM 應用
- Client（客戶端）：主機內的連接器
- Server（伺服器）：提供資料和工具的服務端[5]。

#### MCP 允許伺服器向客戶端提供三類功能：

- Resources（資源）：資料上下文
- Prompts（提示）：預設的訊息模板和工作流程
- Tools（工具）：AI 可執行的功能[5]。

---

### Web Service 如何因應 MCP？

Web Service 若要支援 MCP，需要實作 MCP 伺服器端，將自身資料和功能以 MCP 標準暴露出來，供 AI 應用（MCP 客戶端）存取。這樣 AI 系統就能直接調用 Web Service 的資料和操作功能，實現雙向安全連接[1][4][5]。

例如：

- 對接 GitHub 的 Web Service，可以讓 AI 直接在 IDE 中完成 Pull Request 的建立，而不需人工操作[3]。
- 企業內部系統如 Slack、Google Drive 等，也可以透過 MCP 伺服器連接，讓 AI 助手能讀取和操作相關資料[1]。

---

### 範例說明

1. AI 驅動的開發工具（IDE）：  
   開發者使用支援 MCP 的 IDE（如 Cursor、Windsurf），AI 模型寫完程式碼後，透過 MCP 直接呼叫 GitHub 伺服器 API，完成 Pull Request 的提交，省去手動流程[3]。

2. 企業資料整合：  
   某公司建立 MCP 伺服器連接 Slack 和 Postgres 資料庫，AI 助手能即時讀取會議記錄與資料庫資訊，提供更精準的回覆和建議[1]。

3. 開發者工具平台：  
   平台如 Replit 和 Sourcegraph 整合 MCP，讓 AI 更好地理解程式碼上下文，提升自動化編碼和錯誤修正效率[1]。

####

---

### 安全與隱私考量

MCP 強調用戶同意與控制，要求明確授權資料存取和工具執行，並採取適當的存取控制與隱私保護措施。實作時需設計用戶介面讓用戶審核和授權 AI 的操作，避免濫用[5]。

---

### 結論

MCP 是 AI 與外部資料和工具安全、高效連接的標準協定，Web Service 可透過實作 MCP 伺服器，使 AI 應用無縫訪問其資料和功能，實現更智慧的自動化與整合[1][3][4][5]。

---

**參考來源:**

[1] https://www.anthropic.com/news/model-context-protocol \
[2] https://modelcontextprotocol.io/introduction \
[3] https://www.explainthis.io/zh-hant/ai/mcp \
[4] https://blog.liu-yucheng.com/2025/03/11/anthropic_mcp/ \
[5] https://modelcontextprotocol.io/specification/2025-03-26 \
[6] https://botpress.com/zh-tw/blog/model-context-protocol \
[7] https://openai.github.io/openai-agents-python/mcp/ \
[8] https://cn.linkedin.com/posts/keithlihk_ai-%E6%96%B0%E6%A8%99%E6%BA%96model-context-protocol-mcp5-%E5%88%86%E9%90%98%E6%90%9E%E6%87%82-activity-7314289171097964546-muoS

---

[返回目錄](./../README.md)

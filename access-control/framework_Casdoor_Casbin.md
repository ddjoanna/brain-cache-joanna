# Casdoor 與 Casbin 關係

> Casdoor 與 Casbin 是兩個功能互補的開源框架，分別專注於身份驗證（Authentication）與權限管理（Authorization），可無縫結合使用以實現完整的用戶認證與授權控制。

---

## Casdoor（身份驗證）

- **功能定位**：提供用戶身份驗證和單點登入（SSO）服務，解決用戶管理、登入、註冊等問題。
- **核心特點**：
  - 基於 OAuth 2.0 / OpenID Connect 標準，支持多種第三方登入（如 GitHub、Google、微信、QQ 等）。
  - 提供用戶、角色、組織和客戶端管理界面。
  - 登入成功後生成包含用戶身份和角色信息的 JWT Token。
  - 支持多語言、多租戶，並可集成短信驗證、郵件驗證等安全功能。
- **使用場景**：作為統一身份認證平台，支持多應用單點登入，簡化身份管理流程。
- **擴展性**：提供多種 SDK（JavaScript、Go、Java、Python 等）和插件，方便集成到各類應用。

---

## Casbin（權限管理）

- **功能定位**：靈活的訪問控制框架，用於定義和執行複雜的存取控制策略。
- **核心特點**：
  - 支持多種訪問控制模型：ACL、RBAC、ABAC 及自定義策略。
  - 核心組件為 Enforcer，負責根據策略模型和規則驗證用戶是否有權限訪問資源。
  - 策略存儲可靈活配置，支持文件、數據庫等多種後端。
  - 支持細粒度控制，能根據用戶、資源、操作等多維度判斷權限。
- **使用場景**：API 訪問控制、微服務權限管理、企業級角色與權限分配等。

---

## Casdoor 與 Casbin 的結合流程

1. **身份驗證階段（Casdoor）**

   - 用戶通過 Casdoor 登入，Casdoor 驗證身份並生成 JWT Token，Token 內含用戶身份與角色資訊。

2. **權限驗證階段（Casbin）**
   - 應用解析 Casdoor Token，獲取用戶身份與角色。
   - 使用 Casbin Enforcer 根據策略判斷用戶是否有權限訪問特定資源或執行操作。

---

## 兩者比較表

| 比較項目         | Casbin                                    | Casdoor                         |
| ---------------- | ----------------------------------------- | ------------------------------- |
| 主要功能         | 權限管理（Authorization）                 | 身份驗證（Authentication）      |
| 目標             | 定義與執行存取控制策略                    | 用戶管理、登入與單點登入（SSO） |
| 核心組件         | Enforcer + Adapter                        | 用戶、角色與客戶端管理          |
| 實現方式         | 基於策略模型（Policy）和匹配器（Matcher） | 基於 OAuth 2.0、JWT 等標準      |
| 角色分配         | 配合策略靈活控制                          | 後台管理角色或組織              |
| 是否強制執行權限 | 是（通過 Enforcer）                       | 否（需配合 Casbin 或其他工具）  |
| 使用場景         | 判斷用戶存取權限                          | 確認用戶身份並分配角色          |

---

總結來說，**Casdoor 解決用戶身份認證與管理問題，Casbin 則負責基於身份資訊進行細粒度的權限控制**。兩者結合可構建安全、靈活且易於管理的認證授權系統。

---

**參考來源:**

[1] https://casdoor.github.io/zh/docs/permission/permission-configuration/ \
[2] https://casbin.com/tiktok-illegally-collecting-data-sharing-with-china/ \
[3] https://blog.csdn.net/douke0320/article/details/122266276 \
[4] https://casdoor.org/pdf/Casdoor_Docs_zh.pdf \
[5] https://www.cnblogs.com/casbin/p/16136664.html \
[6] https://studygolang.com/articles/35394 \
[7] https://casbin.com/cakemail-review-design-custom-emails/ \
[8] https://blog.csdn.net/douke0320/article/details/126476389

---

[返回目錄](./../README.md)

# 存取控制模型 RBAC / ABAC / ACL

> 關於三大存取控制模型 RBAC、ABAC 與 ACL 的整理，涵蓋定義、運作方式、優缺點及比較

## RBAC（基於角色的存取控制）

**定義**  
RBAC（Role-Based Access Control）是基於「角色」來管理權限的存取控制模型。權限與角色綁定，使用者透過被指派角色來獲得相應權限。

**運作方式**

- 定義角色（如管理者、工程師、訪客）
- 角色綁定權限（如管理者可讀寫所有資料）
- 使用者被分配角色，繼承角色權限

**優點**

- 易於管理，透過角色統一管理權限
- 適合大規模組織，角色擴展性佳
- 保持一致性與安全性，減少錯誤配置

**缺點**

- 權限較不靈活，無法根據情境（時間、地點等）調整
- 角色數量可能爆炸，增加管理負擔

---

## ABAC（基於屬性的存取控制）

**定義**  
ABAC（Attribute-Based Access Control）根據使用者、資源及環境的屬性動態評估存取權限。

**運作方式**

- 定義多種屬性（如使用者職稱、資源機密等級、存取時間）
- 設定基於屬性的存取政策
- 系統根據屬性與政策動態決定授權

**優點**

- 高度靈活，能根據多種條件動態調整權限
- 適用於安全要求高、權限變動頻繁的場景
- 減少角色數量，避免角色爆炸問題

**缺點**

- 政策設計與管理較複雜
- 即時屬性評估可能影響效能

---

## ACL（存取控制清單）

**定義**  
ACL 為每個資源維護一份清單，列出可存取該資源的使用者或群組及其權限。

**運作方式**

- 直接在資源上設定允許或拒絕的使用者/群組及其權限
- 存取時系統檢查 ACL 決定是否授權

**優點**

- 控制粒度細，針對單一資源設定權限
- 簡單直觀，適合小型系統或單一資源管理

**缺點**

- 管理複雜度高，資源和用戶量大時難維護
- 缺乏動態條件判斷能力
- 效能較低，存取時需查詢大量 ACL

---

## RBAC / ABAC / ACL 比較

| 特性         | RBAC                     | ABAC                         | ACL                          |
| ------------ | ------------------------ | ---------------------------- | ---------------------------- |
| 存取控制方式 | 角色綁定權限             | 根據多種屬性動態判斷         | 資源對用戶/群組的權限清單    |
| 管理難度     | 容易（角色管理）         | 複雜（屬性與政策設計）       | 複雜（大量資源清單維護）     |
| 彈性         | 較低（固定角色）         | 高（多維屬性條件）           | 中（細粒度但無動態條件）     |
| 適用場景     | 角色明確、權限較穩定組織 | 權限頻繁變動、高安全需求場景 | 小型系統或特定資源細粒度控制 |
| 角色數量     | 可能大量角色             | 無需大量角色                 | 無角色概念                   |
| 效能         | 高效                     | 可能影響效能                 | 較低                         |
| 存取控制單位 | 角色                     | 使用者、資源、環境屬性       | 使用者或群組                 |

---

## 如何選擇？

- **ACL** 適合小規模、簡單的系統，管理單一或少量資源。
- **RBAC** 適合角色明確、權限變化較少的企業環境，是 Kubernetes 的主流選擇。
- **ABAC** 適合權限複雜且需動態調整的場景，如金融、政府、雲端服務。

企業可混合使用，例如以 RBAC 作為基礎，再用 ABAC 進行細粒度條件限制，兼顧管理簡單與靈活性。

---

## 簡單 RBAC 範例說明（Casbin 模型）

- 定義角色與權限關係
- 使用者綁定角色
- 查詢使用者對資源的操作權限

```plaintext
[request_definition]
r = sub, obj, act

[policy_definition]
p = sub, obj, act

[role_definition]
g = _, _

[policy_effect]
e = some(where (p.eft == allow))

[matchers]
m = g(r.sub, p.sub) && r.obj == p.obj && r.act == p.act
```

範例政策：

| 類型 | 主體        | 資源        | 操作 |
| ---- | ----------- | ----------- | ---- |
| p    | user_group1 | /home/file  | r    |
| p    | user_group1 | /home/file  | w    |
| p    | user_group2 | /home/file  | x    |
| g    | user1       | user_group1 |
| g    | user2       | user_group1 |
| g    | user3       | user_group2 |

權限查詢示例：

- `enforce("user1", "/home/file", "r")` → true
- `enforce("user1", "/home/file", "x")` → false
- `enforce("user3", "/home/file", "x")` → true

---

以上整理結合多個來源，涵蓋 RBAC、ABAC、ACL 的核心概念與 Kubernetes 中 RBAC 的實踐，幫助理解與選擇合適的存取控制模型。

---

**參考來源:**

[1] https://blog.csdn.net/m0_37163942/article/details/83652065 \
[2] https://www.cnblogs.com/dadadechengzi/p/12598464.html \
[3] https://blog.fleeto.us/post/rbac-in-kubernetes/ \
[4] https://www.cnblogs.com/jpfss/p/11210653.html \
[5] https://blog.csdn.net/panfengyun12345/article/details/72886897 \
[6] https://www.elecfans.com/d/2066340.html \
[7] https://developer.aliyun.com/article/679597 \
[8] https://www.moonpm.com/998.html

---

[返回目錄](./../README.md)

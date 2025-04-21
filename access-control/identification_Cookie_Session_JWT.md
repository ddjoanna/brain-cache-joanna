# Cookie vs Session vs JWT

> Cookie、Session 與 JWT（JSON Web Token）都是用來解決 HTTP 無狀態（stateless）問題的身份驗證與狀態管理機制，但三者在用途、存放位置與實作方式上有明顯差異。

---

## Cookie

- **定義**：Cookie 是瀏覽器儲存的少量資料，通常用來保存用戶識別資訊，如 Session ID。
- **特性**：
  - 由伺服器透過 HTTP 回應頭設定，瀏覽器會自動帶入後續請求。
  - 可設定有效期限、作用域（Domain、Path）、安全屬性（Secure、HttpOnly）。
- **用途**：保持用戶狀態，如登入狀態、偏好設定。
- **缺點**：容量有限（約 4KB），且容易受到 CSRF 攻擊。

---

## Session

- **定義**：Session 是伺服器端儲存的用戶狀態資料，通常與 Cookie 搭配使用，Cookie 中保存 Session ID。
- **運作流程**：
  1. 用戶首次登入，伺服器建立 Session 並生成唯一 Session ID。
  2. Session ID 透過 Cookie 傳送給瀏覽器。
  3. 瀏覽器後續請求帶上該 Cookie，伺服器根據 Session ID 取得對應狀態。
- **優點**：資料存放於伺服器端，安全性較高，能存儲大量狀態資訊。
- **缺點**：伺服器需維護 Session 狀態，擴展性較差，分布式環境需額外同步。

---

## JWT（JSON Web Token）

- **定義**：JWT 是一種基於 JSON 的開放標準（RFC 7519），用於安全地在客戶端和伺服器間傳遞身份驗證和授權資訊的令牌。
- **結構**：由三部分組成，使用 `.` 分隔：
  - Header（標頭）：描述令牌類型與簽名算法。
  - Payload（有效載荷）：包含用戶資訊及聲明（Claims），如用戶 ID、過期時間等。
  - Signature（簽名）：用密鑰對 Header 和 Payload 進行簽名，確保資料完整性與真實性。
- **運作流程**：
  1. 用戶登入成功後，伺服器簽發 JWT。
  2. 客戶端保存 JWT（通常在 LocalStorage 或 Cookie）。
  3. 後續請求在 HTTP Header（Authorization: Bearer ）攜帶 JWT。
  4. 伺服器驗證 JWT 簽名與有效性，授權訪問。
- **優點**：
  - 無狀態（Stateless），伺服器無需存儲會話資料，易於擴展。
  - 可跨域使用，適合前後端分離架構。
- **缺點**：
  - JWT 一旦簽發，無法單獨銷毀（除非設計黑名單機制）。
  - Payload 可被解碼，故不宜存放敏感資料。
  - 若存放於 LocalStorage，易受 XSS 攻擊。

---

## 三者比較

| 特性     | Cookie             | Session                 | JWT                              |
| -------- | ------------------ | ----------------------- | -------------------------------- |
| 資料存放 | 客戶端瀏覽器       | 伺服器端                | 客戶端（LocalStorage 或 Cookie） |
| 狀態管理 | 無狀態，存少量資料 | 有狀態，伺服器維護      | 無狀態，資料自包含               |
| 擴展性   | 好                 | 較差（需 Session 同步） | 好（無需伺服器存儲）             |
| 安全性   | 易受 CSRF 攻擊     | 較高                    | 需防範 XSS，且無法即時撤銷       |
| 使用場景 | 簡單狀態存儲、追蹤 | 傳統網站登入狀態管理    | 前後端分離、分布式認證           |

---

**參考來源:**

[1] https://tw.alphacamp.co/blog/jwt-json-web-token \
[2] https://www.alibabacloud.com/help/tc/api-gateway/traditional-api-gateway/user-guide/jwt-based-authentication \
[3] https://kucw.io/blog/jwt/ \
[4] https://hackmd.io/@yy933/Sy50KyJen \
[5] https://www.explainthis.io/zh-hant/swe/jwt \
[6] https://ithelp.ithome.com.tw/articles/10334612 \
[7] https://ithelp.ithome.com.tw/articles/10359582 \
[8] https://vocus.cc/article/65084dccfd8978000128375f

---

[返回目錄](./../README.md)

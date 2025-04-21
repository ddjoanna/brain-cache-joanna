# JWT

> JSON Web Token（JWT）是一種基於 JSON 的開放標準（RFC 7519），用於在網路應用環境中安全且緊湊地傳遞聲明（Claims）。它的設計目的是實現無狀態的用戶身份認證與授權，特別適合分布式系統和跨域認證場景[1][2][6]。

## JWT 的結構

JWT 由三個部分組成，彼此以「.」分隔：

1. **Header（標頭）**

   - 描述 JWT 的類型（通常是 "JWT"）和簽名演算法（如 HMAC SHA256、RSA 等）。
   - 範例：
     ```json
     {
       "alg": "HS256",
       "typ": "JWT"
     }
     ```

2. **Payload（有效載荷）**

   - 包含聲明（Claims），即要傳遞的資訊。
   - 聲明分為三類：
     - Registered Claims（註冊聲明）：如 `iss`（發行者）、`exp`（過期時間）、`sub`（主題）、`aud`（受眾）等標準欄位。
     - Public Claims（公開聲明）：可自由定義但需避免衝突。
     - Private Claims（私有聲明）：自訂的業務資料。
   - 範例：
     ```json
     {
       "sub": "1234567890",
       "name": "John Doe",
       "iat": 1516239022
     }
     ```

3. **Signature（簽名）**
   - 將 Header 和 Payload 先進行 Base64Url 編碼後，用指定的密鑰和演算法簽名，確保資料未被竄改。
   - 計算方式類似：
     ```
     HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)
     ```

整體格式類似：

```
xxxxx.yyyyy.zzzzz
```

其中 xxxxx 是 Header 的編碼，yyyyy 是 Payload 的編碼，zzzzz 是簽名。

## JWT 的運作流程

1. 使用者登入時，伺服器驗證身份後，生成包含用戶資訊的 JWT，並回傳給客戶端。
2. 客戶端將 JWT 儲存（通常在 LocalStorage 或 Cookie 中）。
3. 後續請求時，客戶端在 HTTP Header 的 `Authorization` 欄位以 `Bearer ` 形式帶上 JWT。
4. 伺服器收到請求後，驗證 JWT 的簽名與有效性（如是否過期），若通過則認定用戶身份，允許存取資源。

此流程使伺服器無需保存 session 狀態，達成無狀態認證[1][4][5]。

## JWT 的優點

- **無狀態（Stateless）**：伺服器不需保存用戶狀態，易於擴展與分布式部署。
- **跨域認證友好**：適合多服務、多域名的單點登入（SSO）場景。
- **自包含（Self-contained）**：Token 本身包含用戶資訊，減少伺服器查詢。
- **輕量且緊湊**：適合網路傳輸，尤其是移動端和 SPA 應用。
- **標準化**：廣泛支持多種語言與框架。

## JWT 的缺點與風險

- **無法單獨銷毀**：JWT 在過期前有效，無法像 session 一樣即時登出或作廢，除非設計額外機制。
- **安全風險**：若 Token 被竊取，攻擊者可冒用身份，需妥善保護 Token（避免 XSS、CSRF）。
- **Payload 不加密**：資料以 Base64Url 編碼，非加密，敏感資訊不應放入 Payload。
- **LocalStorage 安全問題**：存放在 LocalStorage 容易被腳本讀取，存在安全隱患。
- **Token 大小限制**：過大可能影響傳輸效率。

## 適用場景

- **用戶身份認證與授權**：尤其是分布式系統、微服務和跨域應用。
- **單點登入（SSO）**：多個相關服務共享認證狀態。
- **API 認證**：輕量且無狀態的 API 安全驗證。
- **短期存取令牌**：如一次性操作或短期有效的授權。

---

### 總結

JWT 是一種基於 JSON 的安全令牌格式，通過數位簽名保證資料完整性，實現無狀態的用戶認證和授權。它適合現代分布式架構和跨域認證，但在使用時需注意安全性設計與令牌管理。

---

**參考來源:**

[1] https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html \
[2] https://www.cnblogs.com/sevents/articles/17214299.html \
[3] https://juejin.cn/post/7002904348212592654 \
[4] https://www.explainthis.io/zh-hans/swe/jwt \
[5] https://kucw.io/blog/jwt/ \
[6] https://cloud.tencent.com/developer/article/1460770 \
[7] https://yen0304.github.io/p/jwtjson-web-token%E5%8E%9F%E7%90%86%E4%BB%8B%E7%B4%B9%E5%AF%A6%E4%BD%9Cjws/ \
[8] https://blog.csdn.net/gulugulu1103/article/details/134588693

---

[返回目錄](./../README.md)

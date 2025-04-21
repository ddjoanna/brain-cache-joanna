## OAuth 簡介

OAuth 是一種開放標準的授權協議，允許第三方應用程式在不直接取得使用者帳號密碼的情況下，代表使用者存取受保護的資源。它主要解決了授權過程中的安全性和便利性問題，廣泛應用於社交平台、API 授權等場景。

---

## OAuth 1.0 與 OAuth 2.0 的差異

| 比較項目       | OAuth 1.0                                              | OAuth 2.0                                                                   |
| -------------- | ------------------------------------------------------ | --------------------------------------------------------------------------- |
| **安全機制**   | 需要對每個請求進行複雜的簽名（簽名基於密鑰和請求內容） | 放棄簽名，依賴 HTTPS（TLS）加密保障安全                                     |
| **協議性質**   | 嚴格的協議規範                                         | 更像是一個框架，允許多種授權流程和擴展                                      |
| **角色定義**   | Service Provider（服務提供者）角色單一                 | 將 Service Provider 拆分為 Resource Server 與 Authorization Server 兩個角色 |
| **授權流程**   | 流程較複雜，簽名計算繁瑣                               | 流程簡化，提供多種授權類型（授權碼模式、隱式模式、密碼模式、客戶端模式）    |
| **Token 類型** | Token 有對應的 Secret，需簽名驗證                      | Token 簡化為 Access Token，通常為短期有效，支持 Refresh Token               |
| **兼容性**     | 不兼容 OAuth 2.0                                       | 不兼容 OAuth 1.0，為全新設計                                                |
| **適用場景**   | 適合需要高安全性且支持簽名的應用                       | 適合多種應用場景，包含 Web、移動端、桌面應用及 API 授權                     |
| **實現難度**   | 複雜，開發與維護成本較高                               | 簡單，開發者友好，支持更多授權場景                                          |

---

## OAuth 2.0 主要角色

- **Resource Owner（資源所有者）**：通常是最終使用者，擁有受保護的資源。
- **Client（客戶端）**：代表資源所有者訪問資源的應用程式。
- **Authorization Server（授權伺服器）**：負責認證資源所有者並發放授權令牌（Access Token）。
- **Resource Server（資源伺服器）**：存放受保護資源，根據 Access Token 決定是否授權存取。

---

## OAuth 2.0 授權流程簡述（以授權碼模式為例）

1. Client 將使用者導向 Authorization Server 登入並授權。
2. Authorization Server 驗證使用者身份，並返回授權碼（Authorization Code）給 Client。
3. Client 使用授權碼向 Authorization Server 申請 Access Token。
4. Authorization Server 發放 Access Token。
5. Client 使用 Access Token 向 Resource Server 請求受保護資源。
6. Resource Server 驗證 Access Token，若有效則返回資源。

---

## 總結

- **OAuth 1.0** 的簽名機制在理論上能提供強請求完整性保障，但複雜且容易實作錯誤，且存在已知安全漏洞需要修補。
- **OAuth 2.0** 放棄複雜簽名，依賴 HTTPS 保護通訊安全，並引入更多安全設計（如回調地址驗證、Token 續期等），整體安全性更強且更適合現代應用。
- 因此，OAuth 2.0 是對 OAuth 1.0 的安全性和易用性的升級，並非 OAuth 1.0 比 OAuth 2.0 更安全。

OAuth 2.0 是目前主流的授權標準，廣泛應用於現代網路服務與移動應用中。

---

**參考來源:**

[1] https://blog.csdn.net/ivolcano/article/details/90414175 \
[2] https://www.zhihu.com/question/19851243 \
[3] https://lepture.com/zh/2018/oauth2-intro \
[4] https://blog.csdn.net/qq_38941937/article/details/112444312 \
[5] https://workos.com/blog/oauth-vs-oauth-2-differences-what-you-need-to-know \
[6] https://yu-jack.github.io/2020/04/27/oauth-implement/ \
[7] https://developer.aliyun.com/article/491683 \
[8] https://www.technice.com.tw/experience/12520/

---

[返回目錄](./../README.md)

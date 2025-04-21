# 加密（Encryption）

> 加密（Encryption）是一種利用數學演算法將原始資料（明文）轉換成不可讀的密文的技術，目的是保護資料在傳輸或儲存過程中的機密性，防止未授權者取得或竄改資訊。

## 加密的基本原理

- **明文（Plaintext）**：原始可讀的資料。
- **密文（Ciphertext）**：加密後的不可讀資料。
- **加密演算法（Encryption Algorithm）**：將明文轉換成密文的數學方法。
- **解密演算法（Decryption Algorithm）**：將密文還原成明文的過程。
- **密鑰（Key）**：加密和解密過程中使用的秘密參數，密鑰的安全性直接影響加密強度。

加密技術依密鑰使用方式可分為：

- **對稱加密**：加密與解密使用相同密鑰，速度快但密鑰管理較複雜。
- **非對稱加密（公私鑰加密）**：使用一對公鑰和私鑰，公鑰用於加密，私鑰用於解密，方便密鑰分發與身份驗證。

## 加密的核心功能與應用

- **資料保密性**：確保資料內容不被未授權者讀取。
- **資料完整性**：結合數位簽章與雜湊函數，確保資料未被竄改。
- **身份驗證**：透過加密簽章確認資料來源的真實性。
- **授權控制**：配合權杖（Token）與角色基礎存取控制（RBAC）管理使用者權限。

## 加密技術在現代系統中的應用

- **傳輸層加密**：如 TLS/SSL，保障網路傳輸資料安全，防止竊聽與中間人攻擊。
- **資料靜態加密**：資料庫或存儲系統中資料加密，防止資料外洩。
- **服務間加密**：微服務架構中，服務間通信多使用雙向 TLS（mTLS）加密，確保服務間身份驗證與資料安全。
- **API Token 與 JWT**：利用非對稱加密簽章技術，確保 Token 的真實性與防篡改，實現分散式身份認證與授權。
- **零信任安全模型**：結合加密技術與動態存取控制，實現細粒度的安全政策執行。

## 加密的安全特性

- **雪崩效應（Avalanche Effect）**：加密演算法的一種理想特性，輸入的微小變化會導致輸出大幅改變，增加破解難度。
- **數位簽章**：利用私鑰加密資料摘要，接收方用公鑰驗證，確保資料來源與完整性。
- **密鑰管理**：安全的密鑰生成、儲存、分發與更新是整體加密安全的關鍵。

## 加密的優缺點

| 優點                               | 缺點                                   |
| ---------------------------------- | -------------------------------------- |
| 保護資料機密性與完整性             | 加密與解密過程會消耗計算資源           |
| 支援身份驗證與授權控制             | 密鑰管理複雜，密鑰洩漏會導致安全風險   |
| 適用於多種場景（傳輸、存儲、認證） | 不當實作或使用弱演算法可能導致安全漏洞 |

---

## 結論

加密是資訊安全的基石，透過數學演算法和密鑰管理，保障資料在傳輸與儲存過程中的機密性、完整性與可驗證性。現代分布式系統與微服務架構廣泛採用加密技術，結合 TLS、mTLS、數位簽章與權杖機制，實現安全可靠的資料交換與身份認證。

---

**參考來源:**

[1] https://github.com/linvon/blogs/blob/master/%E5%88%86%E5%B8%83%E5%BC%8F%E5%BC%82%E6%AD%A5%E5%B7%A5%E4%BD%9C%E6%B5%81--Temporal%20%E4%BB%8B%E7%BB%8D%E4%B8%8E%E4%BD%BF%E7%94%A8%20.md \
[2] https://ikala.cloud/blog/application-modernization/cloud-service-platform-white-paper-2 \
[3] https://www.netadmin.com.tw/netadmin/zh-tw/technology/7D13ABD7390F4A94B796C738420D8660 \
[4] https://code2life.top/blog/0070-temporal-notes \
[5] https://columns.chicken-house.net/2016/12/01/microservice7-apitoken/ \
[6] https://www.reddit.com/r/ExperiencedDevs/comments/13s8kdb/opinions_about_temporalio_microservice/?tl=zh-hant \
[7] https://www.intel.com.tw/content/www/tw/zh/cloud-computing/microservices.html \
[8] https://cloud.tencent.com/developer/article/1812615

---

[返回目錄](./../README.md)

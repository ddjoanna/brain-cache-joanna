# 不安全的加密存儲

> Insecure Cryptographic Storage（不安全的加密存儲）指的是系統在保護敏感資料時，未能正確或充分使用安全的加密技術，導致資料即使被加密，仍可能被攻擊者破解或取得明文，造成資料洩露與安全風險。

## 不安全加密存儲的常見問題

- **使用弱加密演算法**：例如過時的 DES、MD5 等，容易被暴力破解或碰撞攻擊。
- **加密金鑰管理不當**：金鑰未妥善保護、存放於不安全位置或未加密，攻擊者可直接取得金鑰解密資料[1][7][8]。
- **未加密敏感資料**：部分敏感欄位（如密碼、個資）未經加密或雜湊處理直接存儲[2]。
- **缺乏端到端加密**：資料在傳輸和靜態存儲階段未全面加密，易被攔截或竊取[6]。
- **加密範圍不足**：部分日誌檔、暫存檔、非結構化資料未加密，成為攻擊目標[5]。

## 影響

- 敏感資料（密碼、個人資訊、財務資料）被破解或洩露。
- 攻擊者可利用取得的資料進行身份盜用、詐騙或系統入侵。
- 企業面臨法律責任與信譽損失。

## 解決方案與最佳實踐

- **採用強加密演算法**：使用現代且經過驗證的演算法，如 AES、ChaCha20，避免使用過時算法[2][8]。
- **安全的金鑰管理**：加密金鑰必須存放於安全、受控環境（如硬體安全模組 HSM），並定期輪換[1][7]。
- **全面加密敏感資料**：包括資料庫欄位、備份、日誌及暫存檔等均應加密保護[5][6]。
- **端到端加密**：確保資料在傳輸和靜態存儲過程中均被加密，防止中途攔截。
- **使用透明加密技術**：如檔案級加密，確保資料即使被竊取也無法解密使用[5]。
- **密碼安全儲存**：密碼應使用強雜湊函式（如 bcrypt、Argon2）並加鹽處理。
- **定期安全審計與測試**：檢查加密實施是否符合標準，及早發現弱點。

---

總結來說，不安全的加密存儲主要是因為加密技術選擇不當、金鑰管理疏忽或加密範圍不足，導致敏感資料暴露風險。透過採用強加密算法、嚴格的金鑰管理和全面加密措施，能有效保護資料安全，防止資料洩露與攻擊。

---

**參考來源:**

[1] https://cloud.google.com/learn/what-is-encryption \
[2] https://blog.csdn.net/quiet_girl/article/details/50608959 \
[3] https://www.fortinet.com/tw/resources/cyberglossary/encryption \
[4] https://www.kaspersky.com.hk/resource-center/definitions/encryption \
[5] https://www.secureage.com/secureage/pdf/SecureAge-Technology-Whitepaper-2020-Using-Transparent-Encryption-to-Defeat-12-Common-Data-Breaches-TW.pdf \
[6] https://www.solix.com/zh-TW/blog/learning/encrypted-storage-box-locations/ \
[7] https://www.fortinet.com/tw/resources/cyberglossary/what-is-cryptography \
[8] https://zh.wikipedia.org/zh-tw/%E8%B3%87%E6%96%99%E5%8A%A0%E5%AF%86%E6%A8%99%E6%BA%96

---

[返回目錄](./../README.md)

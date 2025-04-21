# Insecure Direct Object Reference

> Insecure Direct Object Reference（IDOR， 不安全的直接物件引用）是一種常見的存取控制漏洞，發生在應用程式直接使用使用者輸入的識別符（如 URL 參數、表單欄位）來訪問內部物件（如資料庫記錄、檔案等），但未對使用者是否有權限存取該物件進行適當驗證。

## IDOR 的原理與範例

- 應用程式會根據使用者提供的 ID 直接存取物件，例如：
  ```
  https://example.com/users/123
  ```
  這裡的「123」是使用者資料的識別碼。若攻擊者將「123」改為「124」且系統未驗證是否有權限查看該 ID 的資料，就可能讀取或修改他人的資料。
- 另一例子是表單中隱藏欄位包含使用者 ID，若伺服器端未驗證權限，攻擊者可修改該欄位來更新他人資料。

## IDOR 可能造成的危害

- 未授權資料洩漏（如個人資訊、交易明細）。
- 未授權資料修改或刪除。
- 橫向或縱向權限提升（存取其他用戶或管理員資源）。
- 取得系統敏感資源（檔案、訊息等）。

## 防範措施

- **嚴格的存取控制檢查**：每次存取物件前，必須驗證當前使用者是否有權限。
- **避免直接暴露可預測的識別符**：使用複雜且不可預測的 ID（如 UUID、隨機字串）作為物件識別。
- **從會話或認證資訊中取得使用者身份**，避免依賴使用者輸入的 ID。
- **限制物件查詢範圍**：例如只在使用者可訪問的資料集合中查找物件。
- **使用白名單或授權框架**，結構化管理權限檢查。
- **避免在 URL 或表單中直接傳遞敏感物件 ID**，改用服務端管理狀態。

---

簡言之，IDOR 是因為缺乏適當的授權驗證，導致攻擊者能透過修改物件識別碼，直接存取或操作未授權的內部資源。防範 IDOR 的核心在於嚴格的存取控制和避免直接暴露可猜測的物件識別符。

（資料來源：OWASP IDOR 防範說明[1]、PortSwigger 安全教學[2]、OWASP 測試指南[3]）

---

**參考來源:**

[1] https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html \
[2] https://portswigger.net/web-security/access-control/idor \
[3] https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/05-Authorization_Testing/04-Testing_for_Insecure_Direct_Object_References \
[4] https://www.spiceworks.com/it-security/vulnerability-management/articles/insecure-direct-object-reference-idor/ \
[5] https://nordvpn.com/cybersecurity/glossary/insecure-direct-object-references/ \
[6] https://en.wikipedia.org/wiki/Insecure_direct_object_reference \
[7] https://highon.coffee/blog/insecure-direct-object-reference-idor/ \
[8] https://www.spanning.com/blog/insecure-direct-object-reference-web-based-application-security-part-6/

---

[返回目錄](./../README.md)

# Injection Flaws

> Injection Flaws（注入漏洞）是指攻擊者將惡意的程式碼或指令注入到應用程式中，並被當成指令或查詢執行，從而操控系統或竊取資料的一類安全漏洞[1][3][8]。

## 原理

- 攻擊者透過輸入欄位、URL 參數等將惡意資料送入系統，系統未對輸入進行適當過濾或轉義，導致惡意程式碼被解釋器（如資料庫、作業系統命令行）當成指令執行[1][2][4]。
- 這類漏洞常見於 SQL Injection（SQL 注入）、Command Injection（命令注入），甚至 XSS 也屬於注入攻擊的一種[2]。

## 常見類型

- **SQL Injection**：攻擊者插入惡意 SQL 語句，能繞過認證、竊取或修改資料庫資料。
- **Command Injection**：惡意命令被注入並在伺服器作業系統層執行，可能導致系統被完全控制。
- 其他如 LDAP 注入、XPath 注入等也是注入漏洞的變種。

## 攻擊危害

- 取得系統管理權限或資料庫管理權限。
- 竊取敏感資料（帳號、密碼、個資）。
- 修改或刪除資料，破壞系統完整性。
- 執行任意系統命令，植入後門或惡意軟體。
- 破壞企業信譽與用戶信任。

## 防範措施

1. **輸入驗證與過濾**：使用白名單限制輸入字元，避免特殊字元被當作指令執行[2][6]。
2. **參數化查詢（Prepared Statements）**：避免直接拼接 SQL 語句，使用參數化查詢或 ORM 框架[8]。
3. **最小權限原則**：資料庫及系統帳號權限限制，避免攻擊者取得過高權限[2]。
4. **錯誤訊息隱藏**：避免將系統或資料庫錯誤訊息暴露給使用者，減少攻擊者情報[2]。
5. **定期安全掃描與代碼審查**：及早發現注入漏洞並修補[3]。
6. **使用安全框架與函式庫**：利用現有安全工具防止注入。

---

Injection Flaws 是網路應用中最常見且危害嚴重的安全漏洞之一，攻擊者藉由操控輸入資料改變系統行為，造成資料外洩、系統入侵等嚴重後果。透過嚴謹的輸入控制、參數化查詢與權限管理等多層防護措施，可有效降低此類風險[1][2][3][8]。

---

**參考來源:**

[1] https://www.gss.com.tw/eis/168-eis89/1787-eis89-6 \
[2] https://tech-blog.cymetrics.io/posts/jo/zerobased-injectionattack/ \
[3] https://www.gss.com.tw/eis/59-eis48/290-owasp-top10 \
[4] https://blog.csdn.net/ly471911182/article/details/44876751 \
[5] https://i30101000023b.nc.com.tw/modules/news/article.php?storyid=45 \
[6] https://blog.trendmicro.com.tw/?p=57572 \
[7] https://blog.csdn.net/woohooli/article/details/1785897 \
[8] https://owasp.org/www-community/Injection_Flaws

---

[返回目錄](./../README.md)

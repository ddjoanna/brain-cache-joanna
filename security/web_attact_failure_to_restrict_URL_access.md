# 限制 URL 存取失敗

> Failure to Restrict URL Access（限制 URL 存取失敗）是一種常見的安全漏洞，指的是應用程式未能對使用者訪問的 URL 進行適當的存取控制，導致未授權的使用者能夠直接透過修改或猜測 URL，訪問本應受限制或隱藏的敏感頁面或資料。

## 原理與危害

- 應用程式通常會透過隱藏連結或不在介面中顯示敏感頁面的 URL，來防止未授權訪問，但若伺服器端未實施嚴格的權限驗證，攻擊者可直接輸入或猜測這些 URL 進行「強制瀏覽（Forced Browsing）」。
- 這會導致攻擊者繞過正常的使用流程，直接存取管理頁面、用戶資料、備份檔案等敏感資源。
- 可能造成資料外洩、未授權操作、系統被入侵，甚至財務損失。

## 攻擊方式

- **強制瀏覽（Forced Browsing）**：攻擊者透過猜測 URL 結構或使用自動化工具，訪問未公開的頁面或檔案。
- **參數篡改**：修改 URL 中的參數，存取其他使用者或管理員的資料。
- **繞過前端控制**：前端隱藏或禁用的功能，仍可透過直接 URL 訪問。

## 防範措施

- **伺服器端嚴格權限驗證**：每個 URL 請求都必須驗證使用者身份與權限，不能僅依賴前端隱藏或不顯示連結。
- **實施基於角色的存取控制（RBAC）**：根據使用者角色授權存取權限，確保只有授權用戶能訪問敏感頁面。
- **預設拒絕原則**：未明確授權的 URL 存取請求一律拒絕。
- **避免 URL 中暴露敏感資訊**：使用不可預測的識別符或加密參數，防止簡單猜測。
- **定期安全測試與掃描**：使用自動化工具檢測未受保護的 URL 與頁面。
- **移除不必要的檔案與資源**：避免伺服器上存在不被使用但可被訪問的敏感檔案。

---

簡而言之，Failure to Restrict URL Access 是因為缺乏完善的伺服器端存取控制，導致攻擊者能直接透過 URL 訪問未授權的資源。防範的關鍵在於在伺服器端嚴格驗證每個請求的授權，並結合角色權限管理與安全開發流程，避免敏感頁面被未授權訪問。

---

**參考來源:**

[1] https://www.geeksforgeeks.org/what-is-failure-to-restrict-url-access/ \
[2] https://www.veracode.com/security/failure-restrict-url-access/ \
[3] https://susiecybersecurity.wordpress.com/2017/06/25/owasp-security-shepherd-failure-to-restrict-url-access-writes-up/ \
[4] https://cwe.mitre.org/data/definitions/817.html \
[5] https://purpleskypeter.blogspot.com/2018/04/owasp-securityshepherd-url-restrict.html \
[6] https://www.montana.edu/uit/security/web/failure-to-restrict-url-access.html \
[7] https://owasp.org/Top10/A01_2021-Broken_Access_Control/ \
[8] https://stackoverflow.com/questions/8336810/deny-direct-url-access-to-action-method

---

[返回目錄](./../README.md)

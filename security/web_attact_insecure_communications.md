# 不安全的通訊

> Insecure Communications（不安全的通訊）指的是在網路資料傳輸過程中，未採用適當的加密與安全機制，導致資料容易被攔截、竊聽或篡改的安全弱點。

## 不安全通訊的主要問題

- **明文傳輸**：使用 HTTP 等未加密協議，資料以明文形式在網路中傳送，攻擊者可輕易監聽並獲取敏感資訊（如帳號密碼、個人資料）[1][2]。
- **缺乏身份驗證**：通訊雙方無法確保對方身份，容易遭受中間人攻擊（MITM），資料被竄改或竊取。
- **混合內容問題**：HTTPS 頁面中載入 HTTP 資源，破壞整體安全性，導致瀏覽器警告[2]。
- **使用過時或弱加密協議**：如 SSL 2.0、3.0、TLS 1.0 等存在已知漏洞，容易被破解[4][5]。
- **錯誤的憑證配置**：憑證過期、域名不匹配或非受信任憑證會導致連線不安全警告[2][3]。

## 影響

- 敏感資料被攔截，造成個資外洩、帳號被盜用。
- 網站信任度降低，影響用戶體驗與業務收益[2]。
- 容易成為中間人攻擊目標，導致資料完整性與機密性受損。

## 解決方案

- **全面採用 HTTPS**：使用 TLS 協議加密通訊，確保資料傳輸安全[1][2][5]。
- **正確配置 SSL/TLS 憑證**：使用受信任 CA 頒發的憑證，定期更新與檢查憑證有效性[2][3]。
- **避免混合內容**：確保所有資源均透過 HTTPS 載入，防止安全警告與漏洞[2]。
- **使用最新版 TLS 協議**：TLS 1.2 及以上版本，避免使用已知有漏洞的舊版本[4][5]。
- **實施嚴格的憑證驗證與安全標頭**：如 HSTS（HTTP 嚴格傳輸安全）強制瀏覽器使用 HTTPS 連線。
- **加密通訊軟體選擇**：優先使用支援端對端加密且預設啟用的通訊工具，保障訊息隱私[7]。

---

總結來說，Insecure Communications 是因未使用或錯誤使用加密技術，導致資料在傳輸過程中暴露風險。透過部署 TLS/HTTPS、正確管理憑證及避免混合內容等措施，能有效保障網路通訊的機密性與完整性。

---

**參考來源:**

[1] https://www.cloudflare.com/zh-tw/learning/ssl/why-is-http-not-secure/ \
[2] https://www.new-path.com.hk/post/%E4%BD%A0%E8%88%87%E9%80%99%E5%80%8B%E7%B6%B2%E7%AB%99%E9%80%A3%E7%B7%9A%E4%B8%8D%E5%AE%89%E5%85%A8%EF%BC%9A%E5%8E%9F%E5%9B%A0%E8%88%87%E8%A7%A3%E6%B1%BA%E6%96%B9%E6%A1%88%E5%85%A8%E9%9D%A2%E5%89%96%E6%9E%90 \
[3] https://www.jddt.tw/share_why_browser_marks_not_secure.php \
[4] https://blog.csdn.net/maiya_yayaya/article/details/131322417 \
[5] https://zh.wikipedia.org/zh-hant/%E5%82%B3%E8%BC%B8%E5%B1%A4%E5%AE%89%E5%85%A8%E6%80%A7%E5%8D%94%E5%AE%9A \
[6] https://www.tntb.gov.tw/_document/files/download/7/cses05-105.08.pdf \
[7] https://infosecu.technews.tw/2021/01/14/common-communication-software/ \
[8] https://aws.amazon.com/tw/compare/the-difference-between-ssl-and-tls/

---

[返回目錄](./../README.md)

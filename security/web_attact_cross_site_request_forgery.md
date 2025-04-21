# 跨站請求偽造(CSRF)

> 跨站請求偽造（Cross Site Request Forgery，CSRF）是一種網路攻擊，攻擊者誘使已在某網站登入的使用者，在不知情的情況下執行未經授權的操作。CSRF 利用網站對使用者瀏覽器的信任，通過使用者的身份驗證（如 Cookie）發送惡意請求，從而達成攻擊目的[1][2][4][7]。

## CSRF 的運作原理

- 使用者登入網站並取得有效身份驗證（如 Cookie）。
- 攻擊者製作一個惡意請求（例如轉帳、修改密碼），並將此請求隱藏在釣魚郵件、惡意網站或圖片標籤中。
- 使用者在瀏覽器中訪問攻擊者控制的內容時，瀏覽器會自動帶上該網站的身份驗證資訊（Cookie）發送請求。
- 目標網站誤以為是使用者本人發出的合法請求，執行該操作[4][5][7]。

例如，使用者在網銀登入狀態下點擊攻擊者發送的連結，瀏覽器會帶上登入 Cookie，導致銀行執行未授權的轉帳請求[4]。

## CSRF 的攻擊條件

- 攻擊目標網站依賴 Cookie 或其他自動帶入的認證機制驗證使用者身份。
- 惡意請求的參數可被攻擊者預測或構造。
- 使用者在攻擊發生時處於已認證狀態[4]。

## 防範措施

- **Anti-CSRF 令牌（CSRF Token）**：伺服器為每個使用者會話產生不可預測的唯一令牌，並要求在敏感請求中提交該令牌，伺服器驗證令牌有效性以確保請求是合法的[4][5]。
- **SameSite Cookie 屬性**：設定 Cookie 的 SameSite 屬性為 Strict 或 Lax，限制跨站請求時 Cookie 不被自動帶上，減少 CSRF 風險[4][5]。
- **檢查 HTTP Referer 或 Origin 標頭**：驗證請求來源是否為可信任的域名。
- **使用自定義請求標頭**：例如 AJAX 請求中加入自定義標頭，伺服器拒絕沒有該標頭的請求。
- **要求用戶進行額外驗證**：對敏感操作增加 CAPTCHA、二次密碼驗證或重新登入等機制。
- **選擇具備內建 CSRF 防護的框架**，並正確配置[4][5][7]。

## 無效或不足的防護方式

- 僅依賴 HTTPS、只接受 POST 請求、URL 重寫或隱藏參數等措施無法有效防止 CSRF[4]。

---

總結來說，CSRF 是利用使用者已認證身份，在不知情下強迫瀏覽器發送惡意請求的攻擊。防範關鍵在於驗證請求的合法性，常用方法是採用 Anti-CSRF 令牌和 SameSite Cookie 設定，結合多重驗證機制，才能有效降低風險[1][4][5][7]。

---

**參考來源:**

[1] https://owasp.org/www-community/attacks/csrf \
[2] https://en.wikipedia.org/wiki/Cross-site_request_forgery \
[3] https://tech-blog.cymetrics.io/posts/jo/zerobased-cross-site-request-forgery/ \
[4] https://www.freecodecamp.org/chinese/news/what-is-cross-site-request-forgery/ \
[5] https://developer.mozilla.org/zh-TW/docs/Glossary/CSRF \
[6] https://cindyliu923.com/2022/11/20/CSRF/ \
[7] https://www.blackduck.com/glossary/what-is-csrf.html \
[8] https://www.okta.com/identity-101/csrf-attack/

---

[返回目錄](./../README.md)

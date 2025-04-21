# 身份驗證和會話管理漏洞

> Broken Authentication and Session Management 是指應用程式在身份驗證（Authentication）及會話管理（Session Management）機制上的漏洞，攻擊者可藉此冒充合法使用者，取得未授權的存取權限，導致資料外洩、帳號被盜用等嚴重安全問題[1][3][6]。

## 主要問題點

### 1. 身份驗證弱點（Credential Management）

- **弱密碼或預設密碼**：使用者設定易猜測密碼（如 123456、password），攻擊者可透過字典攻擊或憑證填充（Credential Stuffing）輕易入侵。
- **密碼儲存不安全**：未使用強加密或雜湊演算法（如 SHA1、MD5），導致密碼易被破解。
- **密碼重置機制不安全**：未妥善驗證使用者身份即允許重置密碼，攻擊者可藉此劫持帳號。
- **缺乏多因素驗證（MFA）**：單一密碼驗證易被突破，缺少額外驗證層增加風險[5][6]。

### 2. 會話管理弱點（Session Management）

- **會話 ID 管理不當**：會話 ID（Session ID）過於簡單、可預測，或未加密傳輸，易遭截取或偽造。
- **會話固定攻擊（Session Fixation）**：攻擊者強迫使用者使用特定會話 ID，登入後可利用該 ID 冒充使用者。
- **會話未及時失效**：使用者登出後會話仍有效，攻擊者持有舊會話 ID 可繼續存取。
- **Cookie 設定不安全**：未設定 HttpOnly、Secure、SameSite 等屬性，導致 Cookie 被竊取或跨站攻擊。
- **URL 重寫傳遞會話 ID**：會話 ID 暴露在 URL 中，易被截取或分享[4][6][7]。

## 攻擊手法

- **憑證填充攻擊（Credential Stuffing）**：利用大量已洩漏的帳密組合自動嘗試登入。
- **會話劫持（Session Hijacking）**：截取有效會話 ID，冒充使用者。
- **會話固定（Session Fixation）**：強制使用者使用攻擊者指定的會話 ID。
- **暴力破解（Brute Force）**：嘗試大量密碼組合登入。

## 防範措施

| 防範項目          | 建議做法                                                                    |
| ----------------- | --------------------------------------------------------------------------- |
| 強化密碼策略      | 強制使用複雜密碼，限制嘗試次數，實施帳號鎖定機制。                          |
| 密碼安全儲存      | 使用強雜湊算法（如 bcrypt、Argon2）儲存密碼，加入鹽值。                     |
| 多因素驗證（MFA） | 增加第二層驗證（如 OTP、硬體憑證）提高安全性。                              |
| 安全的會話管理    | 產生不可預測的會話 ID，使用安全 Cookie 屬性（HttpOnly、Secure、SameSite）。 |
| 會話失效機制      | 使用者登出或長時間閒置自動失效會話。                                        |
| 防止會話固定      | 登入時重新產生新的會話 ID，避免使用 URL 傳遞會話 ID。                       |
| 密碼重置安全      | 實施嚴格身份驗證流程，避免未授權的密碼重置。                                |
| 監控與警示        | 監控異常登入行為，及時警示與封鎖可疑帳號。                                  |

---

總結來說，Broken Authentication and Session Management 涉及身份驗證與會話控制的多種弱點，攻擊者可藉此冒充使用者或竊取帳號。透過強密碼政策、多因素驗證、安全會話管理及嚴格的密碼重置流程，能有效降低此類風險[1][3][6][7]。

---

**參考來源:**

[1] https://auth0.com/blog/what-is-broken-authentication/ \
[2] https://www.authgear.com/post/broken-authentication-what-is-it-and-how-to-prevent-it \
[3] https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication \
[4] https://www.geeksforgeeks.org/broken-authentication-vulnerability/ \
[5] https://stratixsystems.com/what-is-broken-authentication-and-why-does-it-matter/ \
[6] https://www.loginradius.com/blog/identity/what-is-broken-authentication/ \
[7] https://www.sitelock.com/blog/owasp-top-10-broken-authentication-session-management/ \
[8] https://portswigger.net/web-security/authentication

---

[返回目錄](./../README.md)

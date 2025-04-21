# 跨站腳本攻擊

> 跨站腳本攻擊（Cross-Site Scripting，簡稱 XSS）是一種常見的網頁安全漏洞，攻擊者利用網站對使用者輸入或資料處理不當的弱點，將惡意的腳本程式碼（通常是 JavaScript）注入到網頁中，當其他使用者瀏覽該網頁時，這些惡意腳本會在其瀏覽器端執行[1][3][6]。

## XSS 的運作原理

- 攻擊者發現網站未對使用者輸入進行充分過濾或轉義，將惡意腳本注入網站的輸入欄位、URL 參數或留言板等位置。
- 當其他使用者瀏覽包含惡意腳本的頁面時，瀏覽器會執行這些腳本。
- 惡意腳本可竊取使用者的 Cookie、會話令牌、敏感資料，甚至修改網頁內容或偽造使用者操作，達成身份冒充、資料竊取、網頁篡改、散播惡意軟體等目的[2][5][6]。

## XSS 的主要類型

1. **存儲型 XSS（Stored XSS）**：惡意腳本被永久儲存在網站的資料庫、留言板、評論區等，所有訪問該內容的使用者都會執行。
2. **反射型 XSS（Reflected XSS）**：惡意腳本作為請求參數被即時反射到回應頁面，通常透過誘騙使用者點擊特製連結觸發。
3. **DOM 型 XSS（DOM-based XSS）**：攻擊者透過修改網頁的 DOM 結構，在瀏覽器端注入並執行惡意腳本，不涉及伺服器回應[7]。

## XSS 可能造成的危害

- 竊取使用者認證資訊（如 Cookie、Token），冒充使用者身份。
- 偽造或修改網頁內容，誘導使用者誤操作或釣魚。
- 執行任意 JavaScript，散播惡意軟體或進行其他攻擊行為。
- 破壞網站正常功能與使用者體驗[5][6]。

## 防範 XSS 的常見措施

- **輸入驗證與過濾**：對所有使用者輸入進行嚴格檢查，使用白名單過濾非法字元。
- **輸出轉義**：在將資料輸出到 HTML、JavaScript、CSS 等上下文時，對特殊字元進行適當轉義，避免被當作程式碼執行。
- **內容安全策略（CSP）**：設定 CSP HTTP 標頭，限制可執行的腳本來源，降低惡意腳本執行風險。
- **HTTP Only Cookie**：將敏感 Cookie 設定為 HttpOnly，防止 JavaScript 存取。
- **使用安全框架與函式庫**：採用已內建防 XSS 機制的框架或函式庫。
- **安全響應標頭**：配置如 X-XSS-Protection 等瀏覽器安全標頭[7][5][8]。

---

總結來說，XSS 是一種在使用者端執行惡意腳本的攻擊，利用網站對使用者輸入處理不當的漏洞，攻擊者可竊取資料、篡改頁面或進行其他惡意行為。防範重點在於嚴格輸入驗證、輸出轉義及採用內容安全策略等多層防護措施。

---

**參考來源:**

[1] https://www.baohwatrust.com/technical-article/8723 \
[2] https://www.gss.com.tw/images/stories/epaper_GSS_security/pdf/epaper_gss_security_0067.pdf \
[3] https://www.cloudflare.com/zh-tw/learning/security/threats/cross-site-scripting/ \
[4] https://blog.csdn.net/m0_62480631/article/details/136760896 \
[5] https://www.fortinet.com/tw/resources/cyberglossary/cross-site-scripting \
[6] https://info.support.huawei.com/info-finder/encyclopedia/zh/%E8%B7%A8%E7%AB%99%E8%84%9A%E6%9C%AC%E6%94%BB%E5%87%BB.html \
[7] https://blog.csdn.net/usernameID007/article/details/131882729 \
[8] https://developer.mozilla.org/zh-CN/docs/Glossary/Cross-site_scripting

---

[返回目錄](./../README.md)

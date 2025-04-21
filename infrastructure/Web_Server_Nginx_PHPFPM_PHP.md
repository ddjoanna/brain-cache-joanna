# PHP Web 應用實現併發

> 以下分別說明 Nginx、PHP-FPM、PHP 的角色和實現方式，並附上兩者的比較表格。

## Nginx、PHP-FPM、PHP 的角色簡述

### Nginx

- 是一款高效能的 Web 伺服器，主要負責處理靜態資源請求（如 HTML、圖片、CSS、JS 等），並將動態請求（如 PHP 檔案）轉發給後端的 PHP 解析器。
- Nginx 本身不具備解析 PHP 的能力，它只做反向代理和負載分擔的角色[2][5]。

### PHP-FPM（PHP FastCGI Process Manager）

- 是 PHP 的 FastCGI 實作，負責管理 PHP 的執行進程，包括一個 master 進程和多個 worker 進程。
- PHP-FPM 接收 Nginx 透過 FastCGI 協議轉發的請求，執行 PHP 腳本，並將結果返回給 Nginx[2][3][5]。

### PHP

- 是伺服器端的腳本語言，負責執行具體的業務邏輯和動態內容生成。
- PHP-FPM 的 worker 進程內嵌 PHP 解譯器，實際執行 PHP 代碼[2][3]。

---

## Nginx、PHP-FPM、PHP 角色、用途與 PHP 併發關係表格整理

| 元件    | 角色與用途                                                    | 與 PHP 併發的關係                                           |
| ------- | ------------------------------------------------------------- | ----------------------------------------------------------- |
| Nginx   | 靜態資源服務器、反向代理、負載均衡器，將 PHP 請求轉給 PHP-FPM | 處理大量連線請求，負責快速分發請求，對 PHP 併發起到調度作用 |
| PHP-FPM | PHP FastCGI 進程管理器，管理 PHP 執行進程，處理 PHP 請求      | 支持多 worker 進程並行處理 PHP 請求，提高 PHP 併發能力      |
| PHP     | PHP 語言解譯器，執行動態腳本並生成動態內容                    | 由 PHP-FPM 管理的 worker 進程執行，PHP 本身不直接管理併發   |

---

## 為什麼需要 PHP-FPM 而不是直接透過 Nginx 轉 PHP

- Nginx 本身不具備解析 PHP 的能力，它是一個高效的 HTTP 伺服器和反向代理，專注於處理 HTTP 請求和靜態資源，無法直接執行 PHP 腳本[2][5]。

- PHP-FPM 作為 FastCGI 進程管理器，能夠管理多個 PHP 執行進程（worker），實現 PHP 腳本的高效執行和併發處理。FastCGI 協議允許 PHP-FPM 持續運行，避免每次請求都 fork 新進程，提升性能[2][3][5]。

- PHP-FPM 提供了進程管理、平滑重啟、錯誤日誌等功能，是專門為 PHP 動態內容設計的守護進程，這是 Nginx 無法替代的[2][5]。

---

## 為什麼不用 Apache

- Apache 內建 PHP 模組（mod_php）可以直接解析 PHP，但 Apache 在高併發和靜態資源處理上性能不及 Nginx，且資源消耗較大[4]。

- Nginx 設計為事件驅動架構，能高效處理大量連線，適合靜態內容服務和反向代理，與 PHP-FPM 結合後，能實現更優秀的動態內容處理性能[2][4]。

- Apache 的多進程/多線程模型在高併發時容易造成資源浪費，而 Nginx+PHP-FPM 的分離架構更靈活，易於擴展和維護[2][4]。

---

## 結論

- Nginx 負責高效的 HTTP 請求處理和靜態資源服務，PHP-FPM 負責 PHP 腳本的執行和進程管理，兩者配合能實現高效且可擴展的 PHP Web 應用架構。
- Apache 雖然能直接解析 PHP，但在現代高併發環境下不及 Nginx+PHP-FPM 組合的性能和靈活性[2][4][5]。

---

**參考來源:**

[1] https://blog.csdn.net/zhangbin1988/article/details/136651802 \
[2] https://blog.csdn.net/magic_world_wow/article/details/103902952 \
[3] https://cloud.tencent.com/developer/news/678417 \
[4] https://hcldirgit.github.io/2017/10/13/Nginx/5.%20mod_php%E5%92%8Cmod_fastcgi%E5%92%8Cphp-fpm%E7%9A%84%E4%BB%8B%E7%BB%8D,%E5%AF%B9%E6%AF%94,%E5%92%8C%E6%80%A7%E8%83%BD%E6%95%B0%E6%8D%AE/ \
[5] https://server.51cto.com/article/562257.html \
[6] https://www.cnblogs.com/tinywan/p/10550424.html \
[7] https://www.artacode.com/post/web/nginx-fpm/ \
[8] https://www.ernestchiang.com/zh/posts/2021/benchmark-nginx-php-fpm-between-buster-alpine/

---

[返回目錄](./../README.md)

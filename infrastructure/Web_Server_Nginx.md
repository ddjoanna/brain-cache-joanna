# Nginx

> Nginx 是一款高效能、開源的網路伺服器軟體，最初由俄羅斯工程師伊戈爾·賽索耶夫（Igor Sysoev）於 2004 年開發。Nginx 設計目標是處理高並發、高流量的網路服務，並以其事件驅動架構實現低資源消耗與高性能，廣泛應用於全球眾多大型網站與服務中[1][3]。

## Nginx 是什麼？

- **網頁伺服器**：Nginx 能夠處理 HTTP 請求，回應靜態或動態網頁內容，包括 HTML、圖片、CSS、JavaScript 等[1]。
- **反向代理伺服器**：作為用戶端與後端伺服器之間的中介，Nginx 接收請求並轉發給內部伺服器，提升效能並增加系統彈性[1][2]。
- **負載均衡器**：Nginx 能將請求分配至多台後端伺服器，實現負載分散，提高可用性與處理能力[2][3]。
- **郵件代理伺服器**：支持 SMTP、POP3、IMAP 等郵件協議代理[1]。
- **其他功能**：包括 SSL 加速、緩存服務、WebSocket 支持及訪問控制等[3]。

## Nginx 主要用途

| 用途               | 說明                                                                             |
| ------------------ | -------------------------------------------------------------------------------- |
| **靜態文件服務**   | 高效處理大量靜態資源請求，如圖片、影片、CSS、JavaScript，減輕後端伺服器負擔[3]。 |
| **反向代理**       | 將外部請求代理轉發至內部多台伺服器，隱藏內部結構並提升安全性與性能[1][2]。       |
| **負載均衡**       | 支援多種策略（輪詢、權重、IP 哈希等），均衡分配流量，確保系統穩定運作[2][3]。    |
| **緩存服務**       | 快取靜態或動態內容，降低後端伺服器壓力，加速響應速度[3]。                        |
| **SSL 加速**       | 支援 HTTPS，並可透過硬體加速或優化配置提升加密連線效能[3]。                      |
| **WebSocket 支持** | 支援雙向即時通信，適用於即時聊天、遊戲等應用[3]。                                |
| **訪問控制與安全** | 可設定 IP 白名單、黑名單、限制連線數等安全策略[3]。                              |
| **正向代理**       | 作為用戶端代理，幫助用戶訪問外部網路資源[2]。                                    |
| **動靜分離**       | 靜態資源由 Nginx 直接提供，動態請求轉發給後端應用伺服器，提高效率[2]。           |

## Nginx 與 Apache 的差異

- **架構**：Nginx 採用事件驅動非阻塞架構，能高效處理大量並發連線；Apache 則基於多進程或多線程模型，並發性能相對較弱[1]。
- **模組與擴展性**：Apache 模組可動態加載，靈活度高；Nginx 模組需在編譯時加入，較不靈活[1]。
- **配置管理**：Apache 支持.htaccess 分目錄配置，適合共享主機；Nginx 無此功能，但配置簡潔且集中管理[1]。
- **PHP 支援**：Apache 可直接透過 mod_php 處理 PHP；Nginx 需搭配 FastCGI（如 php-fpm）[1]。

## 簡單入門示例（Ubuntu）

```bash
sudo apt update
sudo apt install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

安裝後，透過瀏覽器訪問伺服器 IP，若出現 Nginx 歡迎頁面即表示安裝成功。主要配置檔位於 `/etc/nginx/`，網站設定檔通常在 `/etc/nginx/sites-available/`，啟用後會連結至 `/etc/nginx/sites-enabled/`。

修改配置後，使用以下指令重新載入設定：

```bash
sudo systemctl reload nginx
```

---

### 總結

Nginx 是一款功能強大且高效的網路伺服器軟體，適用於靜態文件服務、反向代理、負載均衡、緩存、SSL 加速及即時通信等多種場景。其事件驅動架構使其在高並發環境下表現優異，是現代網站和應用架構中不可或缺的基礎設施之一[1][2][3]。

---

**參考來源:**

[1] https://tw.alphacamp.co/blog/nginx
[2] https://www.cnblogs.com/wonchaofan/p/18284917
[3] https://cloud.baidu.com/article/3327869
[4] https://kucw.io/blog/nginx/
[5] https://blog.csdn.net/guting18893110463/article/details/136540734
[6] https://juejin.cn/post/7217340231753580601
[7] https://www.explainthis.io/zh-hant/swe/why-nginx
[8] https://zh.wikipedia.org/zh-hant/Nginx
[9] https://baike.baidu.com/item/nginx/3817705
[10] https://www.cnblogs.com/gucb/p/11990979.html
[11] https://blog.csdn.net/k417699481/article/details/115672191
[12] https://cloud.tencent.com/developer/article/2126436
[13] https://cloud.baidu.com/article/2916001
[14] https://cloud.tencent.com/developer/article/1943958
[15] https://www.cnblogs.com/97z4moon/p/15123572.html
[16] https://www.f5.com.cn/glossary/nginx
[17] https://www.thebyte.com.cn/api-gateway/nginx-conf.html

---

[返回目錄](./../README.md)

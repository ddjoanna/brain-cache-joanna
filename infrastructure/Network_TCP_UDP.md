# TCP vs UDP

> TCP（傳輸控制協定）與 UDP（使用者資料報協定）都是網路傳輸層的協議，但設計目標與特性不同：

## TCP（Transmission Control Protocol）

- **面向連接**：在傳送資料前，TCP 需先透過三次握手建立連線，確保雙方準備好通訊。
- **可靠傳輸**：TCP 會檢查資料包是否遺失、損壞或亂序，並透過重傳機制確保資料完整且依序到達。
- **流量與擁塞控制**：TCP 會控制資料傳送速率，避免接收端負荷過重或網路擁塞。
- **資料傳輸方式**：以字節流方式傳送資料，接收端依序組合還原。
- **頭部較大**：TCP 封包頭部約 20 字節，包含序號、確認號等控制資訊。
- **適用場景**：適合對資料完整性要求高的應用，如網頁瀏覽（HTTP/HTTPS）、電子郵件、檔案傳輸（FTP）、遠端連線（SSH）等。

## UDP（User Datagram Protocol）

- **無連接**：UDP 傳送資料前不建立連線，直接將資料包（資料報）發送出去。
- **不保證可靠性**：不檢查資料包是否送達或順序，資料可能遺失、重複或亂序。
- **無流量與擁塞控制**：資料包以最快速度發送，不會調節傳輸速率。
- **資料傳輸方式**：以獨立資料包形式傳送，每個資料包獨立處理。
- **頭部較小**：UDP 封包頭部約 8 字節，結構簡單。
- **適用場景**：適合對速度和效率要求高、可容忍少量資料遺失的應用，如線上遊戲、語音通話（VoIP）、影音串流、DNS 查詢、VPN 隧道等。

## TCP 與 UDP 比較表

| 特性           | TCP                    | UDP                  |
| -------------- | ---------------------- | -------------------- |
| 連線性         | 面向連接               | 無連接               |
| 傳輸可靠性     | 高，保證資料完整且有序 | 低，不保證資料送達   |
| 流量與擁塞控制 | 有                     | 無                   |
| 傳輸速度       | 較慢                   | 較快                 |
| 頭部大小       | 約 20 字節             | 約 8 字節            |
| 傳輸方式       | 字節流                 | 獨立資料包           |
| 適用場景       | 電子郵件、網頁、FTP 等 | 即時通訊、影音串流等 |

---

總結來說，TCP 適合需要高可靠性和完整性的應用，而 UDP 則適合對速度和效率要求較高且能容忍部分資料遺失的場景[1][2][4][6]。

---

**參考來源:**

[1] https://www.explainthis.io/zh-hant/swe/tcp-udp \
[2] https://www.purevpn.com.tw/blog/tcp-yu-udp-shenme-qubie/ \
[3] https://nordvpn.com/zh/blog/tcp-udp-xieyi-bijiao/ \
[4] https://ithelp.ithome.com.tw/articles/10294859 \
[5] https://lightningxvpn.com/blog/tw/tcp-vs-udp-tw/ \
[6] https://jaminzhang.github.io/network/The-Difference-Between-TCP-And-UDP-Protocol/ \
[7] https://www.yasssssblog.com/2020/10/04/ithome-30-21-tcp-udp/ \
[8] https://www.purevpn.com/zh/blog/tcp-yu-udp-de-qubie/

---

[返回目錄](./../README.md)

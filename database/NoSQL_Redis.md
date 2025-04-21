# Redis

## 基本介紹

Redis 是一個開源的高性能記憶體鍵值（key-value）資料庫，支援多種資料結構，主要用於快取、計數器、排行榜、消息隊列等場景。Redis 採用單線程事件循環架構，將資料存放於記憶體中，讀寫速度極快，並提供持久化機制保證資料安全。

---

## 資料結構與常見使用情境

| 資料結構              | 說明                           | 常見使用情境                                       |
| --------------------- | ------------------------------ | -------------------------------------------------- |
| **String**            | 動態字串，最大可達 512MB       | 快取普通資料、計數器（如網站瀏覽量）、Session 管理 |
| **List**              | 雙向鏈表，支援快速插入刪除     | 消息隊列、堆疊、留言板、排行榜                     |
| **Set**               | 無序不重複元素集合             | 抽獎、標籤系統、好友關係                           |
| **Sorted Set (ZSet)** | 有序集合，元素帶分數排序       | 排行榜、計分系統、事件流、加權推薦                 |
| **Hash**              | 鍵值對集合，適合存儲物件屬性   | 用戶資料、商品屬性等結構化資料                     |
| **GEO**               | 地理位置資料結構，支援座標查詢 | 附近地點查詢、位置服務、地理推薦                   |

---

## 持久化機制

- **RDB（快照）**  
  以快照方式定時將記憶體資料寫入磁碟，恢復速度快，但可能丟失最近變更。Redis 啟動時會載入 RDB 文件恢復資料[2][5][7]。

- **AOF（追加式日誌）**  
  將每條寫命令追加到日誌檔案，重啟時依序執行命令恢復資料，資料更完整但文件較大。為避免文件過大，Redis 支援 AOF 重寫（Rewrite）機制，透過異步 fork 子進程重寫文件，壓縮冗餘命令[3][6][8]。

---

## 高可用架構

- **主從複製（Master-Slave）**  
  主節點負責寫入，從節點負責讀取，提升讀取效能與容錯能力。

- **Redis Sentinel**  
  監控 Redis 節點狀態，自動故障轉移，確保高可用性。

- **Redis Cluster**  
  原生分片機制，實現資料分散存放與水平擴展，支援故障轉移與多主多從架構。

---

## 記憶體淘汰機制（Eviction Policy）

當 Redis 記憶體使用達到 `maxmemory` 限制時，根據設定的淘汰策略清理資料：

| 策略名稱            | 行為說明                           | 適用場景               |
| ------------------- | ---------------------------------- | ---------------------- |
| **noeviction**      | 不淘汰，記憶體滿時寫入操作報錯     | 嚴格保證資料不丟失     |
| **allkeys-lru**     | 淘汰所有 key 中最近最少使用（LRU） | 快取場景，保留熱點資料 |
| **volatile-lru**    | 只淘汰設置過期時間 key 中 LRU      | 部分快取資料設定過期   |
| **allkeys-random**  | 隨機淘汰所有 key                   | 對淘汰要求不嚴格       |
| **volatile-random** | 隨機淘汰設置過期時間 key           | 部分快取資料設定過期   |
| **volatile-ttl**    | 淘汰過期時間最短的 key             | 時間敏感型快取         |

---

**參考來源:**

[1] https://blog.csdn.net/m0_59336430/article/details/126794436 \
[2] https://www.cnblogs.com/linguoguo/p/5430468.html \
[3] https://blog.csdn.net/vmaps/article/details/136485938 \
[4] https://www.rockylinux.cn/notes/redis-basics-08-detailed-explanation-of-configuration.html \
[5] https://zhenye-na.github.io/blog/2019/08/29/redis-cheatsheet.html \
[6] https://redis.com.cn/topics/persistence.html \
[7] https://www.cnblogs.com/traditional/p/13296648.html \
[8] https://help.aliyun.com/zh/redis/user-guide/backup-and-restoration-solutions/

---

[返回目錄](./../README.md)

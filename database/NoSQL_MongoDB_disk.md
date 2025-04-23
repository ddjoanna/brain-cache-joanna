# MongoDB 存儲空間

> MongoDB 的存儲空間在刪除文件（document）後，並不會立即釋放磁盤空間。這是因為 MongoDB 將被刪除的資料空間標記為可重用，而非直接回收釋放，因此磁盤空間的使用量通常不會隨著刪除操作而減少[1][4][6]。

## 造成影響

- **磁盤空間持續被佔用**：即使刪除了大量文件，資料庫佔用的磁盤空間大小不變，可能導致磁盤空間不足，影響系統穩定性和性能[4][7]。
- **無法立即回收空間**：這會造成磁盤空間的浪費，特別是在資料頻繁刪除的場景下，磁盤容量壓力較大[1][4]。

## 解決方案

- **使用 `db.repairDatabase()` 命令**：這是官方推薦的回收磁盤空間的方式，會重新整理資料庫文件，釋放未使用的磁盤空間。但此操作需要額外的磁盤空間（當前資料大小加 2GB），且執行時會有性能影響，且若磁盤空間不足則無法完成[3][4]。
- **使用 dump & restore 方法**：先用 `mongodump` 備份資料，刪除資料庫後再用 `mongorestore` 恢復，這種方法可以在磁盤空間不足時使用，且在副本集環境中可實現不停機回收空間[3]。
- **使用 `compact` 命令**：可回收集合中的空閒空間，但在 MongoDB 4.4 之前版本會阻塞操作，需謹慎使用[5]。
- **刪除整個集合或資料庫**：執行 `dropCollection` 或 `dropDatabase` 可立即釋放對應的磁盤空間，適用於整體刪除場景[1][5]。
- **監控與清理不必要的索引和資料**：刪除廢棄索引和集合也能釋放空間[5]。

## TTL（Time To Live）索引

TTL 是 MongoDB 提供的一種自動過期機制，允許設定特定欄位的文件在指定時間後自動刪除。

- **自動化資料清理**：避免手動刪除過期資料，減少管理負擔。
- **控制資料量**：防止資料無限制增長，降低磁盤壓力。
- **提升系統效能**：定期刪除過期資料，有助於維持資料庫性能和磁盤空間的合理使用。
- **配合空間回收策略**：TTL 刪除資料後，配合上述回收空間方法，能有效管理磁盤空間[2]。

## 總論

MongoDB 刪除文件不會立即釋放磁盤空間，需透過資料庫修復、dump & restore 或刪除整個集合等方式回收。TTL 是自動管理過期資料的關鍵工具，有助於控制資料庫大小與性能維護[1][3][5]。

---

**參考來源:**

[1] https://cloud.tencent.com/developer/article/2292237 \
[2] https://blog.csdn.net/xue317378914/article/details/138160768 \
[3] https://www.cnblogs.com/xibuhaohao/p/14333740.html \
[4] https://blog.csdn.net/mooncarp/article/details/82895636 \
[5] https://help.aliyun.com/zh/mongodb/support/release-the-disk-space-of-an-apsaradb-for-mongodb-instance \
[6] https://docs-pd.nocoly.com/zh-Hans/optimize/mongodb/clean/reclaim-disk-space/ \
[7] https://xie.infoq.cn/article/d8cb871a7733646996f60641a \
[8] https://little-star.love/posts/4c0873be/

---

[返回目錄](./../README.md)

# ClickHouse

> ClickHouse 是一款開源的列式分析型資料庫，專為高效處理大規模數據分析查詢而設計，廣泛應用於即時分析和 OLAP 場景。

## 核心架構

- 採用**列式存儲**，將同一列數據連續存放，優化了磁碟 IO 和 CPU 快取效率，特別適合讀取大量數據的分析查詢。
- 利用**向量化處理**，充分發揮 CPU 多核和 SIMD 指令集的性能，提升查詢速度。
- 支援分布式架構，可橫向擴展以處理海量數據。

## 主要特點

- **高效性能**：單伺服器每秒可處理數十億行數據，查詢延遲低至毫秒級，且能利用多核 CPU 並行計算[1][2][6]。
- **數據壓縮**：強大的壓縮算法大幅減少存儲空間和 IO 負擔，提高查詢效率[1][3]。
- **快速寫入**：支援高速批量寫入，寫入速度可達 50-200MB/s，適合大量數據更新場景[1][3]。
- **靈活索引**：使用非 B 樹索引結構，無需最左前綴原則，且全表掃描速度快，減少索引限制[1]。
- **SQL 支持**：支持大部分 SQL 語法，包含 Join，但 Join 性能較弱且語法特殊[1]。
- **分布式表支持**：可構建分布式表，但性能和物理表相比略有不足[1]。

## 優點

- 高吞吐量和低延遲，適合海量數據的即時分析。
- 高效利用 CPU 和 IO 資源，查詢速度快。
- 良好的數據壓縮能力，節省存儲空間。
- 支援簡單的 SQL 查詢語法，易於使用。

## 缺點

- **不支持事務**，無法進行 ACID 事務操作，不支持真正的刪除和更新，只能透過批量覆蓋[1][3]。
- 不適合高並發查詢，官方建議 QPS 不超過 100，單查詢會佔用大量 CPU 資源[1]。
- Join 性能較差，需特別優化查詢邏輯和數據結構。
- 寫入需批量操作，避免小批量或逐行插入，否則會影響查詢性能[1]。
- 分布式部署和維護較複雜，需注意分區設計和資源管理。

## 適用場景

- 大數據即時分析和報表系統。
- OLAP（聯機分析處理）應用，如用戶行為分析、廣告點擊分析、監控數據聚合。
- 需要高速讀取和批量寫入的數據倉庫。
- 不適合需要強事務支持和高並發寫入的 OLTP 場景。

---

## 列式分析型資料庫 vs 關聯式資料庫 vs 非關聯式資料庫

列式分析型資料庫與關聯式及非關聯式資料庫的主要差異如下：

| 項目             | 列式分析型資料庫（如 ClickHouse）                             | 關聯式資料庫（RDBMS，如 MySQL、PostgreSQL）                  | 非關聯式資料庫（NoSQL，如 MongoDB、Cassandra）                   |
| ---------------- | ------------------------------------------------------------- | ------------------------------------------------------------ | ---------------------------------------------------------------- |
| **資料存儲方式** | 採用**列式存儲**，同一欄位的數據連續存放，優化分析查詢效率    | 採用**行式存儲**，資料以列為單位存放，適合事務處理和頻繁更新 | 多樣化存儲模型（鍵值、文件、圖形、欄族等），針對不同資料類型優化 |
| **主要用途**     | 針對 OLAP（線上分析處理），適合大規模數據的批量讀取與聚合分析 | 針對 OLTP（線上交易處理），適合複雜事務和關聯查詢            | 適合半結構化或非結構化資料和高擴展性需求的應用                   |
| **查詢性能**     | 聚合和掃描大量資料時效率極高，適合複雜分析查詢                | 支援複雜 JOIN 和事務，適合多表關聯查詢                       | 查詢靈活但 JOIN 支持有限或不支持，強調水平擴展和高可用           |
| **寫入性能**     | 高吞吐量批量寫入，適合大量數據匯入，但不適合頻繁小量更新      | 支援 ACID 事務，適合頻繁寫入和更新                           | 高寫入吞吐，適合分布式環境，但一致性通常較弱                     |
| **事務支持**     | 不支持 ACID 事務，無法保證強一致性，主要用於分析場景          | 完整 ACID 事務支持，確保資料一致性                           | 多數採用最終一致性模型，部分 NoSQL 支援有限 ACID                 |
| **擴展性**       | 水平擴展較複雜，通常透過分片和分布式架構實現                  | 傳統上以垂直擴展為主，水平擴展需額外策略                     | 天生支持水平擴展，適合大規模分布式部署                           |
| **資料結構**     | 結構化資料，專注於欄位分析                                    | 嚴格結構化資料，表格間有明確關聯                             | 支援結構化、半結構化與非結構化資料                               |

### 補充說明

- **關聯式資料庫**以表格形式存放資料，強調資料完整性和一致性，適合結構化且關聯性強的資料，並支援複雜查詢與事務處理[9][12]。
- **非關聯式資料庫**提供彈性資料模型，適合多樣化和不斷變化的資料結構，強調高可用性和擴展性，通常採用最終一致性模型[9][12][14]。
- **列式分析型資料庫**則專注於分析型查詢，透過列式存儲和向量化計算，極大提升大數據聚合和掃描效率，適合 OLAP 和報表場景[13]（推論自欄族資料庫特性及分析型資料庫設計）。

---

## 結論

ClickHouse 是一款針對大規模數據分析設計的高性能列式資料庫，擅長高速查詢和批量寫入，但不支持複雜事務和高並發場景，適合用於數據分析和報表等 OLAP 應用。

---

**參考來源:**

[1] https://www.cnblogs.com/jelly12345/p/17028696.html \
[2] https://blog.csdn.net/lovewebeye/article/details/102739939 \
[3] https://blog.csdn.net/u013250861/article/details/134236660 \
[4] https://www.cnblogs.com/love-DanDan/p/18409431 \
[5] https://architect.pub/what-clickhouse-how-does-it-compare-postgresql-and-timescaledb-and-how-does-it-perform-time-series \
[6] https://cloud.baidu.com/article/2946538 \
[7] https://www.ifb.me/blog/backend/clickhouse-starrocks \
[8] https://www.modb.pro/db/579839 \
[9] https://aws.amazon.com/tw/compare/the-difference-between-relational-and-non-relational-databases/ \
[10] https://hackmd.io/@yy933/BJvQBPUf2 \
[11] https://www.codegym.tech/blog/sql-vs-nosql \
[12] https://aws.amazon.com/tw/nosql/ \
[13] https://prisma.dev.org.tw/dataguide/intro/comparing-database-types \
[14] https://learn.microsoft.com/zh-tw/azure/architecture/data-guide/big-data/non-relational-data \
[15] https://www.purestorage.com/tw/knowledge/big-data/structured-vs-unstructured-data.html \
[16] https://www.freecodecamp.org/chinese/news/relational-vs-nonrelational-databases-difference-between-sql-db-and-nosql-db/

---

[返回目錄](./../README.md)

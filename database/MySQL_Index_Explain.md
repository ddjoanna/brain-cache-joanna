# MySQL 索引與 EXPLAIN 整理說明

## MySQL 索引

### 索引定義與作用

- 索引是幫助 MySQL 高效查找資料的數據結構，類似書本目錄，能快速定位資料，避免全表掃描，提升查詢效率。
- 索引會佔用額外空間，並增加寫入時的維護成本。

### 索引類型

| 類型         | 說明                                                      | 特點與應用                                         |
| ------------ | --------------------------------------------------------- | -------------------------------------------------- |
| **主鍵索引** | 唯一標識表中每行，不能為 NULL，一張表只能有一個主鍵索引。 | InnoDB 聚簇索引，數據與索引存放同一結構中。        |
| **唯一索引** | 保證索引列唯一，但允許一個 NULL 值。                      | 用於數據唯一性約束，加速唯一值查詢。               |
| **普通索引** | 最基本的索引類型，無唯一性限制。                          | 主要用於加速查詢。                                 |
| **複合索引** | 基於多列組合建立，遵循左前綴原則。                        | 適合多條件查詢。                                   |
| **全文索引** | 用於文本類型的全文搜索。                                  | 適合模糊查詢、關鍵字搜索，MySQL 5.6+ InnoDB 支持。 |
| **空間索引** | 用於地理空間數據類型。                                    | 支持空間範圍查詢。                                 |

### 索引底層結構

- **B+樹索引**：MySQL 默認索引結構，InnoDB 和 MyISAM 均使用 B+樹，但 InnoDB 為聚簇索引，MyISAM 為非聚簇索引。
- **哈希索引**：基於哈希表，查找速度快，但不支持範圍查詢，主要用於 Memory 引擎。
- **R 樹索引**：用於空間數據類型索引。
- **全文索引**：基於倒排索引實現全文搜索。

### 聚簇索引與非聚簇索引

| 類型           | 說明                                                |
| -------------- | --------------------------------------------------- |
| **聚簇索引**   | InnoDB 主鍵索引，數據和索引存放在一起，查詢效率高。 |
| **非聚簇索引** | 二級索引，葉子節點存主鍵值，查詢需回表，效率較低。  |

### 索引優化原則

- 遵守左前綴原則使用複合索引。
- 選擇高基數列建立索引。
- 避免過多索引影響寫入性能。
- 利用覆蓋索引避免回表。
- 避免對索引列使用函數或隱式類型轉換。

### 索引建立示例

```sql
CREATE INDEX idx_name ON table_name(column_name);
CREATE UNIQUE INDEX idx_unique ON table_name(column_name);
CREATE INDEX idx_multi ON table_name(column1, column2);
CREATE FULLTEXT INDEX idx_fulltext ON table_name(text_column);
```

---

## MySQL EXPLAIN

### 作用

- 查看 MySQL 查詢執行計劃，分析查詢是否使用索引、是否全表掃描、連接順序等，協助優化 SQL。

### 使用方法

```sql
EXPLAIN SELECT * FROM table_name WHERE condition;
```

### 常見欄位說明

| 欄位              | 說明                                                                                    |
| ----------------- | --------------------------------------------------------------------------------------- |
| **id**            | 查詢中每個 SELECT 的識別號，決定執行順序。                                              |
| **select_type**   | 查詢類型，如 SIMPLE、PRIMARY、SUBQUERY 等。                                             |
| **table**         | 查詢涉及的資料表名稱。                                                                  |
| **type**          | 連接類型，效率由好到差：system、const、eq_ref、ref、range、index、ALL。                 |
| **possible_keys** | 可能使用的索引。                                                                        |
| **key**           | 實際使用的索引。                                                                        |
| **key_len**       | 使用的索引長度。                                                                        |
| **ref**           | 哪個欄位或常數與索引列比對。                                                            |
| **rows**          | 預估掃描的資料列數。                                                                    |
| **Extra**         | 額外訊息，如 Using index（覆蓋索引）、Using where（過濾條件）、Using filesort（排序）。 |

### EXPLAIN 作用

- 判斷是否使用索引（key 是否為 NULL）。
- 判斷是否全表掃描（type 為 ALL）。
- 判斷是否回表（Extra 是否有 Using index）。
- 分析多表連接順序與方式。

---

**參考來源:**

[1] https://www.cnblogs.com/yrxing/p/14557150.html \
[2] https://www.cnblogs.com/jojop/p/13951979.html \
[3] https://tech.meituan.com/2014/06/30/mysql-index.html \
[4] https://juejin.cn/post/6931901822231642125 \
[5] https://blog.csdn.net/qq_62636650/article/details/137158976 \
[6] https://javaguide.cn/database/mysql/mysql-index.html \
[7] https://blog.csdn.net/wj1314250/article/details/118462541 \
[8] https://cn.pingcap.com/article/post/3328.html

---

[返回目錄](./../README.md)

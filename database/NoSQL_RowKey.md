# RowKey

> RowKey 是 HBase 中用來唯一標識一行資料的鍵，類似於關聯式資料庫中的主鍵。它是由使用者自行指定的一串不重複字串，且在 HBase 中資料是依 RowKey 的字典序（ASCII 碼順序）全局排序存放，因此 RowKey 的設計直接影響資料的存取效率與系統性能[1][2][4][8]。

## 特點

- **唯一性**：RowKey 必須唯一標識每一行資料。
- **字串形式**：RowKey 可以是任意字串，內部以 byte array 形式儲存。
- **字典序排序**：資料依 RowKey 的字典序排序存放，影響資料分布與讀取效率。
- **用戶指定**：RowKey 完全由使用者設計與指定，不由系統自動生成。
- **影響 Region 分布**：資料依 RowKey 分散到不同 Region，設計不當可能造成熱點問題[1][2][6][8]。

## 核心原則

- **唯一性原則**：RowKey 必須能唯一識別一行資料，避免重複。
- **查詢優化原則**：根據最高頻的查詢場景設計 RowKey，將常一起查詢的資料儘量放在相鄰位置。
- **避免熱點原則**：避免大量資料集中在少數 Region，透過加鹽（salt）、前綴散列等方式分散負載。
- **長度與結構原則**：RowKey 長度宜短且固定，通常建議不超過 16-100 bytes，結構設計要便於範圍掃描與快速定位。
- **時間戳反轉原則**：若需查詢最新資料，建議時間戳取反（如 Long.Max_Value - timestamp）放在 RowKey 中，方便掃描最新記錄[1][2][3][7].

## 優缺點

| 方面   | 優點                                 | 缺點                                   |
| ------ | ------------------------------------ | -------------------------------------- |
| 唯一性 | 確保每筆資料唯一，方便快速定位資料行 | 設計不當可能導致重複或查詢效率低       |
| 排序性 | 依字典序排序，方便範圍掃描與排序查詢 | 排序導致資料集中，易產生 Region 熱點   |
| 靈活性 | 使用者可自定義結構，符合業務需求     | 設計複雜，需考慮查詢場景與負載均衡     |
| 性能   | 合理設計可提升讀寫效率               | 不合理設計會造成性能瓶頸及資料分布不均 |

## 典型應用場景

- **交易類資料查詢**：如 sellerId + timestamp + orderId，方便按賣家及時間範圍查詢交易紀錄。
- **金融風控**：使用 prefix + uid/idcard/tele 等設計，結合散列前綴避免熱點。
- **車聯網資料**：carId + timestamp，或加散列前綴分散負載。
- **最新資料查詢**：uid + Long.Max_Value - timestamp，方便掃描最新操作記錄。
- **全表掃描與範圍查詢**：依 RowKey 設計範圍掃描起止點，提升查詢效率[1][5].

## 結論

RowKey 是 HBase 中最關鍵的設計元素，直接影響資料分布、查詢效率與系統性能。設計時需根據業務查詢需求，結合唯一性、排序性、負載均衡等原則，避免熱點問題，才能發揮 HBase 的高效能與擴展性。

---

**參考來源:**

[1] https://lihuimintu.github.io/2019/08/07/HBase-Rowkey/ \
[2] https://blog.csdn.net/fl63zv9zou86950w/article/details/106066082 \
[3] https://www.cnblogs.com/sx66/p/14239778.html \
[4] https://xie.infoq.cn/article/3f8918d3ef064b7b6b2382e1b \
[5] https://developer.aliyun.com/article/685888 \
[6] https://www.cnblogs.com/zjdxr-up/p/17155135.html \
[7] https://blog.csdn.net/baidu_38225647/article/details/122295214 \
[8] https://docs.jdcloud.com/cn/column-oriented-storage/rowkeydesign

---

[返回目錄](./../README.md)

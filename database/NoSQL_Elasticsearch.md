# ElasticSearch

> ElasticSearch（簡稱 ES）是一個基於 Apache Lucene 的開源分散式搜尋和分析引擎，主要用於全文搜尋、日誌分析、業務分析和安全智慧等場景。它以 JSON 格式儲存文件，並使用倒排索引技術實現高效的全文檢索[3][4][6]。

## ElasticSearch 特性

- **分散式架構**：可水平擴展，支援數百個節點，處理 PB 級資料，具備高可用性和容錯能力[4][6]。
- **RESTful API**：通過 HTTP 提供簡單易用的 API，支援多種程式語言（Java、Python、PHP、JavaScript 等）[3][6]。
- **近乎即時**：資料索引後幾乎可立即搜尋，適合即時監控和異常偵測[3][6]。
- **全文搜尋能力**：支援分詞、相似度匹配、模糊查詢、地理空間查詢等多種查詢方式[6]。
- **聚合分析**：內建強大的聚合框架，可進行複雜的統計和分組分析[6]。
- **生態系統豐富**：與 Kibana（視覺化工具）、Logstash（資料收集與轉換）、Beats（輕量資料傳送器）整合，形成 Elastic Stack[3][6]。

## ElasticSearch 優點

- 高效能，能快速處理大量資料搜尋和分析。
- 易於擴展和管理，支援分散式叢集。
- 強大的全文搜尋和分析功能。
- 開放原始碼，社群活躍。
- 豐富的生態系統和工具支援。

## ElasticSearch 缺點

- 配置和管理較為複雜，需要一定技術門檻。
- 大規模叢集可能面臨資源消耗和調優挑戰。
- 2021 年後授權改變，部分版本不再完全開放原始碼[3]。

## ElasticSearch 應用場景

- 網站和應用程式的全文搜尋。
- 日誌和指標資料的儲存與分析。
- 安全事件監控和異常偵測。
- 電子商務和企業內部資料搜尋。
- 地理資訊系統（GIS）和生物資訊分析等專業領域[3][5]。

---

## OpenSearch 與 ElasticSearch 差異

### 背景

2021 年 Elastic 公司改變 ElasticSearch 的授權策略，不再使用 Apache 2.0 授權，改為 Elastic 授權和 SSPL，限制了原始碼的開放性[3]。為了維持完全開放原始碼的搜尋和分析引擎，Amazon 與社群推出了 OpenSearch 專案，作為 ElasticSearch 和 Kibana 的 Apache 2.0 授權分支[3]。

### OpenSearch 特性

- 基於 ElasticSearch 7.10 版本的分支，保持 Apache 2.0 授權，完全開放原始碼。
- 社群驅動，Amazon 主導開發，持續新增功能和安全修補。
- 保持與 ElasticSearch API 的高度相容性，方便用戶遷移。
- 包含 OpenSearch Dashboards，類似 Kibana 的視覺化工具。
- 強調開放性與社群參與，避免授權限制帶來的風險[3]。

### ElasticSearch 與 OpenSearch 比較

| 方面       | ElasticSearch                        | OpenSearch                                |
| ---------- | ------------------------------------ | ----------------------------------------- |
| 授權       | Elastic 授權 / SSPL（非完全開放）    | Apache 2.0（完全開放原始碼）              |
| 版本基礎   | 持續更新，最新功能多                 | 基於 ElasticSearch 7.10，社群持續維護     |
| 社群與支援 | Elastic 公司主導，商業支援強         | 社群驅動，Amazon 支持，開放參與           |
| 生態系統   | Elastic Stack（Kibana、Logstash 等） | OpenSearch Stack（OpenSearch Dashboards） |
| 適用場景   | 企業級搜尋與分析，商業產品           | 開放原始碼使用者，重視授權自由與社群貢獻  |

### OpenSearch 優缺點

- **優點**：完全開放原始碼，無授權限制，社群活躍，與 ElasticSearch 高度相容。
- **缺點**：新功能開發速度可能較 ElasticSearch 慢，生態系統較 ElasticStack 小。

---

## 總結

ElasticSearch 是功能強大且成熟的分散式搜尋與分析引擎，適用於多種資料搜尋與分析場景，尤其在企業級應用中廣泛使用。OpenSearch 是 ElasticSearch 的開放原始碼分支，提供相似功能且保持 Apache 2.0 授權，適合重視開放性及授權自由的用戶。選擇時可依據授權需求、生態系統偏好及技術支援考量決定。

---

**參考來源:**

[1] https://www.cnblogs.com/buchizicai/p/17093719.html \
[2] https://ithelp.ithome.com.tw/m/articles/10314564 \
[3] https://aws.amazon.com/tw/what-is/elasticsearch/ \
[4] https://www.cnblogs.com/tanghaorong/p/16271893.html \
[5] https://www.omniwaresoft.com.tw/product-news/elastic-news/elasticsearch-in-10minutes/ \
[6] https://houbb.github.io/2018/11/15/elasticsearch-01-overview-01 \
[7] https://www.elastic.co/cn/elasticsearch \
[8] https://www.elastic.co/cn/blog/a-practical-introduction-to-elasticsearch

---

[返回目錄](./../README.md)

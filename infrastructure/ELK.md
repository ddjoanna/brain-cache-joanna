# ELK

> ELK 是一套由三個主要開源工具組成的資料處理與分析平台，分別是 Elasticsearch、Logstash 和 Kibana，合稱 ELK Stack（也稱 Elastic Stack，加入了 Beats 作為第四個組件）。這套工具組合廣泛用於集中式日誌管理、資料搜尋、分析與視覺化。

## ELK 三大組件說明

- **Elasticsearch**  
  是一個分散式、基於 JSON 的搜尋與分析引擎，建構於 Apache Lucene 之上。它能快速索引大量資料，支援複雜查詢與即時分析，適合用於日誌分析、全文檢索、監控等場景。

- **Logstash**  
  是一個強大的資料收集與處理管線工具，能從多種來源（如伺服器日誌、應用程式、資料庫等）收集資料，並進行過濾、轉換與格式化，最後將資料輸送到 Elasticsearch 或其他目的地。

- **Kibana**  
  是一個資料視覺化與探索介面，與 Elasticsearch 緊密整合，提供使用者建立圖表、儀表板和報告的能力，方便分析與監控資料。

- **Beats**（擴充組件）  
  輕量級資料收集代理，安裝於資料來源端，負責將資料傳送至 Logstash 或 Elasticsearch，常見的有 Filebeat（檔案日誌）、Metricbeat（系統指標）等。

## ELK 工作流程

1. **資料收集**：Beats 或 Logstash 從各種資料來源收集原始資料。
2. **資料處理**：Logstash 對資料進行解析、過濾、轉換，提升資料品質與結構化。
3. **資料儲存與索引**：Elasticsearch 將處理後的資料索引並儲存，支援快速搜尋與分析。
4. **資料視覺化**：Kibana 提供豐富的圖表與儀表板，讓使用者直觀地觀察資料趨勢與異常。

## ELK 的應用場景

- 集中式日誌管理與分析
- IT 基礎架構與應用監控
- 安全事件與威脅偵測（SIEM）
- 業務與使用者行為分析
- 網站與系統性能監控

## ELK 的優勢

- 開源且社群活躍，持續更新與擴充
- 支援海量資料的即時搜尋與分析
- 強大的資料處理與轉換能力
- 直觀且可自訂的視覺化介面
- 可擴展性強，適用於各種規模的系統

---

總結來說，ELK Stack 是一套功能完整的資料收集、處理、搜尋與視覺化平台，幫助企業集中管理與分析海量資料，提升故障排除效率與業務洞察力。

---

**參考來源:**

[1] https://www.elastic.co/elastic-stack \
[2] https://aws.amazon.com/what-is/elk-stack/ \
[3] https://logz.io/learn/complete-guide-elk-stack/ \
[4] https://www.secoda.co/glossary/what-is-the-elk-stack-elasticsearch-logstash-kibana \
[5] https://intellipaat.com/blog/what-is-elk-stack/ \
[6] https://www.youtube.com/watch?v=-WhK4eHQTM0 \
[7] https://www.elastic.co/logstash \
[8] https://www.elastic.co/elastic-stack/features

---

[返回目錄](./../README.md)

# Data pipeline

> Data pipeline（資料管線）是一套將資料從來源系統移動到目標系統的系統方法，強調資料流程化、自動化與管理。它允許從多種異質資料來源抽取資料，經過轉換與整合，最終載入至資料倉儲、資料湖泊或分析工具中，以支援後續的資料分析與應用[1][5]。

## Data pipeline 的主要組成部分

- **起點(Origin)**：資料來源，如交易系統、物聯網感測器、社群媒體等。
- **終點(Destination)**：資料最終存放或使用的地方，如資料倉儲、資料湖泊、視覺化工具。
- **資料流(Dataflow)**：資料在起點與終點間的流動過程，通常包含 ETL（抽取 Extract、轉換 Transform、載入 Load）步驟。
- **存儲(Storage)**：資料在不同階段的暫存或永久保存位置，依據資料量、頻率與查詢需求決定。
- **處理(Processing)**：實現資料轉換、複製、串流等操作的過程。
- **工作流(Workflow)**：定義資料處理任務的執行順序與依賴關係。
- **監控(Monitoring)**：監控資料管線運作狀況與效能，確保正常運行。
- **技術(Technology)**：支撐資料管線的工具與平台[1]。

## 常見資料管線工具、處理方式與使用情境表格

| 工具類型           | 代表工具/平台                                                | 處理方式            | 使用情境說明                                                 |
| ------------------ | ------------------------------------------------------------ | ------------------- | ------------------------------------------------------------ |
| 批次處理工具       | Apache Hadoop、Apache Spark                                  | 批次處理(Batch)     | 定期大量資料移動與處理，如市場資料整合、報表生成。           |
| 即時串流處理工具   | Apache Kafka、Apache Flink                                   | 即時處理(Real-time) | 需要即時資料分析的場景，如金融交易監控、物聯網資料即時分析。 |
| 雲原生資料管線工具 | AWS Data Pipeline、Azure Data Factory、Google Cloud Dataflow | 批次與即時混合      | 雲端資料整合與處理，支援彈性擴展與多來源資料管理。           |
| ETL 專用工具       | Talend、Informatica                                          | ETL                 | 資料抽取、轉換與載入，適合資料倉儲建置與資料清理。           |
| 工作流管理工具     | Apache Airflow、Luigi                                        | 工作流調度與管理    | 管理複雜資料任務依賴，確保資料處理流程順序與穩定性。         |

## 使用情境舉例

- **資料工程師**：設計與維護資料管線基礎架構，確保資料流暢與正確。
- **資料科學家/分析師**：依賴資料管線提供清洗後、格式化的資料進行分析與模型訓練。
- **商業決策者**：透過資料管線支援的分析結果做出策略或運營決策。
- **市場行銷**：利用整合的客戶資料進行精準行銷與效果追蹤[1][5]。

總結來說，資料管線是數據驅動時代關鍵的資料處理與整合工具，涵蓋資料抽取、轉換、載入與監控等多個環節，並依據不同需求選擇合適的工具與架構來實現高效的資料流通與應用[1][5]。

---

**參考來源:**

[1] https://hackmd.io/@Willie-The-Lord/Sym6lMv0O \
[2] https://ithelp.ithome.com.tw/m/articles/10352832 \
[3] https://www.sap.com/taiwan/products/data-cloud/master-data-governance/what-is-data-governance.html \
[4] https://aws.amazon.com/tw/what-is/data-governance/ \
[5] https://guzhi.knkconsulting.co/product/data-pipeline/ \
[6] https://learn.microsoft.com/zh-tw/fabric/data-factory/pipeline-runs \
[7] https://docs.aws.amazon.com/zh_tw/datapipeline/latest/DeveloperGuide/dp-writing-pipeline-definition.html \
[8] https://www.accupass.com/event/2406140531586003949200

---

[返回目錄](./../README.md)

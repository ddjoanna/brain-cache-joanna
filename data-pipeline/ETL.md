# ETL

> ETL 是 Extract（擷取）、Transform（轉換）、Load（載入）的縮寫，是一個將來自多個不同來源的資料整合到大型中央儲存庫（如資料倉儲）中的過程[1][2][3]。

## ETL 三大步驟說明：

- **擷取（Extract）**  
  從多個資料來源系統中抽取資料，這些來源可能是不同的資料庫、應用系統或檔案，資料格式和結構可能不一致[2][5]。

- **轉換（Transform）**  
  對擷取的資料進行清洗、格式轉換、資料整併、缺失值處理等作業，確保資料一致性與品質，並符合目標系統的需求[2][5][6]。

- **載入（Load）**  
  將轉換後的資料載入到目標資料庫、資料倉儲或資料湖中，供後續分析和報告使用[1][5]。

## ETL 的應用場景範例

例如零售業公司有多個店面，各自有獨立的銷售系統和資料庫。公司希望整合所有店面數據進行銷售趨勢與庫存分析。透過 ETL，先從各店面擷取資料，接著轉換成統一格式並清理錯誤，最後載入至資料倉儲供分析使用[5]。

## ETL 對企業的價值

- 整合多源資料，確保資料一致性與品質。
- 簡化繁瑣資料處理流程，加速資料分析速度。
- 支援商業智慧與決策分析，提升企業洞察力與競爭力[5][8]。

## 雲端 ETL 工具舉例（以 AWS 為例）

- **AWS Glue**：一站式托管 ETL 服務，協助資料擷取、轉換與載入。
- **Amazon S3**：用於儲存 ETL 過程中的資料，具高可靠性。
- **Amazon Redshift**：快速可擴展的資料倉儲，方便分析。
- **AWS Data Pipeline**：排程與自動化 ETL 工作流程[5]。

---

總結來說，ETL 是企業資料整合與分析的關鍵流程，透過擷取、轉換和載入，將分散且格式不一的資料整合成可用的資訊，支持企業做出更準確的決策。

---

**參考來源:**

[1] https://aws.amazon.com/tw/what-is/etl/ \
[2] https://www.fanruan.com/zh-tw/blog/what-is-ETL \
[3] https://www.purestorage.com/tw/knowledge/what-is-etl.html \
[4] https://aws.amazon.com/tw/compare/the-difference-between-etl-and-elt/ \
[5] https://www.nextlink.cloud/news/what-is-etl/ \
[6] https://marketing.ares.com.tw/newsletter/2023-12-knowbe4/etl \
[7] https://www.oracle.com/tw/integration/what-is-etl/ \
[8] https://mile.cloud/zh/resources/blog/understand-data-pipeline-automation-etl-data-analytics_610

---

[返回目錄](./../README.md)

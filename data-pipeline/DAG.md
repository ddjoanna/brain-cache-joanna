# DAG 有向無環圖

> DAG（Directed Acyclic Graph，有向無環圖）是一種用於描述任務或資料流程的圖形結構，其特點是圖中邊有方向且不會形成環路。這使得 DAG 非常適合用來表示有先後順序且無循環依賴的工作流程或資料處理過程。

## DAG 的說明

- **結構特性**：DAG 由節點（nodes）和有向邊（edges）組成，節點代表任務或資料狀態，有向邊表示任務之間的依賴關係，且不會形成循環，確保流程有明確的開始和結束點[6]。
- **工作流管理**：在工作流系統如 Apache Airflow 中，DAG 用來定義任務的執行順序與依賴，確保任務按預定邏輯執行，且能設定時間排程和錯誤重試等[1][3][4]。
- **資料模型關聯**：在資料工程和資料轉換中，DAG 幫助理解資料模型間的上下游依賴關係，清晰展現資料流向和血緣，有助於追蹤資料影響範圍及改動風險[2]。

## DAG 的應用情境

- **資料工程與 ETL 流程**：利用 DAG 管理資料抽取、轉換、加載（ETL）任務，確保資料處理步驟依序完成，並能視覺化展示資料流向與依賴[1][2]。
- **工作流排程與管理**：在 Airflow 等系統中，DAG 用於定義複雜任務流程，支持任務依賴設定、並行執行、錯誤處理及重試機制，適合自動化運維和資料管道管理[1][3][4]。
- **大規模並行計算**：如 Argo Workflows 中，DAG 用於編排 Fan-out/Fan-in 任務，將大任務拆分成多個子任務並行處理，再彙總結果，提升計算效率和資源利用率[5]。
- **資料血緣分析與影響評估**：透過 DAG 快速識別資料模型間的依賴關係，評估某個資料模型變更對下游模型的影響，降低資料錯誤風險[2]。

總結來說，DAG 是一個強大且靈活的工具，廣泛應用於資料工程、工作流管理及大規模計算任務中，幫助用戶清晰定義和管理複雜的流程依賴與執行順序[1][2][5][6]。

---

**參考來源:**

[1] https://cloud.google.com/composer/docs/how-to/using/writing-dags \
[2] https://www.getdbt.com/blog/dag-use-cases-and-best-practices \
[3] https://hackmd.io/@Arsheng/B18JG06fK \
[4] https://cloud.google.com/composer/docs/composer-3/write-dags \
[5] https://www.alibabacloud.com/help/tc/doc-detail/2861761.html \
[6] https://hazelcast.com/foundations/distributed-computing/directed-acyclic-graph/ \
[7] https://intercom.help/bricks-dag-inc/zh-TW/articles/5910552-%E7%AF%84%E4%BE%8B-%E8%87%AA%E5%8B%95%E5%8C%96%E6%9F%A5%E9%A9%97%E6%A8%A1%E7%B5%84%E4%BD%BF%E7%94%A8%E6%95%99%E5%AD%B8 \
[8] https://aws.amazon.com/cn/blogs/china/amazon-mwaa-hands-on-sharing-cross-dag-task-scheduling/

---

[返回目錄](./../README.md)

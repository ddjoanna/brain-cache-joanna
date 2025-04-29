# 專案目的

學習筆記

## 目錄

### security （安全）

- [加密技術](security/Encryption.md)
- [雜湊函式](security/Encryption_Hash.md)
- [身份驗證與會話管理漏洞](security/web_attact_broken_authentication_and_session_management.md)
- [跨站請求偽造（CSRF）](security/web_attact_cross_site_request_forgery.md)
- [跨站腳本攻擊（XSS）](security/web_attact_cross_site_scripting.md)
- [注入攻擊 (SQL Injection)](security/web_attact_injection_flaws.md)
- [限制 URL 存取失敗](security/web_attact_failure_to_restrict_URL_access.md)
- [資訊洩露與錯誤處理不當](security/web_attact_information_leakage_improper_error_handling.md)
- [不安全通訊](security/web_attact_insecure_communications.md)
- [不安全加密存儲](security/web_attact_insecure_cryptographic_storage.md)
- [不安全直接物件引用未授權資料洩漏](security/web_attact_insecure_direct_object_reference.md)
- [不安全遠程文件載入並執行惡意腳本](security/web_attact_insecure_remote_file_include.md)

### access-control （存取控制）

- [RBAC、ABAC、ACL 授權模型](access-control/model_RBAC_ABAC_ACL.md)
- [Casdoor 與 Casbin 權限框架](access-control/framework_Casdoor_Casbin.md)
- [OAuth 認證協議](access-control/protocol_OAuth.md)
- [JWT 身份識別詳解](access-control/identification_JWT.md)
- [Cookie、Session 與 JWT 身份識別機制](access-control/identification_Cookie_Session_JWT.md)

### system-design （系統設計）

- [分散式微服務架構](system-design/distributed_microservice_architecture.md)
- [Temporal 微服務工作流](system-design/microservice_workflow_Temporal.md)
- [系統設計概述](system-design/system_design_overview.md)
- [系統設計與架構範例](system-design/system_design_with_architecture.md)

### programming （程式設計）

- [PHP、Node.js 與 Golang 比較](programming/language_PHP_Nodejs_Golang.md)
- [PHP 語言介紹](programming/language_PHP.md)
- [Node.js 語言介紹](programming/language_Nodejs.md)
- [Golang 語言介紹](programming/language_Golang.md)
- [物件導向程式設計](programming/design_OOP.md)
- [Clean Architecture](programming/design_Clean_Architecture.md)
- [領域驅動設計](programming/design_Domain_Driven_Design.md)
- [Clean Architecture 與 DDD](programming/design_Clean_Architecture_DDD.md)
- [SOLID 原則](programming/design_OOP_SOLID.md)
- [軟體設計模式](programming/design_pattern_software.md)
- [軟體設計模式中創建型模式](programming/design_pattern_software_creational.md)
- [資料結構概述](programming/data_structure_overview.md)
- [堆疊與佇列](programming/data_structure_Stack_Queue.md)
- [訊息佇列總覽](programming/message_queue_overview.md)
- [Kafka 訊息佇列](programming/message_queue_Kafka.md)
- [併發與平行處理](programming/multi_task_Concurrency_Parallelism.md)
- [併發解決方案](programming/multi_task_Concurrency_solution.md)
- [程序、執行緒與協程](programming/multi_task_Process_Thread_Coroutine.md)
- [競態條件](programming/race_condition.md)
- [API 架構風格總覽](programming/api_architectural_styles_overview.md)
- [Laravel 重大演進與 HTTP 請求生命週期詳細說明](programming/framework_php_laravel_provider.md)
- [Laravel 事件系統詳細說明](programming/framework_php_laravel_event.md)
- [Laravel 服務提供者](programming/framework_php_laravel_provider.md)
- [Laravel 實作 API 請求流量管理](programming/framework_php_laravel_api_rate_limit.md)
- [分頁設計](programming/pagination_page_num_next_page_token.md)
- [CDS 設計模式概述](programming/design_pattern_CDC.md)
- [Debezium 概述](programming/design_pattern_CDC_Debezium.md)
- [CDC 與 MySQL 實作](programming/mysql_debezium.md)

### database （資料庫）

- [資料庫總覽](database/database_overview.md)
- [關聯式資料庫介紹](database/Relational_Database.md)
- [MySQL 索引解析](database/MySQL_Index_Explain.md)
- [MySQL 與 PostgreSQL 比較](database/MySQL_PostgreSQL.md)
- [多版本並發控制（MVCC）](database/Relational_Database_MVCC.md)
- [NoSQL 簡介](database/NoSQL.md)
- [Redis 介紹](database/NoSQL_Redis.md)
- [Redis 與 LUA 腳本](database/NoSQL_Redis_LUA.md)
- [Redis 解決方案](database/NoSQL_Redis_Solution.md)
- [MongoDB 介紹](database/NoSQL_MongoDB.md)
- [MongoDB 查詢與操作](database/NoSQL_MongoDB_query.md)
- [MongoDB 存儲空間](database/NoSQL_MongoDB_disk.md)
- [Elasticsearch 介紹](database/NoSQL_Elasticsearch.md)
- [Elasticsearch 查詢與操作](database/NoSQL_Elasticsearch_query.md)
- [Elasticsearch 分詞器](database/NoSQL_Elasticsearch_analysis.md)
- [Elasticsearch 向量語意搜尋](database/NoSQL_Elasticsearch_vector.md)
- [Elasticsearch 向量維度限制與要求](database/NoSQL_Elasticsearch_vector_dims.md)
- [ACID 特性](database/ACID.md)
- [CAP 與 BASE 理論](database/CAP_BASE.md)
- [兩階段提交與 SAGA 模式](database/2PC_SAGA.md)
- [OLAP 與 OLTP 比較](database/OLAP_OLTP.md)
- [OLAP 線上分析處理](database/OLAP.md)
- [ClickHouse](database/OLAP_ClickHouse.md)
- [ClickHouse 與 Snowflake 比較](database/OLAP_ClickHouse_Snowflake.md)
- [ClickHouse 與 Druid 比較](database/ClickHouse_Druid.md)

### infrastructure （基礎架構）

- [基礎架構即程式碼](infrastructure/Infrastructure_as_Code.md)
- [Kubernetes 介紹](infrastructure/Kubernetes.md)
- [Kubernetes 資源物件](infrastructure/Kubernetes_resource_objects.md)
- [Kubernetes 存取控制](infrastructure/Kubernetes_access_control.md)
- [Minikube](infrastructure/Kubernetes_Minikube.md)
- [Kubernetes 和 Docker Swarm 比較](infrastructure/Kubernetes_Docker_Swarm.md)
- [Helm Chart](infrastructure/Kubernetes_Helm_Chart.md)
- [Terraform 工具](infrastructure/Infrastructure_as_Code_terraform.md)
- [OpenTelemetry](infrastructure/OpenTelemertry.md)
- [Prometheus 與 Jaeger](infrastructure/OpenTelemertry_Prometheus_Jaeger.md)
- [ELK 日誌系統](infrastructure/ELK.md)
- [Docker 與 Traefik](infrastructure/Web_Server_Docker_Traefik.md)
- [Nginx 伺服器](infrastructure/Web_Server_Nginx.md)
- [Nginx 與 Apache 比較](infrastructure/Web_Server_Nginx_Apache.md)
- [Nginx 與 PHP-FPM](infrastructure/Web_Server_Nginx_PHPFPM_PHP.md)
- [OSI 模型](infrastructure/Network_OSI.md)
- [TCP 與 UDP 協議](infrastructure/Network_TCP_UDP.md)
- [虛擬私有雲（VPC）](infrastructure/Network_VPC.md)
- [服務等級協議](infrastructure/Service_Level_Agreement.md)
- [統一資源標識符](infrastructure/universal_resource_URI_URL_URN.md)

### data-pipeline （數據處理）

- [資料管線概述](data-pipeline/data_pipeline_overview.md)
- [ETL 流程介紹](data-pipeline/ETL.md)
- [Airflow 與 NiFi 工具](data-pipeline/ETL_Airflow_NiFi.md)
- [有向無環圖（DAG）概念](data-pipeline/DAG.md)

### storage （儲存）

- [儲存系統概述](storage/storage_overview.md)

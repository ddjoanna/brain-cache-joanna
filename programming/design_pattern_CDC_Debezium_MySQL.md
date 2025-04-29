# 實作 Debezium 應用於 MySQL

> 主要流程是透過 Debezium MySQL 連接器捕捉 MySQL 的 Binlog 變更事件，並將資料變更以事件流形式發送到 Kafka，再由下游系統消費這些事件。以下是詳細步驟與說明：

---

## 前置準備

- **MySQL 配置**

  - 啟用 Binlog（必須是 ROW 格式）
  - 設定唯一的 server-id

  ```ini
  [mysqld]
  server-id=184054
  log_bin=mysql-bin
  binlog_format=ROW
  binlog_row_image=FULL
  binlog_expire_logs_seconds=604800
  gtid_mode=ON
  enforce_gtid_consistency=TRUE
  ```

  - 開啟必要的權限給 Debezium 使用者（如 REPLICATION SLAVE、REPLICATION CLIENT 權限）

  ```sql
  CREATE USER IF NOT EXISTS 'debezium'@'%' IDENTIFIED BY 'dbzpassword';
  GRANT SELECT, RELOAD, SHOW DATABASES, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'debezium'@'%';
  FLUSH PRIVILEGES;
  ```

- **Kafka 環境**
  - 部署 Kafka 叢集（可用本地或雲端服務）
  - 部署 Kafka Connect（Debezium 連接器運行於此）

---

## 安裝 Debezium MySQL Connector

- 從 Debezium 官方網站下載對應版本的 `debezium-connector-mysql`
- 將連接器放置於 Kafka Connect 的插件目錄
- 重啟 Kafka Connect，使其載入連接器插件

  ```yml
  services:
    mysql:
      image: mysql:8.0
      environment:
        MYSQL_ROOT_PASSWORD: root
        MYSQL_DATABASE: ddjoanna
        MYSQL_USER: ddjoanna
        MYSQL_PASSWORD: secret
      ports:
        - "3307:3306"
      volumes:
        - mysql_data:/var/lib/mysql
        - ./.config/mysql/my.cnf:/etc/mysql/conf.d/my.cnf # 掛載自訂配置
        - ./.config/mysql/init.sql:/docker-entrypoint-initdb.d/init.sql # 掛載自訂初始化腳本
      restart: unless-stopped
      networks:
        - ddjoanna_network
    debezium:
      image: debezium/connect:3.0.0.Final
      depends_on:
        - kafka
        - mysql
      ports:
        - "8083:8083"
      environment:
        BOOTSTRAP_SERVERS: kafka:9092
        GROUP_ID: 1
        CONFIG_STORAGE_TOPIC: debezium_connect_configs
        OFFSET_STORAGE_TOPIC: debezium_connect_offsets
        STATUS_STORAGE_TOPIC: debezium_connect_statuses
        KEY_CONVERTER_SCHEMAS_ENABLE: "false"
        VALUE_CONVERTER_SCHEMAS_ENABLE: "false"
        CONNECT_PRODUCER_RETRIES: 10 # Kafka Producer 最大重試次數，避免暫時性錯誤導致資料遺失
        CONNECT_PRODUCER_RETRY_BACKOFF_MS: 1000 # 重試間隔時間（毫秒）
        CONNECT_REST_RETRY_BACKOFF_MS: 1000 # REST 請求重試間隔時間
        CONNECT_REST_RETRY_MAX_ATTEMPTS: 10 # REST 請求最大重試次數
        DEBEZIUM_CONNECT_KEEP_ALIVE_INTERVAL_MS: 40000 # Keep-alive 設定，避免網路閒置斷線導致延遲
        CONNECT_LOG4J_ROOT_LOGLEVEL: INFO # 監控與日誌等級
        TASKS_MAX: 1 # 同時執行任務數量
      restart: unless-stopped
      networks:
        - ddjoanna_network
    kafka:
      image: bitnami/kafka:3.5.1-debian-11-r75
      environment:
        KAFKA_CFG_NODE_ID: 0
        KAFKA_CFG_PROCESS_ROLES: controller,broker
        KAFKA_CFG_CONTROLLER_QUORUM_VOTERS: "0@kafka:9093"
        KAFKA_CFG_LISTENERS: PLAINTEXT://:9092,CONTROLLER://:9093,EXTERNAL://:9094
        KAFKA_CFG_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,EXTERNAL://localhost:9094
        KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP: CONTROLLER:PLAINTEXT,EXTERNAL:PLAINTEXT,PLAINTEXT:PLAINTEXT
        KAFKA_CFG_CONTROLLER_LISTENER_NAMES: CONTROLLER
        KAFKA_CFG_AUTO_CREATE_TOPICS_ENABLE: "true" # 啟用自動建立 Topic
      ports:
        - "9092:9092" # internal communication between Kafka brokers
        - "9094:9094" # external communication
        - "9997:9997"
      restart: unless-stopped
      networks:
        - ddjoanna_network
    kafka-ui:
      image: provectuslabs/kafka-ui:v0.7.2
      environment:
        KAFKA_CLUSTERS_0_NAME: local
        KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: kafka:9092
        KAFKA_CLUSTERS_0_METRICS_PORT: 9997
        # KAFKA_CLUSTERS_0_SCHEMAREGISTRY: http://schemaregistry0:8085
        KAFKA_CLUSTERS_0_KAFKACONNECT_0_NAME: first
        KAFKA_CLUSTERS_0_KAFKACONNECT_0_ADDRESS: http://kafka-connect0:8084
        DYNAMIC_CONFIG_ENABLED: "true"
      ports:
        - 8084:8080
      depends_on:
        - kafka
      restart: unless-stopped
      networks:
        - ddjoanna_network

  volumes:
    mysql_data:
      driver: local

  networks:
    ddjoanna_network:
      driver: bridge
  ```

---

## 配置 Debezium MySQL Source Connector

```bash
curl --location 'http://localhost:8083/connectors' \
--header 'Content-Type: application/json' \
--data '{
    "name": "mysql-connector",
    "config": {
        "connector.class": "io.debezium.connector.mysql.MySqlConnector",
        "database.hostname": "mysql",
        "database.port": "3306",
        "database.user": "debezium",
        "database.password": "dbzpassword",
        "database.server.id": "184054",
        "database.server.name": "ddjoanna",
        "database.include.list": "ddjoanna",
        "include.schema.changes": "true",
        "schema.history.internal.kafka.bootstrap.servers": "kafka:9092",
        "schema.history.internal.kafka.topic": "schema-changes.ddjoanna",
        "snapshot.mode": "initial",
        "database.allowPublicKeyRetrieval": "true",
        "database.useSSL": "false",
        "topic.prefix": "ddjoanna"
    }
}'
'
```

- `database.server.id`：MySQL 伺服器唯一 ID，避免多個連接器衝突
- `database.server.name`：Debezium 事件中用於標記來源的邏輯名稱
- `database.include.list` 與 `table.include.list`：指定要監控的資料庫與資料表
- `database.history.internal.kafka.topic`：存放資料庫結構變更的 Kafka 主題
- `snapshot.mode`：可選擇 `initial` / `never` / `always`，分別表示從初始化建立快照、不建立快照、永遠建立快照
- `database.allowPublicKeyRetrieval`：可選擇 `true` / `false`，分別表示允許建立公鑰檢查，不允許建立公鑰檢查
- `database.useSSL`：可選擇 `true` / `false`，分別表示啟用 SSL 連線，不啟用 SSL 連線(在本地測試或非生產環境中，沒有設定憑證檔案)

---

## 確認連接器狀態正常

- 確認連接器狀態正常，開始捕捉 MySQL 的資料變更

```bash
curl --location 'http://localhost:8083/connectors/mysql-connector/status'
```

- 取得所有連線器

```bash
curl --location 'http://localhost:8083/connectors' \
--header 'Content-Type: application/json'
```

---

## 消費變更事件

- Debezium 會將每筆資料變更（INSERT、UPDATE、DELETE）以事件形式寫入 Kafka 主題，事件包含鍵（主鍵）與值（變更前後資料）
- 下游系統（如資料倉庫、搜尋引擎、報表系統）可透過 Kafka 消費這些事件，實現資料同步與即時分析

---

## 注意事項與最佳實踐

- **MySQL Binlog 必須設定為 ROW 格式**，Debezium 才能捕捉行級變更
- **避免 server-id 衝突**，每個 Debezium 連接器需設定唯一的 `database.server.id`
- **Kafka Connect 與 Kafka 需有良好監控與資源配置**，確保資料流穩定無阻塞
- **資料庫用戶需具備足夠權限**，且密碼安全管理（可結合 AWS Secrets Manager 等工具）
- **Schema 變更管理**，Debezium 會將結構變更寫入專用 Kafka 主題，需確保此主題可用且保留策略合理
- **事件格式理解**，Debezium 事件包含 envelope 結構，需根據業務需求解析與處理
- **錯誤與重試機制**，Kafka Connect 支援自動重試與錯誤處理，需配置合適的策略

---

**參考來源:**

[1] https://www.alibabacloud.com/help/zh/apsaramq-for-kafka/cloud-message-queue-for-kafka/user-guide/use-a-debezium-mysql-source-connector-to-synchronize-mysql-database-data-to-apsaramq-for-kafka \
[2] https://docs.aws.amazon.com/zh_tw/msk/latest/developerguide/mkc-debeziumsource-connector-example.html \
[3] https://docs.redhat.com/zh-cn/documentation/red_hat_build_of_debezium/2.3.7/html/debezium_user_guide/descriptions-of-debezium-mysql-connector-data-change-events \
[4] https://www.omniwaresoft.com.tw/techcolumn/kafka-techcolumn/what-is-cdc/ \
[5] https://docs.aws.amazon.com/zh_tw/msk/latest/developerguide/msk-connect-debeziumsource-connector-example-steps.html \
[6] https://docs.redhat.com/zh-cn/documentation/red_hat_build_of_debezium/2.1.4/html/debezium_user_guide/descriptions-of-debezium-mysql-connector-data-change-events \
[7] https://www.cnblogs.com/Marydon20170307/p/17935472.html \
[8] https://ithelp.ithome.com.tw/m/articles/10271356

---

[返回目錄](./../README.md)

# OpenTelemetry 應用

> 以下分別說明 OpenTelemetry 與 Prometheus、Jaeger 的結合應用，並附上兩者的比較表格。

## Prometheus 與 OpenTelemetry 的結合

Prometheus 是一個專注於度量（Metrics）數據收集、存儲和查詢的系統，常用於監控服務健康狀態與性能。OpenTelemetry 可將應用中收集的度量數據通過 Prometheus Exporter 導出到 Prometheus，實現統一的度量數據收集和管理。

- OpenTelemetry SDK 自動或手動收集應用指標（如請求數量、延遲、錯誤率）。
- 透過 Prometheus Exporter，將這些度量數據暴露在 HTTP `/metrics` 端點，供 Prometheus 以拉取（pull）方式定期抓取。
- Prometheus 負責存儲時序數據，並提供 PromQL 查詢語言和告警功能。
- Grafana 等工具可從 Prometheus 獲取數據，進行可視化展示。

此結合方案常用於性能監控、服務健康檢查及告警管理[1][2][5][7]。

---

## Jaeger 與 OpenTelemetry 的結合

Jaeger 是一個分布式追蹤系統，專注於收集和分析跨多服務請求的追蹤數據。OpenTelemetry 生成的追蹤（Trace）數據可通過 Jaeger Exporter 發送至 Jaeger。

- OpenTelemetry SDK 在應用中生成追蹤 Span，捕捉請求在各服務間的流轉與延遲。
- 追蹤數據通過 Jaeger Exporter 推送到 Jaeger Collector。
- Jaeger 提供可視化界面，展示請求調用鏈路、Span 時間線及依賴關係。
- 運維和開發人員可利用 Jaeger 進行故障診斷和性能瓶頸分析。

此結合方案適用於微服務架構下的跨服務調用追蹤與故障排查[1][3][5][7]。

---

## Prometheus 與 Jaeger 差異比較表

| 特性                        | Prometheus                            | Jaeger                                 |
| --------------------------- | ------------------------------------- | -------------------------------------- |
| **數據類型**                | 度量（Metrics），數值型時序數據       | 追蹤（Tracing），跨服務請求調用鏈路    |
| **數據收集方式**            | 拉取（Pull）模式，定期抓取 `/metrics` | 推送（Push）模式，SDK 主動發送數據     |
| **主要功能**                | 存儲、查詢時序數據，告警與性能監控    | 分布式追蹤數據收集、可視化與故障診斷   |
| **查詢與分析工具**          | PromQL 查詢語言，Grafana 可視化       | Jaeger UI 追蹤視覺化，無專門查詢語言   |
| **告警能力**                | 內建強大告警系統                      | 無內建告警，專注追蹤數據分析           |
| **典型應用場景**            | 服務健康監控、性能指標分析、告警管理  | 跨服務調用追蹤、性能瓶頸定位、故障排查 |
| **與 OpenTelemetry 的關係** | 接收 OpenTelemetry 導出的度量數據     | 接收 OpenTelemetry 導出的追蹤數據      |

---

總結來說，OpenTelemetry 作為統一的數據收集與標準化框架，透過 Exporter 將度量數據導出給 Prometheus，將追蹤數據導出給 Jaeger，兩者協同提供完整的可觀察性解決方案，涵蓋從性能監控到跨服務調用追蹤的全方位需求[1][5]。

---

**參考來源:**

[1] https://learn.microsoft.com/zh-tw/dotnet/core/diagnostics/observability-prgrja-example \
[2] https://learn.microsoft.com/zh-cn/dotnet/core/diagnostics/observability-prgrja-example \
[3] https://www.showapi.com/news/article/67c4fd764ddd79f11a058d3c \
[4] https://blog.csdn.net/YiGeiGiaoGiao/article/details/133352561 \
[5] https://blog.csdn.net/YiGeiGiaoGiao/article/details/147140211 \
[6] https://github.com/ZYangLin/openTelemetryPratice \
[7] https://www.cnblogs.com/gaoyanbing/p/18670241 \
[8] https://www.aneasystone.com/archives/2022/11/opentelemetry-observability.html

---

[返回目錄](./../README.md)

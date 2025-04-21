# OpenTelemetry

> OpenTelemetry 是一個由 Cloud Native Computing Foundation（CNCF）托管的開源可觀察性框架和工具套件，旨在為分佈式系統提供統一的遙測數據（包括追蹤、度量和日誌）的生成、收集、處理和導出標準[1][2][6]。

## 主要組成部分

- **追蹤（Tracing）**：追蹤記錄請求在多個服務間的流轉過程，通過「span」（跨度）表示單次操作，有助於定位延遲和性能瓶頸[3][5][6]。
- **度量（Metrics）**：度量反映系統運行狀況的數據，如請求數量、錯誤率、CPU 使用率等，幫助監控服務健康和性能[3][5][11]。
- **日誌（Logs）**：日誌記錄應用運行時的事件和訊息，對故障排查和行為分析非常重要[3][5][6]。
- **上下文管理（Context Propagation）**：將追蹤、度量和日誌數據關聯起來，實現跨服務的完整分佈式觀察視圖[2][7]。

## 核心組件

- **API 和 SDK**：為多種語言（如 Java、Python、Go 等）提供標準接口和實現，方便應用程式生成和導出遙測數據[2][4][6]。
- **收集器（Collector）**：獨立代理服務，負責接收、處理和轉發遙測數據，支持多種格式和後端[2][4][6]。
- **自動插桩**：無需修改源碼即可對應用進行監控數據收集[4][6]。
- **導出器（Exporter）**：將數據發送到不同的觀察後端，如 Prometheus、Jaeger、Elastic Stack 等[2][4][6]。

## 主要應用場景

- **性能監控與優化**：通過追蹤和度量數據識別瓶頸，優化系統性能[3][6]。
- **故障診斷**：跨服務追蹤幫助快速定位錯誤根源[3][6]。
- **監控告警**：利用度量數據設置告警，及時響應異常[3]。
- **運維與可觀察性**：實現分佈式系統的全面可觀察性，提升運維效率[6][7]。
- **數據統一管理**：支持多語言、多平台，統一收集和管理遙測數據[2][4]。

## 特色與優勢

- **開源且供應商中立**：不綁定特定後端，支持多種觀察平台和商業解決方案[1][2][9]。
- **跨語言和跨平台支持**：涵蓋主流語言和技術棧[2][6]。
- **高度可擴展**：支持定制接收器、導出器、儀表化庫和上下文傳播格式[2]。
- **融合歷史項目優勢**：由 OpenTracing 和 OpenCensus 合併而成，整合了兩者的優點[2][6]。

總結來說，OpenTelemetry 是一個強大的、標準化的開源可觀察性解決方案，幫助開發和運維團隊在複雜分佈式系統中實現高效的性能監控、故障診斷和運維管理，提升系統穩定性和用戶體驗[1][2][6][9]。

---

**參考來源:**

[1] https://opentelemetry.io/zh/docs/what-is-opentelemetry/
[2] https://opentelemetry.opendocs.io/docs/what-is-opentelemetry/
[3] https://greptime.cn/blogs/2024-09-05-opentelemetry
[4] https://www.elastic.co/cn/what-is/opentelemetry
[5] https://www.cnblogs.com/hacker-linner/p/17613281.html
[6] https://blog.csdn.net/qq_14829643/article/details/134764903
[7] https://observability.cn/project/opentelemetry/mxwclg35nkqmi2pq/
[8] https://www.cnblogs.com/ulricqin/p/18587833
[9] https://www.splunk.com/zh_tw/solutions/opentelemetry.html
[10] https://xuqilong.top/pages/13f6ab/
[11] https://www.emqx.com/zh/blog/open-telemetry-the-basics-and-benefits-for-mqtt-and-iot-observability

---

[返回目錄](./../README.md)

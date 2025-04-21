# Helm Charts

> Helm 是 Kubernetes 的套件管理工具，類似 Linux 系統中的 apt 或 yum，用於簡化 Kubernetes 應用的部署、管理與升級。它將 Kubernetes 應用封裝成稱為 **Chart** 的軟體包，方便用戶快速安裝和管理複雜的 Kubernetes 資源。

---

## Helm Chart 是什麼？

- **Chart** 是 Helm 中應用的打包格式，一個 Chart 是一組描述 Kubernetes 資源的檔案集合，通常包含多個 YAML 模板與配置檔案，並打包成 tar 格式的軟體包。
- Chart 內主要包含：
  - `Chart.yaml`：描述 Chart 的基本資訊，如名稱、版本、描述等。
  - `values.yaml`：預設配置值，用戶可透過此檔案自訂部署參數。
  - `templates/` 目錄：存放 Kubernetes 資源的模板文件，透過模板引擎渲染生成最終的 YAML。
  - 其他輔助文件，如 README、schema 等。

---

## Helm 的工作原理

1. **Chart 創建與打包**  
   開發者編寫 Chart，定義 Kubernetes 應用的所有資源與配置，並打包成 Chart 軟體包。

2. **Chart 發布與儲存**  
   Chart 可以發布到 Helm Repository（類似軟體倉庫），方便用戶下載和管理。

3. **安裝與部署**  
   用戶使用 `helm install` 命令，Helm 會從倉庫下載 Chart，根據用戶提供的配置（覆蓋 `values.yaml` 預設值），渲染模板生成 Kubernetes 資源清單，並提交給 Kubernetes API 伺服器，完成應用部署。

4. **管理與升級**  
   Helm 支援應用的升級（`helm upgrade`）、回滾（`helm rollback`）、刪除（`helm uninstall`）等生命週期管理操作。

---

## Helm 的作用與優勢

- **簡化 Kubernetes 應用部署**  
  用戶無需手動編寫大量 YAML 文件，只需一條命令即可快速部署複雜應用。

- **配置靈活**  
  透過 `values.yaml` 和命令行參數，輕鬆調整部署參數，支持多環境配置。

- **版本管理**  
  Chart 支援版本控制，方便應用版本的升級與回滾。

- **依賴管理**  
  Chart 可定義依賴其他 Chart，實現複雜應用的組合部署。

- **社群與生態豐富**  
  有大量官方和第三方 Chart 倉庫，涵蓋各種常見應用。

---

## 總結

- Helm Chart 是 Kubernetes 應用的包管理格式，將多個 Kubernetes 資源描述文件封裝成一個可重用、可分享的套件。
- Helm 作為 Kubernetes 的包管理器，通過 Chart 實現應用的快速部署、版本控制和生命週期管理，大幅提升 Kubernetes 應用的易用性和維護效率。

---

**參考來源:**

[1] https://www.redhat.com/zh/topics/devops/what-is-helm \
[2] https://www.cnblogs.com/peng-zone/p/11821498.html \
[3] https://blog.csdn.net/fegus/article/details/127315041 \
[4] https://www.thebyte.com.cn/container/Helm.html \
[5] https://yifan-online.com/zh/km/article/detail/7605 \
[6] https://www.cnblogs.com/szx666/p/14662630.html \
[7] https://www.thebyte.com.cn/application-centric/Helm.html \
[8] https://blog.ivansli.com/2024/07/07/240707-helm/

---

[返回目錄](./../README.md)

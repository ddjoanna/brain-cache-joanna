# Kubernetes 中常見的資源物件及其功能

> 以下依據 Kubernetes 主要資源類型及其用途，整理成幾個分類表格，方便理解 Kubernetes 中常見的資源物件（Resource Objects）及其功能。

## 工作負載（Workloads）資源

| 資源類型        | 描述                                                   | 用途                                       | 特點                                       |
| --------------- | ------------------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| **Pod**         | Kubernetes 中最小的部署單位，包含一個或多個容器。      | 執行應用程式容器，是調度和管理的基本單位。 | 容器共享網路和儲存，生命週期短暫且可替換。 |
| **Deployment**  | 管理無狀態應用的 Pod 副本，支持滾動更新與回滾。        | 用於無狀態服務的部署與擴展。               | 自動擴縮、滾動升級、回滾。                 |
| **StatefulSet** | 管理有狀態應用的 Pod，提供穩定的網路 ID 和持久化儲存。 | 適合資料庫、分散式系統等有狀態應用。       | 保證 Pod 順序啟動與終止，穩定網路和儲存。  |
| **DaemonSet**   | 確保每個 Node 上運行一個 Pod 實例。                    | 適合系統級任務，如日誌收集、監控代理。     | 新增節點自動部署，節點移除自動清理。       |
| **Job**         | 一次性任務控制器，確保 Pod 成功執行後結束。            | 適合批次處理、資料轉換等短暫任務。         | 支援重試和失敗處理。                       |
| **CronJob**     | 基於 Job 的排程控制器，定時執行任務。                  | 適合定時備份、報表生成等周期性任務。       | 支援類似 Linux cron 的排程語法。           |

---

## 網路與服務（Networking & Service Discovery）

| 資源類型    | 描述                                               | 用途                                            | 特點                                                |
| ----------- | -------------------------------------------------- | ----------------------------------------------- | --------------------------------------------------- |
| **Service** | 定義一組 Pod 的存取策略，提供穩定 IP 和 DNS 名稱。 | 負責流量負載均衡和服務發現。                    | 支援 ClusterIP、NodePort、LoadBalancer 等多種類型。 |
| **Ingress** | 定義從外部到集群內服務的 HTTP/HTTPS 路由規則。     | 用於實現基於路徑或主機名的流量路由和 TLS 終止。 | 支援多種 Ingress Controller，靈活路由。             |

---

## 儲存（Storage）

| 資源類型                        | 描述                                     | 用途                             | 特點                                                         |
| ------------------------------- | ---------------------------------------- | -------------------------------- | ------------------------------------------------------------ |
| **Volume**                      | Pod 中掛載的儲存資源，支持多種儲存後端。 | 提供容器間共享或持久化資料存儲。 | 支援多種類型，如 emptyDir、hostPath、PersistentVolumeClaim。 |
| **PersistentVolume (PV)**       | 叢集級別的儲存資源，由管理員配置。       | 提供持久化儲存給 Pod 使用。      | 與 PersistentVolumeClaim 配合使用。                          |
| **PersistentVolumeClaim (PVC)** | 用戶對持久化儲存的請求。                 | Pod 通過 PVC 使用 PV。           | 抽象底層儲存細節，方便動態配置。                             |

---

## 配置與機密管理（Configuration & Secrets）

| 資源類型      | 描述                                           | 用途                                 | 特點                                 |
| ------------- | ---------------------------------------------- | ------------------------------------ | ------------------------------------ |
| **ConfigMap** | 用於存儲非敏感配置資料，如設定檔、環境變數等。 | 將配置與容器映像分離，方便更新配置。 | 支援鍵值對、文件等多種格式。         |
| **Secret**    | 用於存儲敏感資料，如密碼、憑證、API 金鑰等。   | 保護敏感資訊，避免明文存放。         | 支援加密存儲和基於 RBAC 的存取控制。 |

---

## 命名空間與資源管理（Namespace & Resource Management）

| 資源類型          | 描述                                         | 用途                         | 特點                             |
| ----------------- | -------------------------------------------- | ---------------------------- | -------------------------------- |
| **Namespace**     | 將集群資源分隔成多個虛擬集群，實現資源隔離。 | 多租戶環境下隔離資源和權限。 | 支援配額管理和資源限制。         |
| **ResourceQuota** | 限制 Namespace 中資源使用量和物件數量。      | 控制資源分配，避免資源濫用。 | 可限制 CPU、記憶體、Pod 數量等。 |

---

## 其他常見資源

| 資源類型           | 描述                                                      | 用途                    | 特點                                   |
| ------------------ | --------------------------------------------------------- | ----------------------- | -------------------------------------- |
| **ReplicaSet**     | 確保指定數量的 Pod 副本持續運行，通常由 Deployment 管理。 | 保持 Pod 副本數量穩定。 | 一般不直接使用，配合 Deployment 使用。 |
| **ServiceAccount** | 用於 Pod 的身份認證，控制對 API Server 的存取權限。       | 管理 Pod 的權限和認證。 | 與 RBAC 配合使用。                     |

---

### 總結

Kubernetes 的資源類型豐富且多樣，涵蓋了應用部署、網路服務、儲存管理、配置管理及資源隔離等多個方面。這些資源物件組合起來，構成了 Kubernetes 強大的容器編排和管理能力。

---

**參考來源:**

[1] https://godleon.github.io/blog/Kubernetes/k8s-CoreConcept-ResourceObject-Overview/ \
[2] https://blog.pichuang.com.tw/20211112-how-to-sizing-kubernetes-resource-and-infra-resource.html \
[3] https://blog.csdn.net/weixin_41904435/article/details/140780502 \
[4] https://kubernetes.io/zh-cn/docs/reference/using-api/api-concepts/ \
[5] https://www.microfusion.cloud/hk/2020/02/27/kubernetes-gke-1/ \
[6] https://www.hwchiu.com/docs/2022/k8s-capacity-allocatable \
[7] https://learn.microsoft.com/zh-tw/azure/kubernetes-fleet/concepts-resource-propagation \
[8] https://www.ibm.com/docs/zh-tw/cloud-paks/cp-management/2.3.x?topic=collector-kubernetes-metrics-events-resources

---

[返回目錄](./../README.md)

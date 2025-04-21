# Minikube

> Minikube 是一款在本地快速啟動 Kubernetes 單節點集群的工具，適合學習、開發、測試和模擬 Kubernetes 環境。它在個人電腦的虛擬機或容器中運行完整的 Kubernetes 叢集，支援大部分 Kubernetes 功能，如 DNS、Ingress、ConfigMap、Secrets、Dashboard 等，方便用戶熟悉 Kubernetes 生態與操作。

---

## 用途與實作步驟

### 用途 1：學習與實驗 Kubernetes

Minikube 是入門 Kubernetes 的理想環境，讓使用者能在本地熟悉 Kubernetes 的基本概念與指令操作。

#### 實作步驟

1. 啟動 Minikube 單節點集群：

   ```bash
   minikube start
   ```

2. 驗證節點狀態：

   ```bash
   kubectl get nodes
   ```

   預期顯示 `minikube` 節點狀態為 `Ready`。

3. 部署範例應用（Nginx）：

   ```bash
   kubectl create deployment nginx --image=nginx
   kubectl expose deployment nginx --type=NodePort --port=80
   ```

4. 取得並存取應用 URL：

   ```bash
   minikube service nginx --url
   ```

   在瀏覽器中打開該 URL，確認 Nginx 運行正常。

---

### 用途 2：開發與測試容器化應用程式

利用 Minikube 模擬真實 Kubernetes 環境，方便開發者構建、部署和測試容器化應用。

#### 實作步驟

1. 使用 Minikube 內部 Docker 環境構建映像：

   ```bash
   eval $(minikube docker-env)
   docker build -t my-nginx:v1 .
   ```

2. 編寫 Kubernetes 部署文件 `deployment.yaml`，內容示例：

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: my-nginx
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: my-nginx
     template:
       metadata:
         labels:
           app: my-nginx
       spec:
         containers:
           - name: my-nginx
             image: my-nginx:v1
             ports:
               - containerPort: 80
   ```

3. 部署應用：

   ```bash
   kubectl apply -f deployment.yaml
   ```

4. 暴露服務並取得訪問地址：

   ```bash
   kubectl expose deployment my-nginx --type=NodePort --port=80
   minikube service my-nginx --url
   ```

---

### 用途 3：測試 Kubernetes 高級資源與功能

Minikube 支援多種 Kubernetes 進階功能，如 Ingress、ConfigMap、Secret 等，適合功能測試。

#### 實作步驟

1. 啟用 Ingress 插件：

   ```bash
   minikube addons enable ingress
   ```

2. 建立 ConfigMap：

   ```bash
   kubectl create configmap app-config --from-literal=env=production
   kubectl describe configmap app-config
   ```

3. 建立 Secret 儲存敏感資料：

   ```bash
   kubectl create secret generic db-credentials --from-literal=username=admin --from-literal=password=pass123
   kubectl get secret db-credentials -o yaml
   ```

4. 編寫並部署 Ingress 配置（`ingress.yaml`）：

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: example-ingress
   spec:
     rules:
       - host: example.local
         http:
           paths:
             - path: /
               pathType: Prefix
               backend:
                 service:
                   name: my-nginx
                   port:
                     number: 80
   ```

5. 部署 Ingress 並啟動隧道：

   ```bash
   kubectl apply -f ingress.yaml
   minikube tunnel
   curl http://example.local
   ```

---

### 用途 4：測試不同 Kubernetes 版本

Minikube 支援指定 Kubernetes 版本，方便測試應用相容性。

#### 實作步驟

1. 啟動指定版本的 Minikube：

   ```bash
   minikube start --kubernetes-version=v1.25.0
   ```

2. 驗證 Kubernetes 版本：

   ```bash
   kubectl version --short
   ```

3. 部署應用並測試相容性。

---

### 用途 5：模擬多節點 Kubernetes 環境

Minikube 支援多節點模擬，方便測試調度與容錯。

#### 實作步驟

1. 啟動多節點集群：

   ```bash
   minikube start --nodes=3
   ```

2. 查看節點列表：

   ```bash
   kubectl get nodes
   ```

3. 部署應用，觀察 Pod 調度情況。

---

### 用途 6：快速建立與重置開發測試環境

Minikube 可快速清理並重建 Kubernetes 環境，方便開發迭代。

#### 實作步驟

1. 清理所有資源：

   ```bash
   kubectl delete all --all
   ```

2. 重置 Minikube：

   ```bash
   minikube delete
   minikube start
   ```

3. 快速重複部署應用：

   ```bash
   kubectl delete -f deployment.yaml
   kubectl apply -f deployment.yaml
   ```

---

## 總結

Minikube 是本地運行 Kubernetes 單節點集群的輕量級工具，適合學習、開發、測試及功能驗證。它支援多種 Kubernetes 功能與插件，並可模擬多節點環境和指定版本，方便用戶在本地快速搭建完整的 Kubernetes 環境。

---

**參考來源:**

[1] https://kubernetes.io/zh-cn/docs/tutorials/hello-minikube/ \
[2] https://www.cnblogs.com/itzgr/p/11044235.html \
[3] https://www.guandata.com/gy/post/28495.html \
[4] https://k8s.whuanle.cn/2.deploy/1.minikube.html \
[5] https://www.cnblogs.com/FLY_DREAM/p/13951719.html \
[6] https://people.wikimedia.org/~jayme/k8s-docs/v1.16/zh/docs/setup/learning-environment/minikube/ \
[7] https://vividcode.cc/minikube-get-started/ \
[8] https://colobu.com/2022/06/02/setup-a-k8s-cluster-with-minikube/

---

[返回目錄](./../README.md)

# Kubernetes 中 RBAC 的實踐說明

> 以下是 Kubernetes 中 RBAC（基於角色的存取控制）的實踐說明，分為核心概念、配置示例、最佳實踐與運作流程四部分整理：

---

## 核心概念

- **角色（Role / ClusterRole）**  
  定義一組權限規則（rules），指定可操作的資源類型（resources）及允許的行為（verbs，如 get、list、create、delete 等）。

  - Role：作用於特定命名空間（namespace）內。
  - ClusterRole：作用於整個集群（cluster）範圍，可跨命名空間。

- **角色綁定（RoleBinding / ClusterRoleBinding）**  
  將角色授權給使用者（User）、群組（Group）或服務帳號（ServiceAccount）。

  - RoleBinding：綁定 Role 至 namespace 內的主體。
  - ClusterRoleBinding：綁定 ClusterRole 至整個集群的主體。

- **主體（Subjects）**  
  包含 User、Group、ServiceAccount，代表被授權的實體。

- **權限（Permissions）**  
  透過定義資源（resources）和動作（verbs）組合，控制可執行的操作。

---

## 配置示例

### Role 與 RoleBinding 範例（命名空間級別）

```yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: pod-reader
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: read-pods
  namespace: default
subjects:
  - kind: User
    name: alan
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

- 使用者 `alan` 獲得在 `default` 命名空間中讀取 Pod 的權限。

### ClusterRole 與 ClusterRoleBinding 範例（集群級別）

```yaml
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: service-watcher
rules:
  - apiGroups: [""]
    resources: ["services"]
    verbs: ["get", "list", "watch"]
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: watch-services-global
subjects:
  - kind: User
    name: bob
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: service-watcher
  apiGroup: rbac.authorization.k8s.io
```

- 使用者 `bob` 可在整個集群中監視服務（services）。

---

## RBAC 最佳實踐

- **最小權限原則**：只授予使用者或服務帳號執行工作所需的最低權限，避免過度授權。
- **定期審核**：定期檢查角色與角色綁定，確保符合最新安全政策。
- **命名空間隔離**：利用命名空間分隔不同團隊或應用，限制權限範圍。
- **使用 ClusterRole 與 ClusterRoleBinding 管理跨命名空間權限**，避免重複配置。
- **服務帳號（ServiceAccount）授權**：為 Pod 或控制器分配專用服務帳號，限制其操作權限。

---

## RBAC 運作流程與啟用

- Kubernetes API Server 啟動時需開啟 RBAC 授權模式（`--authorization-mode=RBAC`）。
- 使用者或服務帳號發出 API 請求時，API Server 會根據 RBAC 規則判斷是否允許該操作。
- RBAC 規則可動態更新，無需重啟 API Server。
- RBAC 與身份認證（Authentication）配合使用，確保請求者身份明確。

---

## 實際應用示意

- 多團隊共用一個 Kubernetes 集群，透過命名空間與 RBAC 控制各團隊只能操作自己命名空間的資源。
- 為自動化工具、Operator、Controller 指定服務帳號及相應角色，限制其權限範圍。
- 利用 ClusterRole 管理集群級別資源的存取，如節點、持久卷等。

---

以上內容綜合了 Kubernetes 官方文檔與實務案例，說明了 RBAC 在 Kubernetes 中的核心概念、配置方式、最佳實踐及運作機制，幫助安全且有效地管理集群存取權限。

---

**參考來源:**

[1] https://vocus.cc/article/6561a6d4fd8978000126c320 \
[2] https://kubernetes.io/zh-cn/docs/concepts/security/rbac-good-practices/ \
[3] https://kubernetes.io/zh-cn/docs/reference/access-authn-authz/rbac/ \
[4] https://www.anquanke.com/post/id/300925 \
[5] https://ithelp.ithome.com.tw/articles/10300806 \
[6] https://erhwenkuo.github.io/kubernetes/05-reference/access-authn-authz/k8s-authorization-of-sa-with-rbac/ \
[7] https://ithelp.ithome.com.tw/m/articles/10346993 \
[8] https://cloud.google.com/kubernetes-engine/docs/best-practices/rbac

---

[返回目錄](./../README.md)

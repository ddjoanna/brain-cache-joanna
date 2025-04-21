## Docker 與 Traefik 說明

> Traefik 是一款現代化的開源反向代理與負載均衡器，特別適合容器化環境（如 Docker、Kubernetes），能自動發現服務並動態配置路由，減少手動設定負擔。Traefik 支援 HTTP、HTTPS、TCP、UDP 等多種協議，並內建 Let’s Encrypt 自動管理 SSL 證書，方便安全地暴露服務。

---

## Traefik 使用情境範例說明

- **微服務架構**：多個 Docker 容器化服務（Web API、前端、後端服務）動態啟停，Traefik 自動發現並路由流量，實現負載均衡和高可用。
- **本地開發環境**：開發者快速啟動多個容器服務，Traefik 自動配置路由和 HTTPS，無需手動設定反向代理。
- **多個 Web 服務共存**：同一台主機上運行多個網站或應用，透過不同域名或路徑由 Traefik 分流請求到對應容器。
- **混合協議支持**：除了 HTTP，還可代理 TCP/UDP 服務，如資料庫或消息隊列。

---

## Docker-Compose 配置範例：多個 Web Server 流量分類

以下示範如何用 Traefik 搭配 Docker Compose，根據不同網域將流量導向兩個不同的 Web 服務容器。

```yaml
version: "3.8"

services:
  traefik:
    image: traefik:v2.10
    command:
      - "--api.insecure=true" # 啟用儀表板（開發用）
      - "--providers.docker=true" # 啟用 Docker Provider，自動發現容器
      - "--entrypoints.web.address=:80" # 定義 HTTP 入口點
      - "--entrypoints.websecure.address=:443" # 定義 HTTPS 入口點
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true" # TLS挑戰
      - "--certificatesresolvers.myresolver.acme.email=you@example.com"
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"
    ports:
      - "80:80"
      - "443:443"
      - "8080:8080" # Traefik 儀表板
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock:ro" # 監控 Docker 容器
      - "./letsencrypt:/letsencrypt" # SSL 證書存放
    restart: always

  web1:
    image: nginx:alpine
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.web1.rule=Host(`web1.example.com`)"
      - "traefik.http.routers.web1.entrypoints=web"
      - "traefik.http.services.web1.loadbalancer.server.port=80"

  web2:
    image: nginx:alpine
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.web2.rule=Host(`web2.example.com`)"
      - "traefik.http.routers.web2.entrypoints=web"
      - "traefik.http.services.web2.loadbalancer.server.port=80"
```

### 說明

- Traefik 監控 Docker 容器，根據容器標籤自動建立路由規則。
- 訪問 `web1.example.com` 的流量會被導向 `web1` 容器。
- 訪問 `web2.example.com` 的流量會被導向 `web2` 容器。
- Traefik 同時管理 HTTP 和 HTTPS（可自動申請證書）。
- 儀表板可透過 8080 端口查看服務狀態。

---

## 小結

- **Traefik** 是容器化環境中自動化流量管理的利器，支持動態服務發現與配置。
- 適用於多服務、多域名、多協議的流量分類與負載均衡。
- 與 Docker 深度整合，減少手動配置，提升微服務架構的靈活性與可維護性。

---

**參考來源:**

[1] https://blog.tangwudi.com/technology/docker12880/ \
[2] https://blog.csdn.net/galoiszhou/article/details/142761319 \
[3] https://www.4async.com/2016/08/2016-08-01-introduce-traefik-load-balance/ \
[4] https://developer.volcengine.com/articles/7392433028087332874 \
[5] https://www.qikqiak.com/post/traefik-2.1-101/ \
[6] https://docs.youdianzhishi.com/k8s/network/traefik/ \
[7] https://soulteary.com/2023/07/18/traefik-v3-docker-comprehensive-user-guide-basics.html \
[8] https://www.showapi.com/news/article/66b97e0f4ddd79f11a000054

---

[返回目錄](./../README.md)

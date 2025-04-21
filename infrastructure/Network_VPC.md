# VPC

> VPC（Virtual Private Cloud，虛擬私有雲）是一種在公有雲環境中，為用戶建立的邏輯隔離虛擬網路，讓用戶能像在自有資料中心內操作傳統網路一樣，完全掌控和管理其網路環境[1][2][5][6]。

---

## VPC 的主要特性與組成

- **邏輯隔離虛擬網路**  
  VPC 提供一個獨立的虛擬網路空間，讓用戶在雲端中部署資源（如虛擬機、容器、資料庫等），彼此隔離且安全，避免與其他用戶的資源互相干擾[1][3][5]。

- **子網（Subnet）**  
  VPC 內部可劃分多個子網，每個子網擁有獨立的 IP 地址範圍，且必須位於單一可用區域。子網用於分類管理不同類型的資源，並可設定不同的安全策略[1][2][5]。

- **IP 定址**  
  用戶可自訂 VPC 及子網的 IPv4 和 IPv6 地址範圍，並可將公有 IP 地址或 IPv6 全球唯一地址配置給 VPC 中的資源，如虛擬機、NAT 閘道、負載均衡器等[1][2]。

- **路由與閘道**  
  VPC 使用路由表控制網路流量的導向，並透過網際網路閘道（Internet Gateway）連接到公網，或使用 VPN、專線等方式連接到內部部署網路。還可利用 VPC 端點私下連接 AWS 服務，避免經過公網[1][2][5][6]。

- **安全控制**  
  包含虛擬防火牆（vFW）、安全組（Security Group）等多層安全機制，控制流入與流出 VPC 或子網的流量，保障網路安全[5][6]。

- **對等互連（Peering）與傳輸閘道**  
  支援不同 VPC 間的對等連線，實現跨 VPC 資源互訪；傳輸閘道則作為中央樞紐，連接多個 VPC、VPN 及專線，統一管理流量路由[1][5][6]。

- **流量鏡射與流量日誌**  
  可複製網路流量送至安全監控設備進行深度檢查，並記錄 VPC 內網路介面的 IP 流量資訊，方便監控與故障排查[1][2]。

---

## VPC 的用途與優勢

- **安全隔離**  
  透過 VPC，使用者可在共享的公有雲基礎設施上建立獨立且安全的網路環境，避免不同用戶間的資源互相干擾或攻擊[5]。

- **靈活的網路配置**  
  使用者能自訂 IP 位址範圍、子網劃分、路由策略與安全規則，滿足複雜多變的應用需求[1][3]。

- **混合雲與多區域部署**  
  支援與內部資料中心透過 VPN 或專線連接，實現混合雲架構；並可跨多個可用區域部署資源，提高可用性與容錯性[1][5]。

- **簡化管理**  
  以軟體定義網路方式管理，無需實體硬體設備，快速部署與擴展，降低運維成本[3][6]。

---

## 總結

VPC 是一種虛擬化的私有網路解決方案，讓用戶在公有雲上擁有類似自有資料中心的網路控制權，具備高度的安全性、靈活性與可擴展性。它是現代雲端架構中不可或缺的基礎設施，廣泛應用於 AWS、Google Cloud、阿里雲、華為雲等多家雲服務平台[1][3][5][6][8]。

---

**參考來源:**

[1] https://docs.aws.amazon.com/zh_tw/vpc/latest/userguide/what-is-amazon-vpc.html \
[2] https://docs.aws.amazon.com/zh_cn/vpc/latest/userguide/what-is-amazon-vpc.html \
[3] https://mile.cloud/zh/resources/blog/vpc-introduction-network-setting-subnet_533 \
[4] https://cloud.google.com/vpc/docs/overview \
[5] https://info.support.huawei.com/info-finder/encyclopedia/zh/VPC.html \
[6] https://www.amazonaws.cn/vpc/ \
[7] https://cloud.google.com/vpc/docs/advanced-vpc \
[8] https://www.aliyun.com/product/vpc

---

[返回目錄](./../README.md)

# Terraform

> Terraform 是由 HashiCorp 公司開發的一款開源基礎設施即代碼（Infrastructure as Code，IaC）工具，允許使用者透過宣告式的配置語言（HashiCorp 配置語言，HCL）來定義、預覽及管理雲端及本地基礎設施資源[1][2][4][5]。

---

## 核心概念與工作原理

- **資源（Resource）與提供者（Provider）**  
  Terraform 的核心是「資源」和「提供者」兩大概念。資源代表基礎設施中的具體項目，如虛擬機、網路、安全組等；提供者則是與特定平台（如 AWS、阿里雲、Azure、Google Cloud）溝通的插件，負責創建和管理這些資源[2][4]。

- **宣告式配置**  
  使用者以 HCL 編寫配置檔，描述理想的基礎設施狀態。Terraform 會解析這些檔案，生成執行計劃（Plan），展示將對現有基礎設施進行的新增、修改或刪除操作，經用戶確認後執行，確保基礎設施與配置一致[1][3][5]。

- **狀態管理**  
  Terraform 會維護一個狀態檔案（state file），記錄基礎設施的當前狀態，作為未來變更的參考。狀態鎖定機制避免多人同時修改造成衝突[5][7]。

- **依賴關係圖**  
  Terraform 會根據配置自動識別資源間的依賴關係，確保按正確順序創建或銷毀資源[7]。

---

## 主要特點

- **多雲與混合雲支持**  
  支援多種公有雲、私有雲及 SaaS 服務，透過豐富的提供者插件實現跨平台管理[1][4]。

- **模組化與重用**  
  支援模組（Module）設計，方便重用和分享基礎設施配置，提高維護性和一致性[4]。

- **自動化與版本控制**  
  配置文件可納入版本控制系統，結合 CI/CD 流程實現基礎設施自動化部署[5]。

- **可擴展性**  
  開放的插件架構允許開發者擴展支持更多平台和資源類型[4][5]。

---

## 工作流程簡述

1. **編寫配置**：使用 HCL 描述所需基礎設施。
2. **初始化（terraform init）**：下載並安裝所需提供者插件。
3. **規劃（terraform plan）**：生成變更計劃，預覽資源變更。
4. **應用（terraform apply）**：執行計劃，創建或修改資源。
5. **管理與更新**：修改配置並重複規劃與應用步驟，維持基礎設施狀態。

---

## 適用場景

- 雲端基礎設施自動化管理。
- 跨多雲環境資源統一配置與部署。
- 基礎設施版本控制與審計。
- 複雜系統依賴管理與持續交付。

---

**參考來源:**

[1] https://help.aliyun.com/zh/terraform/introduction-of-terraform-1 \
[2] https://help.aliyun.com/zh/terraform/what-is-terraform \
[3] https://www.purestorage.com/tw/knowledge/terraform-plan.html \
[4] https://cit965.netlify.app/docs/terraform/terraform%E4%BB%8B%E7%BB%8D/ \
[5] https://www.omniwaresoft.com.tw/hashicorp-terraform/ \
[6] https://www.alibabacloud.com/help/zh/arms/prometheus-monitoring/terraform-overview \
[7] https://aws.amazon.com/tw/compare/the-difference-between-terraform-and-kubernetes/

---

[返回目錄](./../README.md)

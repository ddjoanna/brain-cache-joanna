# Infrastructure as Code (IaC) 說明

> Infrastructure as Code（基礎設施即代碼，簡稱 IaC）是一種通過編寫和管理可執行代碼來描述、配置、部署及維護 IT 基礎設施的技術和方法。它將基礎設施資源（如虛擬機、網絡、存儲、負載均衡、數據庫等）以代碼形式定義，並利用自動化工具實現基礎設施的自動化配置和管理。

## IaC 的核心價值與優勢

- **自動化與一致性**：消除手動配置錯誤，確保不同環境（開發、測試、預生產、正式）基礎設施配置一致。
- **可追溯與版本控制**：基礎設施配置文件可存放於 Git 等版本控制系統，支持審查、回滾和歷史追蹤。
- **快速部署與擴展**：通過代碼快速創建、修改和銷毀基礎設施，支援彈性擴展和不可變基礎設施理念。
- **提升協作效率**：團隊成員可通過 pull request 和代碼審查流程協同管理基礎設施變更。
- **降低運維風險與成本**：減少人工操作錯誤和重複工作，提高基礎設施管理的可靠性和效率。

---

## IaC 的應用場景

- **多環境管理**  
  在開發、測試、預生產和生產環境中，保持基礎設施配置一致，避免環境切換問題。

- **雲資源自動化部署**  
  利用 IaC 自動化創建和管理雲端虛擬機、網絡、安全組、存儲等資源。

- **持續集成/持續交付（CI/CD）**  
  將基礎設施配置納入 CI/CD 流水線，自動化基礎設施的部署和更新。

- **災難恢復與擴展**  
  快速重建基礎設施，實現快速擴容和故障恢復。

- **合規與安全審計**  
  通過代碼審查和版本控制，確保基礎設施符合安全和合規要求。

---

## IaC 常用工具

- **Terraform**：雲平台無關的基礎設施編排工具，使用 HCL 語言描述資源。
- **Ansible**：基於 YAML 的配置管理和應用部署工具，支持自動化任務。
- **Chef、Puppet、SaltStack**：配置管理工具，支持複雜基礎設施配置。
- **CloudFormation（AWS）**、**ARM Templates（Azure）**：雲廠商專屬 IaC 工具。

---

## IaC 與傳統基礎設施管理比較表

| 特性         | 傳統手動管理                     | Infrastructure as Code (IaC)               |
| ------------ | -------------------------------- | ------------------------------------------ |
| **配置方式** | 手動操作，通過控制台或命令行配置 | 以代碼形式描述基礎設施，通過自動化工具執行 |
| **一致性**   | 易出錯，環境間配置不一致         | 保證環境配置一致，支持不可變基礎設施       |
| **版本控制** | 無版本控制，難以追蹤歷史變更     | 配置文件存於版本控制系統，支持審查和回滾   |
| **部署速度** | 慢，需人工操作                   | 快速自動化部署，支持大規模擴展             |
| **錯誤率**   | 高，易因手動操作導致配置錯誤     | 低，代碼可測試和審查，減少人為錯誤         |
| **協作效率** | 低，溝通和同步困難               | 高，通過代碼審查和 CI/CD 流程協作          |
| **可追蹤性** | 差，缺乏完整審計和變更記錄       | 好，版本控制系統提供完整變更歷史           |

---

## 總結

Infrastructure as Code（IaC）是現代 IT 基礎設施管理的核心方法，通過代碼實現基礎設施的自動化、標準化和可追蹤管理。它能大幅提升部署效率、降低錯誤率，並支持 DevOps 和 CI/CD 流程，廣泛應用於雲計算資源管理、多環境同步、持續交付、災難恢復及合規審計等場景。

---

**參考來源:**

[1] https://www.aliyun.com/getting-started/what-is/what-is-iac \
[2] https://aws.amazon.com/cn/what-is/iac/ \
[3] https://www.trendmicro.com/zh_hk/what-is/cloud-security/infrastructure-as-code.html \
[4] https://blog.csdn.net/universsky2015/article/details/140028749 \
[5] https://doc.devpod.cn/devops/infrastructure-as-code-15237133.html \
[6] https://blog.csdn.net/ss810540895/article/details/130944273 \
[7] https://www.redhat.com/zh/topics/automation/what-is-infrastructure-as-code-iac \  
[8] https://learn.microsoft.com/zh-cn/devops/deliver/what-is-infrastructure-as-code \

---

[返回目錄](./../README.md)

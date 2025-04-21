# Information Leakage（資訊洩露）和 Improper Error Handling（不當錯誤處理）

> Information Leakage（資訊洩露）與 Improper Error Handling（不當錯誤處理）是常見且危害重大的安全弱點，兩者往往相互關聯，導致敏感資訊暴露並增加系統被攻擊的風險。

## Information Leakage（資訊洩露）

### 定義與成因

資訊洩露指的是機密或敏感資料在未經授權的情況下被外洩或暴露，可能是意外或惡意行為導致[1][2][5]。

- **內部因素**：員工疏忽（如誤發郵件、丟失設備）、惡意竊取、系統配置錯誤等。
- **外部因素**：駭客入侵、惡意軟體感染、未授權存取等。
- **錯誤配置或設計缺陷**：如不當的權限設定、未加密敏感資料、系統回傳過多錯誤細節。

### 影響

- 個人資料、商業機密洩漏，造成經濟損失與法律風險。
- 企業信譽受損，客戶流失。
- 可能引發後續攻擊（如身份盜用、詐騙）。

### 預防與應對措施

- 實施嚴格的存取控制與權限管理。
- 加密敏感資料並限制資料暴露範圍。
- 員工安全意識培訓與內部監控。
- 定期安全審計與漏洞掃描。
- 事件發生時快速識別、回應並通知利害關係人[5][6]。

---

## Improper Error Handling（不當錯誤處理）

### 定義與問題

不當錯誤處理指系統在遇到錯誤或異常時，未妥善處理或過度暴露錯誤訊息，導致敏感內部資訊（如系統架構、資料庫結構、程式碼路徑、堆疊追蹤等）被外部使用者獲取[4]。

- 例如，系統直接回傳詳細的錯誤堆疊訊息給使用者。
- 錯誤訊息中包含帳號、密碼、API 金鑰等敏感資訊。

### 風險

- 攻擊者可利用錯誤訊息分析系統弱點，設計針對性攻擊。
- 增加資料洩露風險。
- 破壞使用者信任與系統穩定性。

### 防範建議

- 僅回傳通用且不含敏感資訊的錯誤訊息給終端使用者。
- 在伺服器端記錄詳細錯誤日誌，供開發與維運分析。
- 實施錯誤分類與分級管理，避免敏感資訊外洩。
- 使用安全框架與中介軟體統一錯誤處理。
- 定期測試錯誤處理流程，確保不洩露敏感資料。

---

## 總結

| 風險類型     | 主要問題             | 影響                               | 防範重點                               |
| ------------ | -------------------- | ---------------------------------- | -------------------------------------- |
| 資訊洩露     | 機密資料未授權暴露   | 經濟損失、法律風險、信譽受損       | 權限控管、資料加密、員工培訓、監控     |
| 不當錯誤處理 | 錯誤訊息暴露系統細節 | 協助攻擊者偵測弱點，增加攻擊成功率 | 通用錯誤訊息、伺服器日誌、錯誤分級管理 |

資訊洩露與不當錯誤處理往往相輔相成，合理設計錯誤處理流程並嚴格保護敏感資料，是降低系統安全風險的重要環節[1][2][4][5]。

---

**參考來源:**

[1] https://www.fortinet.com/tw/resources/cyberglossary/data-leak \
[2] https://legal.fronteo.com/zh-TW/fllp/information-leakage \
[3] https://law.moj.gov.tw/LawClass/LawAll.aspx?PCode=I0050021 \
[4] https://www.twcert.org.tw/newepaper/cp-92-38-c01cc-3.html \
[5] https://www.microsoft.com/zh-tw/security/business/security-101/what-is-a-data-breach \
[6] https://legal.fronteo.com/zh-TW/fllp/leakage-investigation \
[7] https://www.irs.gov/zh-hant/identity-theft-fraud-scams/data-breach-information-for-taxpayers \
[8] https://www.taipeinet.com.tw/tw/news/show.aspx?num=1672&kind=14

---

[返回目錄](./../README.md)

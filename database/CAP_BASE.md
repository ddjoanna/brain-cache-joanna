# CAP vs BASE 理論

## CAP 理論說明

CAP 理論，又稱為布魯爾定理（Brewer's theorem），是分布式系統設計中的核心理論，由 Eric Brewer 於 2000 年提出，並在 2002 年由 Seth Gilbert 和 Nancy Lynch 正式證明[5][4]。

CAP 代表三個特性：

- **一致性（Consistency）**：所有節點在同一時間點看到相同的資料狀態，即每次讀取都能取得最新的寫入結果。
- **可用性（Availability）**：系統的每個非故障節點都能在合理時間內回應請求，保證系統持續可用。
- **分區容錯性（Partition tolerance）**：系統能夠容忍網路分區（節點間通訊中斷或延遲），依然保持運作。

CAP 理論指出，在分布式系統中，這三者最多只能同時滿足兩項，無法三者兼得[1][2][3][4][5]。當網路分區發生時，系統必須在一致性和可用性之間做出取捨：

- **CP 系統（Consistency + Partition tolerance）**：保證資料一致性與分區容錯，犧牲部分可用性。當分區發生時，部分節點可能無法提供服務以維持一致性。
- **AP 系統（Availability + Partition tolerance）**：保證系統可用與分區容錯，犧牲一致性。分區期間系統仍回應請求，但資料可能暫時不一致。
- **CA 系統（Consistency + Availability）**：保證一致性與可用性，但不具備分區容錯性。此模型在無分區的理想環境下可行，現實分布式環境中較少見[5][4]。

---

## BASE 理論說明

BASE 理論是為了彌補傳統 ACID（原子性、一致性、隔離性、持久性）在分布式系統中難以實現的限制而提出的輕量級一致性模型，常用於 NoSQL 和大數據系統。

BASE 代表：

- **Basically Available（基本可用）**：系統保證基本的可用性，能對請求做出響應，但響應可能是部分資料或延遲的結果。
- **Soft state（軟狀態）**：系統狀態允許隨時間變化，即使沒有輸入，狀態也可能改變（例如透過後台同步）。
- **Eventual consistency（最終一致性）**：系統不保證立即一致，但保證在沒有新的更新後，最終所有節點的資料會達到一致。

BASE 理論強調系統的可用性和可擴展性，允許短暫的不一致，適合高併發、大規模分布式場景，與 CAP 理論中的 AP 模型相呼應[1][5]。

---

## 總結比較

| 理論          | 核心概念               | 主要特性                                 | 適用場景                  |
| ------------- | ---------------------- | ---------------------------------------- | ------------------------- |
| **CAP 理論**  | 分布式系統三大特性取捨 | 一致性、可用性、分區容錯性三者只能二選一 | 分布式系統設計與架構選擇  |
| **BASE 理論** | 輕量級一致性模型       | 基本可用、軟狀態、最終一致性             | 大數據、NoSQL、高併發系統 |

---

**參考來源:**

[1] https://cloud.tencent.com/developer/article/1860632 \
[2] https://www.hollischuang.com/archives/666 \
[3] https://xunhuanfengliuxiang.gitbooks.io/system-desing/content/fen-bu-shi-xi-tong-de-cap-li-lun.html \
[4] https://zh.wikipedia.org/zh-hant/CAP%E5%AE%9A%E7%90%86 \
[5] https://blog.csdn.net/weixin_49025285/article/details/140309592 \
[6] https://godleon.github.io/blog/Architecture_Design/Architecture-Design-HA-CAP/ \
[7] https://juejin.cn/post/7277490138517798931

---

[返回目錄](./../README.md)

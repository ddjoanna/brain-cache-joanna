# ACID 事務模型

> ACID 是資料庫事務（Transaction）必須具備的四個基本特性，用以確保資料操作的正確性與可靠性。

## 四個基本特性

### 原子性（Atomicity）

事務中的所有操作要麼全部完成，要麼全部不做，確保不可分割。若事務中任何一個步驟失敗，系統會回滾至事務開始前的狀態，避免資料不完整或錯誤。例如轉帳時，扣款和入帳必須同時成功或同時失敗[1][3][5]。

### 一致性（Consistency）

事務執行前後，資料必須保持一致的狀態，遵守資料庫的完整性約束。事務將資料庫從一個有效狀態轉變為另一個有效狀態，任何違反規則的操作都會被拒絕[1][3][5]。

### 隔離性（Isolation）

多個事務並發執行時，彼此間不會互相干擾。每個事務的中間狀態對其他事務不可見，避免讀到未提交的資料或發生競爭條件。隔離性確保事務間執行結果如同串行執行[1][3][5][6]。

### 持久性（Durability）

一旦事務提交，對資料的修改即永久保存，即使系統發生故障（如斷電、崩潰）也不會遺失。資料的改變會被寫入持久儲存設備[1][3][5]。

---

### 補充說明

- ACID 事務模型多用於關聯式資料庫，保證交易的正確性與可靠性。
- 在分散式系統中，實現 ACID 事務較為複雜，常用二階段提交（2PC）、三階段提交（3PC）等協議來達成[2]。
- 分散式環境下，因 CAP 理論限制，系統可能會在一致性、可用性與分區容錯性間做權衡，部分系統選擇放寬一致性，採用 BASE 模型[1][4][6][7]。
- 微服務架構中，因服務自治和去中心化資料庫，通常採用最終一致性和補償交易（如 SAGA 模式）來替代嚴格的 ACID 事務[5]。

---

## 總結：

| ACID 特性 | 說明                                 |
| --------- | ------------------------------------ |
| 原子性    | 事務不可分割，全部成功或全部失敗     |
| 一致性    | 事務前後資料保持一致，符合完整性約束 |
| 隔離性    | 多事務並發執行不互相干擾             |
| 持久性    | 事務提交後資料永久保存，不會丟失     |

---

**參考來源:**

[1] https://aws.amazon.com/tw/compare/the-difference-between-acid-and-base-database/ \
[2] https://rickhw.github.io/2020/05/16/DistributedSystems/Distributed-Transactions/ \
[3] https://www.solix.com/zh-TW/kb/acid-transactions/ \
[4] https://hackmd.io/@AmdAc990TDm3EkP4EmImTA/Hkg62nmND \
[5] https://blog.udn.com/robertyjlai/160267981 \
[6] https://blog.csdn.net/poocher/article/details/115049598 \
[7] https://cloud.tencent.com/developer/article/1165624 \
[8] https://blog.csdn.net/xingduan5153/article/details/103443037

---

[返回目錄](./../README.md)

# Stack（堆疊）與 Queue（佇列）說明

## Stack（堆疊）

- **定義與特性**  
  Stack 是一種線性資料結構，遵循「後進先出」（LIFO, Last In First Out）原則，即最後放入的元素會最先被取出。可以想像成一疊盤子，最上面的盤子先被拿走。
- **基本操作**
  - `push`：將元素加入堆疊頂端
  - `pop`：從堆疊頂端取出元素
  - `peek`（或 `top`）：查看堆疊頂端元素但不移除
- **時間複雜度**
  - 插入（push）與刪除（pop）均為 O(1)
  - 查找（lookup）為 O(n)
- **實作方式**  
  可用陣列（Array）或鏈結串列（Linked List）實作。陣列實作因記憶體連續且操作簡單，通常效率較好，但大小固定；鏈結串列則可動態調整大小。
- **應用範例**
  - 瀏覽器的回上一頁功能
  - 程式語言的函數呼叫堆疊（Call Stack）
  - 撤銷（Undo）功能
  - 遞迴運算與表達式求值

---

## Queue（佇列）

- **定義與特性**  
  Queue 是一種線性資料結構，遵循「先進先出」（FIFO, First In First Out）原則，即最先加入的元素會最先被取出。可以想像成排隊買票，先來的人先買票。
- **基本操作**
  - `enqueue`：將元素加入佇列尾端
  - `dequeue`：從佇列前端取出元素
  - `front`：查看佇列前端元素但不移除
- **時間複雜度**
  - 插入（enqueue）與刪除（dequeue）均為 O(1)
  - 查找（access）為 O(n)
- **實作方式**  
  可用陣列（Array）或鏈結串列（Linked List）實作。陣列實作時常用環狀佇列（Circular Queue）避免空間浪費。
- **應用範例**
  - 作業系統的排程（Ready Queue、Job Queue）
  - 非同步事件處理（Event Queue）
  - 緩衝區（Buffering）
  - 廣度優先搜尋（BFS）

---

## Stack 與 Queue 的比較

| 特性         | Stack（堆疊）                | Queue（佇列）              |
| ------------ | ---------------------------- | -------------------------- |
| 存取順序     | 後進先出（LIFO）             | 先進先出（FIFO）           |
| 新增元素位置 | 頂端（尾端）                 | 尾端                       |
| 移除元素位置 | 頂端（尾端）                 | 前端                       |
| 常用操作     | push、pop、peek              | enqueue、dequeue、front    |
| 典型應用     | 函數呼叫堆疊、瀏覽器歷史紀錄 | 任務排程、事件處理、緩衝區 |
| 實作結構     | 陣列或鏈結串列               | 陣列（環狀佇列）或鏈結串列 |

---

## 總結

- **Stack** 適用於需要「後進先出」的場景，強調最近加入的元素先被處理。
- **Queue** 適用於需要「先進先出」的場景，強調公平排隊與依序處理。

兩者皆是基礎且重要的抽象資料結構，廣泛應用於程式設計、系統架構與演算法中。

---

**參考來源:**

[1] https://justnote.coderbridge.io/2022/03/06/stack-and-queue/ \
[2] https://pjchender.github.io/dsa/dsa-stacks-queues/ \
[3] https://jimmyswebnote.com/stack-queue/ \
[4] https://ithelp.ithome.com.tw/m/articles/10325925 \
[5] https://simonecheng.github.io/stack-and-queue/ \
[6] https://blog.csdn.net/fight_girl/article/details/78075119 \
[7] https://ithelp.ithome.com.tw/m/articles/10276473 \
[8] https://hackmd.io/@asdfghjklll123/BJchfgWJ5

---

[返回目錄](./../README.md)

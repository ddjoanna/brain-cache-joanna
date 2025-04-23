# MongoDB 查詢與操作

> MongoDB 常用的查詢與操作方式，包括 CRUD、聚合（aggregate）及關聯查詢（join lookup）：

## 1. CRUD 操作（增刪改查）

- **Create（新增）**

  - `insertOne()`：插入單個文件
  - `insertMany()`：插入多個文件

  ```js
  db.collection.insertOne({ name: "Alice", age: 25 });
  db.collection.insertMany([{ name: "Bob" }, { name: "Charlie" }]);
  ```

- **Read（查詢）**

  - `find()`：查詢文件，可帶條件過濾
  - `findOne()`：查詢單個文件

  ```js
  db.collection.find({ age: { $gt: 20 } });
  db.collection.findOne({ name: "Alice" });
  ```

- **Update（更新）**

  - `updateOne()`：更新單個文件
  - `updateMany()`：更新多個文件
  - `replaceOne()`：替換整個文件

  ```js
  db.collection.updateOne({ name: "Alice" }, { $set: { age: 26 } });
  db.collection.updateMany({ age: { $lt: 30 } }, { $inc: { age: 1 } });
  ```

- **Delete（刪除）**
  - `deleteOne()`：刪除單個文件
  - `deleteMany()`：刪除多個文件
  ```js
  db.collection.deleteOne({ name: "Bob" });
  db.collection.deleteMany({ age: { $gte: 30 } });
  ```

以上 CRUD 操作均針對單一集合，且寫入操作在單個文件層級是原子性的[1][2][3][5]。

## 2. 聚合操作（Aggregate）

MongoDB 聚合框架用於對資料進行複雜的查詢和數據處理，常見操作包括分組、過濾、排序、計算等。

- 使用 `aggregate()` 方法，傳入一組管道（pipeline）階段：

```js
db.collection.aggregate([
  { $match: { status: "A" } }, // 篩選
  { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }, // 分組計算
  { $sort: { total: -1 } }, // 排序
]);
```

聚合管道可串接多個階段，靈活處理複雜邏輯，適合統計分析、報表等需求。

## 3. Join 查詢（$lookup）

MongoDB 4.0 以後支援類似 SQL 的 join 操作，使用 `$lookup` 來實現跨集合關聯查詢。

- 範例：從 orders 集合中查詢訂單並關聯用戶資料

```js
db.orders.aggregate([
  {
    $lookup: {
      from: "users", // 目標集合
      localField: "user_id", // orders 中的欄位
      foreignField: "_id", // users 中的欄位
      as: "user_info", // 結果放入陣列欄位
    },
  },
]);
```

`$lookup` 可實現一對多、多對多關聯，方便在無關聯型資料庫中進行關聯查詢。

---

## 總結：

| 操作類型 | 常用方法                                              | 功能說明                   |
| -------- | ----------------------------------------------------- | -------------------------- |
| **CRUD** | `insertOne()`, `find()`, `updateOne()`, `deleteOne()` | 新增、查詢、更新、刪除文件 |
| **聚合** | `aggregate()`                                         | 複雜資料處理、分組、統計   |
| **Join** | `$lookup`（聚合管道中）                               | 跨集合關聯查詢             |

這些是 MongoDB 最常用的查詢與操作方式，能滿足大部分應用的資料操作需求[1][2][3][5]。

---

**參考來源:**

[1] https://www.mongodb.com/zh-cn/resources/products/fundamentals/crud \
[2] https://docs.mongoing.com/mongodb-crud-operations \
[3] https://www.mongodb.com/zh-cn/docs/mongodb-shell/crud/ \
[4] https://blog.csdn.net/u014231523/article/details/103355631 \
[5] https://www.mongodb.com/zh-cn/docs/rapid/crud/ \
[6] https://mongoing.com/docs/crud.html \
[7] https://mongodb.net.cn/manual/crud/ \
[8] https://www.mongodb.com/zh-cn/docs/drivers/go/v1.16/fundamentals/crud/

---

[返回目錄](./../README.md)

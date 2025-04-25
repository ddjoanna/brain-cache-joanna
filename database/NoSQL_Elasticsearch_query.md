# Elasticsearch 常用查詢與操作總整理

## 基本查詢

### 查詢所有文件（Match All Query）

```json
GET /index_name/_search
{
  "query": {
    "match_all": {}
  }
}
```

- 功能：取得索引中所有文件，類似 SQL 的 `SELECT *`。
- 用途：測試或需要全量資料時使用。

---

### 根據 ID 查詢

```json
GET /index_name/_doc/1
```

- 功能：根據文件 ID 精確查詢。
- 類似 SQL：`SELECT * FROM index_name WHERE _id = '1'`。

---

## 文字查詢

### Match Query（全文匹配）

```json
GET /index_name/_search
{
  "query": {
    "match": {
      "field_name": "搜尋內容"
    }
  }
}
```

- 會先分詞，再根據詞條匹配倒排索引。
- 適合全文檢索。

---

### Term Query（精確匹配）

```json
GET /index_name/_search
{
  "query": {
    "term": {
      "field_name.keyword": "精確值"
    }
  }
}
```

- 不分詞，直接匹配詞條，適合 keyword 或數值欄位。
- 用於精確查詢。

---

### Multi Match Query（多欄位全文檢索）

```json
GET /index_name/_search
{
  "query": {
    "multi_match": {
      "query": "搜尋詞",
      "fields": ["field1", "field2"]
    }
  }
}
```

- 同時在多個欄位搜尋，提升搜尋覆蓋率。

---

### Match Phrase Query（短語匹配）

```json
GET /index_name/_search
{
  "query": {
    "match_phrase": {
      "field_name": "完整短語"
    }
  }
}
```

- 搜尋連續且順序一致的詞組。

---

### Prefix Query（前綴查詢）

```json
GET /index_name/_search
{
  "query": {
    "prefix": {
      "field_name": "前綴詞"
    }
  }
}
```

- 查找以指定字串開頭的詞。

---

### Wildcard Query（通配符查詢）

```json
GET /index_name/_search
{
  "query": {
    "wildcard": {
      "field_name": "elasti*"
    }
  }
}
```

- 支援 `*` 和 `?` 通配符，模糊匹配。

---

### Fuzzy Query（模糊查詢）

```json
GET /index_name/_search
{
  "query": {
    "fuzzy": {
      "field_name": {
        "value": "elstic",
        "fuzziness": "AUTO"
      }
    }
  }
}
```

- 容許拼寫錯誤的近似匹配。

---

## 布林查詢（Bool Query）

### 說明

- **must**：所有條件必須滿足（AND）；適合相關度排序的全文檢索。
- **should**：至少滿足一個條件（OR）。
- **must_not**：條件必須不滿足（NOT）。
- **filter**：必須滿足，且不影響相關性評分，適合過濾、篩選條件。

### 範例

```json
GET /index_name/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "title": "Elasticsearch" } },
        { "range": { "date": { "gte": "2023-01-01" } } }
      ],
      "should": [
        { "term": { "category": "tech" } }
      ],
      "must_not": [
        { "term": { "status": "draft" } }
      ],
      "filter": [
        { "term": { "brand": "Starbucks" } }
      ]
    }
  }
}
```

---

## 範圍查詢（Range Query）

```json
GET /index_name/_search
{
  "query": {
    "range": {
      "price": {
        "gte": 100,
        "lte": 500
      }
    }
  }
}
```

- 查詢數字或日期在指定區間的文件。

---

## 字段存在查詢（Exists Query）

```json
GET /index_name/_search
{
  "query": {
    "exists": {
      "field": "field_name"
    }
  }
}
```

- 查找該欄位存在（非空）的文件。

---

## 聚合查詢（Aggregations）

### Terms 聚合（分組計數）

```json
GET /index_name/_search
{
  "size": 0,
  "aggs": {
    "category_count": {
      "terms": {
        "field": "category.keyword"
      }
    }
  }
}
```

- 統計不同類別的文件數量。

---

## IK 分詞器相關操作

### 使用 IK 分詞器

- 在 mapping 中設定欄位使用 IK 分詞器：

```json
{
  "mappings": {
    "properties": {
      "name": {
        "type": "text",
        "analyzer": "ik_max_word",
        "search_analyzer": "ik_smart"
      }
    }
  }
}
```

- `ik_max_word`：細粒度分詞，適合建立索引。
- `ik_smart`：粗粒度分詞，適合搜尋時使用。

---

### 查看 IK 分詞結果

使用 `_analyze` API 測試分詞效果：

```json
GET /_analyze
{
  "analyzer": "ik_max_word",
  "text": "高山茶葉"
}
```

回傳示例：

```json
{
  "tokens": [{ "token": "高山" }, { "token": "茶葉" }, { "token": "高山茶" }]
}
```

---

## 其他常用查詢

### Terms Query（多值精確匹配）

- 查找欄位值在指定列表中的文件。

```json
GET /index_name/_search
{
  "query": {
    "terms": {
      "field_name.keyword": ["value1", "value2"]
    }
  }
}
```

---

**參考來源:**

[1] https://blog.csdn.net/weixin_43597208/article/details/135002703 \
[2] https://www.cnblogs.com/xingzr/p/18529208 \
[3] https://blog.csdn.net/Solo95/article/details/138393437 \
[4] https://www.jianshu.com/p/33e711424cf6 \
[5] https://www.cnblogs.com/leadership/p/12396971.html \
[6] https://maizitoday.github.io/post/elasticsearch%E5%B8%B8%E7%94%A8%E6%80%BB%E7%BB%93/ \
[7] https://n3xtchen.github.io/n3xtchen/elasticsearch/2017/07/05/elasticsearch-23-useful-query-example/ \
[8] https://www.elastic.co/cn/blog/a-practical-introduction-to-elasticsearch

---

[返回目錄](./../README.md)

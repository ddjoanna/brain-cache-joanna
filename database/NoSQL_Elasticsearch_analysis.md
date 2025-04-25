# 常見的 ElasticSearch 中文分詞插件

> ElasticSearch（ES）的分詞插件主要用於將輸入的文字拆分成詞條，以利建立索引和搜尋。由於 ES 預設的分詞器對中文支援有限，因此常透過安裝第三方中文分詞插件來提升中文文本的搜尋效果。

## IK 分詞插件（analysis-ik）

- **介紹**：IK 分詞插件是基於詞典的中文分詞工具，採用“正向迭代最細粒度切分算法”，支援兩種分詞模式：
  - **ik_max_word**：最細粒度拆分，會將詞語拆分成盡可能多的組合，適合建立索引時使用，能覆蓋更多可能的搜尋詞。
  - **ik_smart**：較粗粒度拆分，分詞結果較簡潔，適合搜尋時提高精準度。
- **特性**：
  - 支援英文字母、數字、中文詞彙分詞，兼容韓文、日文字符。
  - 支援用戶自定義詞庫，能透過更新詞典改善分詞效果。
  - 有動態熱更新詞庫的功能（部分平台支援如阿里雲 OSS 動態加載詞典）。
- **安裝與使用**：將 IK 插件放入 ES 的 plugins 目錄，重啟 ES 即可使用。
- **應用**：廣泛用於中文全文檢索、日誌分析、電商商品搜索等場景。
- **優點**：分詞細膩，詞庫豐富且可自定義，兼容多語言。
- **缺點**：細粒度分詞可能導致索引膨脹，需依需求調整分詞模式。

## AliNLP 分詞插件（analysis-aliws）

- **介紹**：阿里雲 ElasticSearch 內建的系統插件，集成了 AliNLP 的中文分詞能力。
- **特性**：
  - 提供分析器（aliws）和分詞器（aliws_tokenizer），不會截取虛詞和符號。
  - 支援詞庫熱更新，方便動態調整分詞詞典。
- **應用**：適合需要阿里雲生態整合、且對虛詞處理有特殊需求的用戶。
- **優點**：系統集成度高，詞庫可熱更新，對中文語義理解較好。
- **缺點**：依賴阿里雲環境，彈性較一般開源插件低。

## ElasticSearch 內置分詞器

- **介紹**：ES 自帶多種分詞器，如 standard（標準分詞器）、simple（簡單分詞器）、whitespace（空白分詞器）、keyword（關鍵字分詞器）等。
- **特性**：這些分詞器對英文效果較好，但對中文分詞支援有限，通常無法有效拆分中文詞語。
- **應用**：適合英文或結構化文本，中文場景一般需搭配第三方插件。

---

## 分詞插件的作用與重要性

- **分詞器**將輸入的文本拆分成最小的詞條（token），這些詞條是 ES 建立索引和搜尋的基本單位。
- 中文文本無明顯空格分隔詞語，分詞器的好壞直接影響搜尋的精準度和召回率。
- 不同分詞器對同一文本的拆分結果差異很大，影響搜尋結果的覆蓋範圍和準確性。

---

## 總結

ElasticSearch 中文分詞插件中，IK 分詞器是最常用且功能強大的開源方案，提供細粒度和粗粒度兩種模式，並支持詞庫自定義和熱更新，適合多數中文搜尋場景。阿里雲的 AliNLP 分詞插件則集成了更高階的語義分析能力，適合阿里雲用戶。ES 內置分詞器對中文支援有限，通常需搭配第三方插件使用以提升中文搜尋體驗。

以上分詞插件的選擇與配置，需根據具體業務需求、資料特性及搜尋精度要求來決定。

---

**參考來源:**

[1] https://www.alibabacloud.com/help/zh/es/user-guide/use-the-analysis-ik-plug-in \
[2] https://help.aliyun.com/zh/es/user-guide/use-the-analysis-aliws-plug-in \
[3] https://blog.csdn.net/qq_43646524/article/details/139420773 \
[4] http://www.javaboy.org/2020/1126/es-analyzer.html \
[5] https://blog.csdn.net/zxd1435513775/article/details/127870981 \
[6] https://github.com/YVictor13/ElasticSearch-study/blob/master/src/Elasticsearch%20%20%E5%88%86%E8%AF%8D%E5%99%A8.md \
[7] https://www.cnblogs.com/booksea/p/17615360.html \
[8] https://cloud.tencent.com/document/product/845/46266

---

[返回目錄](./../README.md)

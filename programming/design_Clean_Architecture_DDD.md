# Clean Architecture vs Domain-Driven Design

Clean Architecture 與領域驅動設計（Domain-Driven Design, DDD）兩者常被一同提及，但本質與焦點有所不同，且兩者可以互補使用。

## 差異說明

| 項目                 | Clean Architecture                                                                                                     | 領域驅動設計（DDD）                                                                                                       |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **核心概念**         | 一種軟體架構設計模式，強調系統分層與依賴反轉，讓業務邏輯與外部細節（UI、資料庫等）解耦，確保系統易於維護與測試。       | 一套以業務領域為核心的軟體開發方法論，強調深入理解業務、建模複雜領域、使用統一語言（Ubiquitous Language）與戰術設計模式。 |
| **關注點**           | 系統架構的分層與依賴方向，確保業務邏輯獨立且不受外部變化影響。                                                         | 領域模型的建模與設計，聚焦於業務知識與邏輯的準確表達與演進。                                                              |
| **層級結構**         | 明確分為 Entities（實體）、Use Cases（用例）、Interface Adapters（介面轉換）、Frameworks & Drivers（框架與驅動）四層。 | 聚焦於 Domain Layer（領域層），包含 Entities、Value Objects、Aggregates、Repositories 等戰術設計元素。                    |
| **業務邏輯實現**     | 業務邏輯主要在 Entities 與 Use Cases 層實現。                                                                          | 業務邏輯集中在 Domain Model（領域模型）中，強調模型的豐富行為與規則。                                                     |
| **與外部系統的關係** | 透過依賴反轉與介面，將外部系統（資料庫、UI、第三方服務）隔離在外層。                                                   | 透過 Hexagonal Architecture（六角形架構）等模式，強調與外部系統的「Port」與「Adapter」分離，保持領域核心純淨。            |
| **實作關係**         | 可以視為一種架構骨架，DDD 的戰術設計（如 Entities、Repositories）可用於實現 Clean Architecture 中的內層。              | DDD 提供具體的建模工具與設計模式，幫助實現 Clean Architecture 內部的業務層。                                              |

## 互補關係

- Clean Architecture 提供系統分層與依賴規則的架構框架，DDD 則提供領域模型的設計方法與戰術模式，兩者結合能更有效地組織代碼與業務邏輯。
- 在 Clean Architecture 中，DDD 的 Entities 與 Use Cases 對應 Domain Layer 與 Application Layer，DDD 的 Repository 模式可實作 Clean Architecture 的 Gateway 介面。
- DDD 使業務層代碼更能反映業務語言與規則，避免業務邏輯散落在架構層級中，提升語意清晰度與可維護性[1][2][3]。

## 簡要總結

- **Clean Architecture** 是架構設計原則，強調層次分離與依賴反轉。
- **DDD** 是領域建模方法，強調業務知識的抽象與實踐。
- DDD 的戰術設計填補了 Clean Architecture 內部業務層的實作細節，使架構更貼近業務需求。
- 兩者結合能打造結構清晰、業務豐富且易於維護的軟體系統。

此差異與結合方式在實務中被廣泛討論與應用，且有豐富的實例與經驗分享[1][3][7]。

---

**參考來源:**

[1] https://www.youtube.com/watch?v=AiQgpOXk2kk \
[2] https://mileschou.me/blog/ddd-and-ca-started-day-2/ \
[3] https://ithelp.ithome.com.tw/articles/10222311 \
[4] https://teddy-chen-tw.blogspot.com/2019/10/ddd.html \
[5] http://gelis-dotnet.blogspot.com/2021/01/ddd.html \
[6] https://teddy-chen-tw.blogspot.com/2020/08/10repository.html \
[7] http://gelis-dotnet.blogspot.com/2020/12/ddd-clean-architecture.html \
[8] https://www.cnblogs.com/helios-fz/p/15632243.html

---

[返回目錄](./../README.md)

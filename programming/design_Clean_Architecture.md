# Clean Architecture

> Clean Architecture 是由 Robert C. Martin（Uncle Bob）提出的一種軟體設計架構，目標是創建一個易於維護、擴展且不依賴特定框架的系統，核心理念是讓系統中的商業邏輯（業務規則）獨立於外部細節（如資料庫、UI、框架等）[1][4][5]。

## 說明

Clean Architecture 將系統分為多個同心環狀層級，通常包括以下四層：

- **Entities（實體層）**：定義核心業務邏輯與規則，純粹的業務物件，與外部框架或資料庫無關。
- **Use Cases（用例層）**：實現應用程式邏輯，協調 Entities 執行特定業務流程。
- **Interface Adapters（介面轉換層）**：負責將資料從外部格式轉換成內部格式，反之亦然，如 DTO（資料傳輸物件）。
- **Frameworks & Drivers（框架與驅動層）**：包含 UI、資料庫、外部服務等具體實作細節。

層級之間的依賴只能由外層指向內層，內層不得依賴外層，且資料格式也應該分離[2][3][4]。

## 特性

- **依賴規則（Dependency Rule）**：依賴方向由外向內，內層不依賴外層。
- **邊界隔離（Boundaries）**：每層有明確責任，透過接口隔離內外層。
- **獨立性**：不依賴特定框架、資料庫、UI 或外部服務，方便替換與測試。
- **可測試性**：業務邏輯可在無 UI、資料庫環境下獨立測試。
- **分層原則**：層級清晰，防止跨層直接依賴。
- **依賴反轉原則（Dependency Inversion Principle）**：透過介面反轉依賴，維持依賴方向正確[1][3][4][5]。

## 應用場景

- 複雜業務系統，需長期維護與擴展。
- 需要高可測試性與低耦合度的系統。
- 希望系統能夠靈活替換 UI、資料庫或第三方服務。
- 團隊規模較大，需明確分工與層次分離。

## 優缺點

| 優點                         | 缺點                                         |
| ---------------------------- | -------------------------------------------- |
| 業務邏輯獨立，易於維護與擴展 | 實作複雜，初期開發成本較高                   |
| 高可測試性，方便單元測試     | 層級間資料轉換與介面設計較繁瑣               |
| 易於替換外部框架與技術       | 過度嚴格可能導致開發效率下降                 |
| 促進良好架構設計與分層責任   | 部分物件放置層級有灰色地帶，實作上有彈性空間 |

總結來說，Clean Architecture 強調系統內部業務邏輯的純淨與獨立，通過嚴格的分層與依賴反轉原則，降低系統耦合度，提升可維護性與可測試性，但實踐時需要在潔癖與實用性間取得平衡[1][3][4][5]。

**參考來源:**

[1] https://ithelp.ithome.com.tw/articles/10335570 \
[2] https://www.techtarget.com/whatis/definition/clean-architecture \
[3] https://teddy-chen-tw.blogspot.com/2020/08/clean-architecture.html \
[4] https://hackmd.io/@fz000530/HyXzjCkDkx \
[5] https://pjchender.github.io/golang/note-go-clean-architecture/ \
[6] https://teddy-chen-tw.blogspot.com/2018/07/clean-architecture4.html \
[7] https://blog.jaggerwang.net/clean-architecture-best-practices/

---

[返回目錄](./../README.md)

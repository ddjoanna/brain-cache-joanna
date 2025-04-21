# SOLID 設計模式

> SOLID 是五個物件導向設計原則的縮寫，幫助開發者寫出更易維護、擴展且高內聚低耦合的程式碼。以下說明每個原則並附上 PHP 範例：

---

## 單一職責原則 (Single Responsibility Principle, SRP)

**定義**：一個類別應該只有一個改變的理由，也就是專注於單一職責。  
**範例**：

```php
// 負責使用者資料處理
class User {
    private $name;
    public function __construct($name) {
        $this->name = $name;
    }
    public function getName() {
        return $this->name;
    }
}

// 負責使用者資料儲存
class UserRepository {
    public function save(User $user) {
        // 儲存使用者資料到資料庫
    }
}
```

使用者資料處理與儲存分離，符合單一職責[1]。

---

## 開放封閉原則 (Open-Closed Principle, OCP)

**定義**：軟體實體（類別、函式等）應該對擴展開放，對修改封閉。  
**範例**：

```php
interface Shape {
    public function area();
}

class Rectangle implements Shape {
    public function __construct(private $width, private $height) {}
    public function area() {
        return $this->width * $this->height;
    }
}

class Circle implements Shape {
    public function __construct(private $radius) {}
    public function area() {
        return pi() * pow($this->radius, 2);
    }
}

function calculateArea(Shape $shape) {
    return $shape->area();
}
```

新增新形狀只需新增類別，不用修改既有程式碼[1][2]。

---

## 里氏替換原則 (Liskov Substitution Principle, LSP)

**定義**：子類別必須能替換父類別，且行為不變。  
**範例**：

```php
class Bird {
    public function fly() {
        // 飛行邏輯
    }
}

class Sparrow extends Bird {
    // 可以飛行，符合替換原則
}

class Ostrich extends Bird {
    public function fly() {
        throw new Exception("Ostrich can't fly");
    }
}
```

此例 Ostrich 不應繼承 Bird，因為無法實現 fly 方法，違反 LSP[6]。正確做法是重新設計繼承結構。

---

## 介面隔離原則 (Interface Segregation Principle, ISP)

**定義**：客戶端不應被迫依賴它不使用的方法，應拆分成多個專一介面。  
**範例**：

```php
interface FileStorage {
    public function storeFile(string $name);
    public function getFile(string $name);
}

interface ServerManagement {
    public function createServer(string $region);
    public function listServer(string $region);
}

class AmazonWebServices implements FileStorage, ServerManagement {
    public function storeFile(string $name) { /*...*/ }
    public function getFile(string $name) { /*...*/ }
    public function createServer(string $region) { /*...*/ }
    public function listServer(string $region) { /*...*/ }
}

class SomeNewCloudService implements FileStorage {
    public function storeFile(string $name) { /*...*/ }
    public function getFile(string $name) { /*...*/ }
    // 不實作 ServerManagement 介面，避免空方法
}
```

避免龐大介面強迫實作未使用方法[4][7]。

---

## 依賴反轉原則 (Dependency Inversion Principle, DIP)

**定義**：高層模組不應依賴低層模組，兩者都應依賴抽象；抽象不應依賴細節，細節應依賴抽象。  
**範例**：

```php
interface Database {
    public function save($data);
}

class MySQLDatabase implements Database {
    public function save($data) {
        // 實作儲存資料
    }
}

class User {
    private $database;
    public function __construct(Database $database) {
        $this->database = $database;
    }
    public function save() {
        $this->database->save($this);
    }
}
```

User 類別依賴 Database 抽象介面，而非具體 MySQLDatabase，方便替換[1][5]。

---

這五個原則合稱 SOLID，是物件導向設計的基石，能有效提升 PHP 程式碼的可維護性與擴展性。

---

**參考來源:**

[1] https://kamadiam.com/solid-principles-in-php/ \
[2] https://docfunc.com/posts/55/%E7%94%A8-php-%E8%A7%A3%E9%87%8B-solid-%E5%8E%9F%E5%89%87%E8%A3%A1%E7%9A%84-o-post \
[3] https://vocus.cc/article/62b3f00afd89780001f46964 \
[4] https://docfunc.com/posts/60/%E7%94%A8-php-%E7%B0%A1%E5%96%AE%E4%BB%8B%E7%B4%B9-solid-%E5%8E%9F%E5%89%87%E8%A3%A1%E9%9D%A2%E7%9A%84-i-post \
[5] https://ithelp.ithome.com.tw/articles/10326238 \
[6] https://github.com/wataridori/solid-php-example \
[7] https://ithelp.ithome.com.tw/m/articles/10192464 \
[8] https://blog.csdn.net/gitblog_00049/article/details/139109743

---

[返回目錄](./../README.md)

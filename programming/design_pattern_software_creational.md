# 軟體設計模式中的創建型模式說明

> 創建型模式（Creational Patterns）專注於對象的創建過程，目的是將對象的實例化細節從使用者代碼中分離，提升系統的靈活性和可維護性。這類模式隱藏了具體類的實例創建方式，讓系統可以根據需求靈活地創建對象。

## 創建型模式的主要類型與典型應用場景

| 設計模式                                 | 典型應用場景                                               | 說明                                                            |
| ---------------------------------------- | ---------------------------------------------------------- | --------------------------------------------------------------- |
| **單例模式 (Singleton)**                 | 需要確保一個類只有一個實例，且該實例可被全局訪問。         | 例如：配置管理器、日誌記錄器、資料庫連線池。                    |
| **工廠方法模式 (Factory Method)**        | 當類的實例化推遲到子類實現，且系統需要依賴抽象而非具體類。 | 例如：不同資料庫驅動的連線工廠，不同日誌系統的建立。            |
| **抽象工廠模式 (Abstract Factory)**      | 需要創建一系列相關或相依的對象，且不想指定具體類。         | 例如：跨平台 GUI 元件庫，根據系統環境創建不同風格的按鈕與視窗。 |
| **建造者模式 (Builder)**                 | 創建複雜對象，且希望將對象的建造過程與表示分離。           | 例如：生成複雜的報表、組合複雜的產品訂單。                      |
| **原型模式 (Prototype)**                 | 需要通過複製現有實例來創建新對象，避免昂貴的實例化過程。   | 例如：複製大量相似物件，遊戲角色快速生成。                      |
| **延遲初始化模式 (Lazy Initialization)** | 對象的創建或某些計算推遲到第一次使用時進行。               | 例如：延遲載入大型配置或資源。                                  |

---

## PHP 實作範例說明

### 1. 單例模式 (Singleton)

確保類別只有一個實例，並提供全局訪問點。

```php
class Singleton {
    private static ?Singleton $instance = null;

    private function __construct() {
        // 私有建構子防止外部實例化
    }

    public static function getInstance(): Singleton {
        if (self::$instance === null) {
            self::$instance = new Singleton();
        }
        return self::$instance;
    }

    public function doSomething() {
        echo "Singleton instance method called.\n";
    }
}

// 使用範例
$instance = Singleton::getInstance();
$instance->doSomething();
```

---

### 2. 工廠方法模式 (Factory Method)

定義一個建立對象的接口，讓子類決定實例化哪個類。

```php
interface Logger {
    public function log(string $message);
}

class FileLogger implements Logger {
    public function log(string $message) {
        echo "Logging to a file: $message\n";
    }
}

class DatabaseLogger implements Logger {
    public function log(string $message) {
        echo "Logging to a database: $message\n";
    }
}

abstract class LoggerFactory {
    abstract public function createLogger(): Logger;

    public function logMessage(string $message) {
        $logger = $this->createLogger();
        $logger->log($message);
    }
}

class FileLoggerFactory extends LoggerFactory {
    public function createLogger(): Logger {
        return new FileLogger();
    }
}

class DatabaseLoggerFactory extends LoggerFactory {
    public function createLogger(): Logger {
        return new DatabaseLogger();
    }
}

// 使用範例
$factory = new FileLoggerFactory();
$factory->logMessage("This is a log message.");
```

---

### 3. 抽象工廠模式 (Abstract Factory)

提供一個介面，創建一系列相關或相依的對象。

```php
interface Button {
    public function paint();
}

class WinButton implements Button {
    public function paint() {
        echo "Render a button in Windows style.\n";
    }
}

class MacButton implements Button {
    public function paint() {
        echo "Render a button in Mac style.\n";
    }
}

interface GUIFactory {
    public function createButton(): Button;
}

class WinFactory implements GUIFactory {
    public function createButton(): Button {
        return new WinButton();
    }
}

class MacFactory implements GUIFactory {
    public function createButton(): Button {
        return new MacButton();
    }
}

// 使用範例
function clientCode(GUIFactory $factory) {
    $button = $factory->createButton();
    $button->paint();
}

clientCode(new WinFactory());
clientCode(new MacFactory());
```

---

### 4. 建造者模式 (Builder)

將複雜對象的建造過程與表示分離。

```php
class Product {
    private array $parts = [];

    public function add(string $part) {
        $this->parts[] = $part;
    }

    public function show() {
        echo "Product parts: " . implode(', ', $this->parts) . "\n";
    }
}

interface Builder {
    public function buildPartA();
    public function buildPartB();
    public function getResult(): Product;
}

class ConcreteBuilder implements Builder {
    private Product $product;

    public function __construct() {
        $this->product = new Product();
    }

    public function buildPartA() {
        $this->product->add("PartA");
    }

    public function buildPartB() {
        $this->product->add("PartB");
    }

    public function getResult(): Product {
        return $this->product;
    }
}

class Director {
    private Builder $builder;

    public function __construct(Builder $builder) {
        $this->builder = $builder;
    }

    public function construct() {
        $this->builder->buildPartA();
        $this->builder->buildPartB();
    }
}

// 使用範例
$builder = new ConcreteBuilder();
$director = new Director($builder);
$director->construct();
$product = $builder->getResult();
$product->show();
```

---

### 5. 原型模式 (Prototype)

通過複製現有對象創建新對象。

```php
class Prototype {
    public string $field;

    public function __clone() {
        // 可在此實作深拷貝邏輯
    }
}

// 使用範例
$original = new Prototype();
$original->field = "Original";

$clone = clone $original;
$clone->field = "Clone";

echo $original->field . "\n"; // Original
echo $clone->field . "\n";    // Clone
```

---

## 總結

創建型設計模式透過封裝對象創建的細節，提高系統靈活性與可維護性。根據不同需求，選擇適合的模式能有效解決對象創建的複雜度和耦合問題。

---

**參考來源:**

[1] https://blog.sunlan.me/2023/02/18/%E6%B5%85%E8%B0%88%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%C2%B7%E9%A9%BE%E9%A9%AD%E5%8F%98%E5%8C%96%E4%B9%8B%E9%81%93%EF%BC%88%E5%88%9B%E5%BB%BA%E5%9E%8B%E6%A8%A1%E5%BC%8F%E7%AF%87%EF%BC%89/ \
[2] https://blog.csdn.net/zengchenAAA/article/details/137938449 \
[3] https://zh.wikipedia.org/zh-hant/%E5%89%B5%E5%BB%BA%E5%9E%8B%E6%A8%A1%E5%BC%8F \
[4] https://design-patterns.readthedocs.io/zh_CN/latest/creational_patterns/creational.html \
[5] https://ithelp.ithome.com.tw/articles/10209153 \
[6] http://www.runoob.com/design-pattern/design-pattern-intro.html \
[7] https://blog.csdn.net/qq_45110186/article/details/136295939 \
[8] https://www.cnblogs.com/aalan/p/16988376.html

---

[返回目錄](./../README.md)

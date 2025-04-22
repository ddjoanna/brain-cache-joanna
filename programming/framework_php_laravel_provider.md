# Laravel 12 服務提供者

## register 與 boot 的差異

Laravel 的服務提供者（Service Provider）主要有兩個方法：`register()` 和 `boot()`，它們的差異在於執行時機與用途。

| 項目             | register()                           | boot()                                             |
| ---------------- | ------------------------------------ | -------------------------------------------------- |
| 執行時機         | 在所有服務提供者註冊之前執行         | 在所有服務提供者註冊完成後執行                     |
| 主要用途         | 將服務綁定（bind）到服務容器         | 執行依賴已註冊服務的初始化邏輯，如事件監聽、路由等 |
| 可否使用其他服務 | 不行，因為其他服務可能尚未註冊       | 可以，因為所有服務都已註冊完成                     |
| 典型操作         | 綁定接口與實作、註冊單例、註冊服務等 | 註冊事件監聽器、路由、Blade 指令、視圖組合器等     |

簡單來說，`register()` 只做「註冊綁定」，不執行任何依賴其他服務的邏輯；`boot()` 則是「啟動階段」，可以安全使用其他已註冊服務，執行初始化工作[1][2][5][6][7][8]。

---

## bind 與 singleton 的使用情境差異

Laravel 服務容器提供兩種主要綁定方式：

| 方法        | 說明                               | 使用情境範例                                             |
| ----------- | ---------------------------------- | -------------------------------------------------------- |
| `bind`      | 每次解析都會建立新的實例           | 需要每次使用都產生新物件，例如建立多個不同狀態的服務實例 |
| `singleton` | 只建立一次實例，後續皆回傳同一物件 | 需要全應用共用同一物件，例如資料庫連接、設定物件等       |

例如：

```php
// bind 綁定，每次呼叫都會 new 新物件
$this->app->bind('App\Services\FooService', function ($app) {
    return new \App\Services\FooService();
});

// singleton 綁定，第一次呼叫建立物件，之後共用
$this->app->singleton('App\Services\BarService', function ($app) {
    return new \App\Services\BarService();
});
```

---

## 典型的 Laravel Provider 範例說明

假設我們要建立一個自訂服務提供者 `App\Providers\ExampleServiceProvider`，用來註冊一個簡單的服務 `ExampleService`。

```php
namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use App\Services\ExampleService;

class ExampleServiceProvider extends ServiceProvider
{
    // 註冊服務綁定
    public function register()
    {
        // 將 ExampleService 綁定為 singleton
        $this->app->singleton(ExampleService::class, function ($app) {
            // 假設 ExampleService 需要讀取 config 的設定
            $config = $app['config']->get('example');
            return new ExampleService($config);
        });
    }

    // 啟動階段，註冊事件或初始化
    public function boot()
    {
        // 註冊一個事件監聽器
        \Event::listen('example.event', function ($payload) {
            // 處理事件
        });

        // 也可以註冊 Blade 指令、路由等
    }
}
```

### 使用步驟

1. 在 `config/app.php` 的 `providers` 陣列加入：

```php
App\Providers\ExampleServiceProvider::class,
```

2. 在需要使用 `ExampleService` 的地方，透過依賴注入取得：

```php
use App\Services\ExampleService;

class SomeController extends Controller
{
    protected $example;

    public function __construct(ExampleService $example)
    {
        $this->example = $example;
    }

    public function index()
    {
        // 使用 $this->example
    }
}
```

---

## 總結

- **register()**：只做服務綁定，不可使用其他尚未註冊的服務，適合放置 `bind()`、`singleton()` 等綁定邏輯。
- **boot()**：所有服務註冊完成後執行，可安全使用其他服務，適合註冊事件、路由、Blade 指令等初始化行為。
- **bind()**：每次解析都會產生新物件，適用於需要多個獨立實例的服務。
- **singleton()**：只產生一次物件，後續共用同一實例，適用於共用連接或設定物件。

這樣的設計讓 Laravel 的服務註冊與啟動流程清晰且模組化，有助於維護與擴展[1][2][3][5][6][7][8]。

---

**參考來源:**

[1] https://www.cnblogs.com/hanyouchun/p/5504315.html
[2] https://dev.tldrlss.com/article/2024/11/laravel-service-provider-register-boot-intro/
[3] https://old-oomusou.goodjack.tw/laravel/laravel-service-provider/
[4] https://blog.csdn.net/qq_38989173/article/details/124174668
[5] https://dev.tldrlss.com/zh-cn/article/2024/11/laravel-service-provider-register-boot-intro/
[6] https://masteringlaravel.io/daily/2024-01-09-what-is-the-difference-between-boot-and-register-in-service-providers
[7] https://stackoverflow.com/questions/49782349/difference-between-boot-and-register-method-of-app-service-provider-class-in-lar
[8] https://cloud.tencent.com/developer/article/1586253

---

[返回目錄](./../README.md)

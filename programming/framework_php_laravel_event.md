# Laravel 12 事件系統詳細說明

> Laravel 的事件系統基於觀察者模式，允許你定義「事件」（Event）來表示應用中發生的特定行為或狀態變化，並用「監聽器」（Listener）來響應這些事件。這種設計能有效解耦應用邏輯，提升可維護性與可擴展性[1][3][5]。

## 事件的定義

事件通常是 PHP 物件，放置於 `app/Events` 目錄。事件類別通常會使用 `Dispatchable` 和 `SerializesModels` trait，方便事件的觸發與序列化[1][5]。

## 監聽器的定義

監聽器是負責處理事件的類別，放置於 `app/Listeners` 目錄，必須實作 `handle` 方法，接收事件物件並執行相應邏輯。監聽器可以同步執行，也可以透過實作 `ShouldQueue` 介面，將事件處理放入隊列非同步執行[1][3][5]。

## 事件與監聽器的註冊

事件與監聽器的關聯通常在 `app/Providers/EventServiceProvider.php` 的 `$listen` 陣列中註冊[1][5]。

## 事件觸發

事件可以透過 `event()` 輕鬆觸發，通常在應用程式的特定邏輯點，例如用戶註冊後[1][5]。

---

## 典型應用：用戶註冊後發送歡迎郵件完整範例

### Step 1：建立事件類別 `UserRegistered`

```php
namespace App\Events;

use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;
use App\Models\User;

class UserRegistered
{
    use Dispatchable, SerializesModels;

    public $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }
}
```

### Step 2：建立監聽器 `SendWelcomeEmail`

```php
namespace App\Listeners;

use App\Events\UserRegistered;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Support\Facades\Mail;
use App\Mail\WelcomeMail;

class SendWelcomeEmail implements ShouldQueue
{
    public function handle(UserRegistered $event)
    {
        Mail::to($event->user->email)->send(new WelcomeMail($event->user));
    }
}

```

### Step 3：建立郵件類別 `WelcomeMail`

```php
namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;
use App\Models\User;

class WelcomeMail extends Mailable
{
    use Queueable, SerializesModels;

    public $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function build()
    {
        return $this->subject('歡迎加入我們的網站')
                    ->markdown('emails.welcome');
    }
}
```

### Step 4：建立郵件視圖 `resources/views/emails/welcome.blade.php`

```blade
@component('mail::message')
# 歡迎 {{ $user->name }}

感謝您註冊我們的網站！

祝您使用愉快。

@endcomponent
```

### Step 5：EventServiceProvider 註冊事件與監聽器

`app/Providers/EventServiceProvider.php`

```php
namespace App\Providers;

use Illuminate\Foundation\Support\Providers\EventServiceProvider as ServiceProvider;
use App\Events\UserRegistered;
use App\Listeners\SendWelcomeEmail;

class EventServiceProvider extends ServiceProvider
{
    protected $listen = [
        UserRegistered::class => [
            SendWelcomeEmail::class,
        ],
    ];

    public function boot()
    {
        parent::boot();
    }
}
```

### Step 6：觸發事件範例（通常在註冊控制器）

```php
use App\Events\UserRegistered;
use App\Models\User;
use Illuminate\Http\Request;

class RegisterController extends Controller
{
    public function register(Request $request)
    {
        // 驗證與建立用戶
        $user = User::create([
            'name' => $request->name,
            'email' => $request->email,
            'password' => bcrypt($request->password),
        ]);

        // 觸發註冊事件
        event(new UserRegistered($user));

        // 其他註冊後邏輯
        return redirect()->route('home')->with('success', '註冊成功，歡迎郵件已發送！');
    }
}
```

---

## 補充說明

- **事件隊列**：監聽器實作 `ShouldQueue` 後，事件處理會放入隊列，避免阻塞請求。
- **事件廣播**：Laravel 支援事件廣播功能，可用於即時通知。
- **事件序列化**：事件類別使用 `SerializesModels` trait，方便事件在隊列中序列化與反序列化。

---

## 總結

Laravel 12 的事件系統是一種強大的機制，讓你能夠將應用程式的行為封裝成事件，並在適當時機觸發這些事件。這不僅有助於解耦應用邏輯，還提高了應用程式的可維護性與可擴展性。以上範例展示了如何利用事件系統，在用戶註冊後自動發送歡迎郵件，符合 Laravel 12 的標準實作方式，並兼顧同步與非同步處理。

---

**參考來源:**

[1] https://blog.csdn.net/2402_85762143/article/details/140232587 \
[2] https://laravel.dev.org.tw/docs/12.x/configuration \
[3] https://m.php.cn/zh-tw/faq/406078.html \
[4] https://laravel.dev.org.tw/docs/12.x/authentication \
[5] https://learnku.com/docs/laravel-kernel/event-driven-programming/6936 \
[6] https://docs.laravel-dojo.com/laravel/12.0/facades \
[7] https://docs.laravel-dojo.com/laravel/12.0/testing \
[8] https://yeeinhole.github.io/2020/04/25/laravel-1/

---

[返回目錄](./../README.md)

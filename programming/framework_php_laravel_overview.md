# Laravel 5 到 Laravel 12 重大演進與 HTTP 請求生命週期詳細說明

---

## 一、Laravel 12 核心元件概述

Laravel 12 延續 Laravel 框架簡潔、高效與現代化的設計理念，核心元件包括：

- **MVC 架構**  
  分離 Model（資料）、View（視圖）與 Controller（控制器），提升代碼組織與維護性。

- **路由系統**  
  管理 URL 與請求對應的控制器或閉包函式。

- **Blade 模板引擎**  
  簡潔且強大的模板語法，支援繼承與元件化。

- **Eloquent ORM**  
  物件關聯映射，簡化資料庫操作。

- **中介層（Middleware）**  
  攔截並處理 HTTP 請求與回應，如驗證、CSRF 防護等。

- **服務提供者（Service Providers）**  
  註冊與啟動應用服務，是框架啟動的核心。

- **Artisan CLI**  
  命令列工具，支持自動化任務。

- **設定與環境管理**  
  集中管理多環境設定。

- **測試與除錯工具**  
  提升代碼品質與錯誤追蹤。

- **現代前端整合**  
  支援 Vite、Tailwind CSS、React、Vue、Livewire 等。

---

## 二、Laravel 12 HTTP 請求生命週期詳細說明

Laravel 12 的 HTTP 請求生命週期描述從請求進入框架到回應送出整個流程，並因架構調整，請求核心管理已從傳統的 `app/Http/Kernel.php` 移轉至 `bootstrap/app.php`。

### 1. 請求進入入口檔案

- 使用者在瀏覽器發起 HTTP 請求，Web 伺服器（Apache、Nginx）將請求導向 `public/index.php`。
- `index.php` 載入 Composer 自動加載器，並從 `bootstrap/app.php` 取得 Laravel 應用實例，完成初始化。

### 2. HTTP Kernel 及中介層管理（改由 bootstrap/app.php）

- Laravel 12 不再使用 `app/Http/Kernel.php`，改為在 `bootstrap/app.php` 中集中管理中介層。
- 透過 `withMiddleware` 方法註冊全域中介層與中介層群組（如 `web`、`api`），處理 Session、CSRF、認證等橫切關注點。

```php
->withMiddleware(function (Middleware $middleware) {
    $middleware->append(\App\Http\Middleware\EnsureTokenIsValid::class);
    $middleware->web(append: [
        \App\Http\Middleware\EnsureUserIsSubscribed::class,
    ]);
    $middleware->api(prepend: [
        \App\Http\Middleware\EnsureTokenIsValid::class,
    ]);
});
```

### 3. 服務提供者註冊與啟動

- 服務提供者在啟動階段被註冊，載入資料庫、事件、認證等服務。

### 4. 路由匹配與控制器執行

- 請求經過中介層後，路由系統根據路由規則將請求導向對應控制器或閉包函式。
- 控制器執行業務邏輯，可能與 Eloquent ORM 互動。

### 5. 產生回應

- 控制器將資料傳遞給視圖（Blade 模板）或直接產生 JSON 等格式的回應。

### 6. 回應經過終極中介層處理

- 回應經過最後的中介層處理，如設定 HTTP 標頭、壓縮等。

### 7. 回應送回用戶端

- HTTP Kernel 將回應送回瀏覽器，完成請求-回應循環。

### 8. 請求結束與資源釋放

- Laravel 釋放資源，完成請求生命週期。

---

## 三、Laravel 5 到 Laravel 12 重大演進整理

| 版本範圍            | 重大演進與變化                                                                                                                                                                                        |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Laravel 5.x**     | - 目錄結構調整（Commands → Jobs，Handlers → Listeners）。- 路由篩選器改為 Middleware。- 服務容器與事件系統增強。- Eloquent ORM 優化。                                                                 |
| **Laravel 6 ~ 8**   | - 支援 Serverless（Laravel Vapor）。- 任務排程與隊列系統強化。- API Resources 與認證系統（Passport、Sanctum）完善。- Blade 與前端工具整合。                                                           |
| **Laravel 9**       | - PHP 8.0 起步，利用新語法與性能優化。- 引入功能旗標套件 Pennant。- 驗證規則支援 `__invoke()`。- 核心元件重構，模型 Casts 改為方法。                                                                  |
| **Laravel 10 ~ 11** | - PHP 8.2+ 支援。- 推出 React、Vue、Livewire 入門套件，整合 Inertia.js、Tailwind CSS。- 身份驗證強化，加入 WorkOS AuthKit。- 框架維護與依賴更新。                                                     |
| **Laravel 12**      | - 延續 Laravel 11 改進，依賴 Symfony 6.2+，PHP 8.2-8.4 支援。- 新增 React、Vue、Livewire 入門套件，整合 Shadcn UI、Flux UI。- WorkOS AuthKit 擴充身份驗證方案。- 核心架構調整，提升維護性與開發體驗。 |

---

## 四、重要技術與架構演進細節

- **目錄結構調整與中介層引入**  
  Laravel 5 引入 Middleware 取代路由篩選器，提升請求攔截彈性，並調整命名與目錄結構。

- **HTTP Kernel 架構調整**  
  Laravel 11 起，`app/Http/Kernel.php` 被移除，改由 `bootstrap/app.php` 管理中介層設定，架構更集中且現代化。

- **PHP 版本升級**  
  Laravel 9 起要求 PHP 8.0，Laravel 12 支援 PHP 8.2-8.4，利用現代 PHP 語法與型別系統提升性能與安全。

- **功能旗標與漸進式發布**  
  Laravel 9 的 Pennant 套件支援功能開關與 A/B 測試。

- **身份驗證系統強化**  
  Laravel 12 引入 WorkOS AuthKit，支援社交登入、SSO、通行密鑰等企業級身份驗證方案。

- **前端生態整合**  
  Laravel 11/12 推出多種入門套件，整合 React、Vue、Livewire、Inertia.js、Tailwind CSS、Shadcn UI、Flux UI，提升開發效率。

- **核心元件重構**  
  Laravel 9+ 重構 HTTP Kernel、模型 Casts 及其他核心元件，提升類型安全與維護性。

- **維護與依賴更新**  
  Laravel 12 以穩定性與依賴現代化為主，降低破壞性改動，方便升級。

---

**參考來源:**

[1] https://laravel.com/docs/12.x \
[2] https://laravel.com/docs/9.x \
[3] https://laravel.com/docs/8.x \
[4] https://github.com/laravel/laravel \
[5] https://laravel-news.com/ \
[6] https://laracasts.com/discuss \
[7] https://www.php.net/ \
[8] https://symfony.com/

---

[返回目錄](./../README.md)

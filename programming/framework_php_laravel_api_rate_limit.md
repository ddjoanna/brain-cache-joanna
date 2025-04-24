## Laravel API Rate Limit

> 用於控制 API 請求流量的機制，能有效防止濫用、維持系統效能、確保資源公平分配。以下將說明其主要應用場景與實作方式。

---

**常見應用場景**

- 防止惡意攻擊  
  限制單一來源（如 IP 或用戶）在短時間內的請求次數，可有效防止 DoS（Denial of Service）攻擊、暴力破解等惡意行為[5][6][7]。

- 維持系統穩定與效能  
  當 API 服務面對大量流量時，Rate Limiting 可避免伺服器過載，確保所有用戶都能獲得穩定的響應[5][6][7]。

- 資源公平分配  
  避免個別用戶或應用耗盡系統資源，確保多用戶或多應用場景下的公平競爭[5][6][7]。

- 升級與分級服務  
  根據用戶身份（如普通用戶、VIP、API Key 等）設定不同的流量限制，實現服務分級與差異化[5][7]。

---

**實際應用範例**

- **全域 API 請求限制**  
  適用於所有 API 路由，預設每分鐘 60 次（可自訂）[5][6][7]。

  ```php
  // app/Providers/RouteServiceProvider.php
  RateLimiter::for('api', function (Request $request) {
      return Limit::perMinute(60)->by($request->ip());
  });
  ```

- **依用戶身份動態限制**  
  例如，普通用戶每分鐘 100 次，VIP 用戶每分鐘 500 次[5][7]。

  ```php
  RateLimiter::for('api', function (Request $request) {
      $user = $request->user();
      if ($user && $user->isPremium()) {
          return Limit::perMinute(500)->by($user->id);
      }
      return Limit::perMinute(100)->by(optional($user)->id ?: $request->ip());
  });
  ```

- **特定路由自訂限制**  
  針對敏感或高資源消耗的 API 設定更嚴格的限制，例如登入、註冊等[6][7]。

  ```php
  Route::post('/login', [AuthController::class, 'login'])->middleware('throttle:5,1');
  ```

- **自訂超限回應**  
  當請求超過限制時，回傳 429 Too Many Requests，可自訂訊息與回應格式[1][5]。

  ```php
  RateLimiter::for('api', function (Request $request) {
      return [
          Limit::perMinute(100)->response(function ($request, $headers) {
              return response('Too many requests, please try again later.', 429, $headers);
          }),
      ];
  });
  ```

---

**技術實現重點**

- 透過 `ThrottleRequests` middleware 或自訂 RateLimiter 規則，靈活套用於不同路由或用戶層級[5][6][7]。
- 可依據用戶、IP、API Key、HTTP 方法等多維度設計限制策略[5][6][7]。
- 超限時自動回應 429 狀態碼，並可自訂訊息與重試等待時間[5][1]。
- 支援快取後端（如 Redis、Memcached）以提升效能與分散式應用支援[8]。

---

**總結**

Laravel API Rate Limiting 適用於任何需要防止濫用、保護系統資源、實現分級服務的 API 應用場景。其彈性設計可滿足從簡單到複雜的流量管控需求，是現代 API 開發不可或缺的重要工具[5][6][7]。

---

**參考來源:**

[1] https://blog.twjoin.com/laravel-%E9%99%90%E5%88%B6%E6%B5%81%E9%87%8F%E5%B7%A5%E5%85%B7-ratelimiter-throttlerequests-b8c418a13701 \
[2] https://blog.csdn.net/kevin_tech/article/details/104093999 \
[3] https://docs.laravel-dojo.com/laravel/master/rate-limiting \
[4] https://hackmd.io/@RainBowT/SJY9ER8In \
[5] https://dev.to/programmerhasan/how-to-create-api-rate-limit-policies-in-laravel-2m4k \
[6] https://www.interserver.net/tips/kb/how-to-use-rate-limiting-in-laravel/ \
[7] https://loadforge.com/guides/configuring-rate-limiting-in-laravel-a-step-by-step-guide \
[8] https://docs.cornch.dev/zh-tw/laravel/9.x/rate-limiting

---

[返回目錄](./../README.md)

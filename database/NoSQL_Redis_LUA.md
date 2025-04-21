# Redis Lua 腳本完整說明與應用

## 什麼是 Redis Lua 腳本？

Redis 從 2.6 版本開始內建 Lua 腳本支持，允許用戶在伺服器端執行一段 Lua 程式碼，將多條 Redis 命令組合成一個原子操作執行。Lua 是一種輕量級、高效且可嵌入的腳本語言，適合實現複雜邏輯與條件判斷。

---

## Lua 腳本的核心特點

- **原子性**：整個 Lua 腳本在 Redis 伺服器端作為一個整體執行，不會被其他命令打斷，保證操作原子性。
- **減少網路開銷**：多條命令合併成一個腳本執行，客戶端與伺服器間只需一次請求。
- **腳本快取與重用**：Redis 會為腳本生成 SHA1 校驗和，支持 `EVALSHA` 命令直接調用快取腳本，節省網路帶寬。
- **靈活擴展**：Lua 腳本內可調用 Redis 命令（`redis.call()`、`redis.pcall()`），實現複雜業務邏輯。

---

## 主要命令與語法

- **EVAL**  
  執行 Lua 腳本，語法：

  ```
  EVAL script numkeys key [key ...] arg [arg ...]
  ```

  - `script`：Lua 腳本內容。
  - `numkeys`：後續 key 的數量。
  - `key`：腳本使用的 Redis key。
  - `arg`：傳入腳本的參數。

- **EVALSHA**  
  根據 SHA1 校驗和執行已快取的腳本，避免重複傳輸腳本內容。

- **SCRIPT LOAD**  
  預先加載腳本，返回 SHA1 校驗和。

- **SCRIPT EXISTS**  
  檢查腳本是否已存在於伺服器。

- **SCRIPT FLUSH**  
  清除所有快取腳本。

- **SCRIPT KILL**  
  強制停止長時間執行的腳本（有限制條件）。

---

## Lua 腳本中調用 Redis 命令

- `redis.call(command, key, arg1, arg2, ...)`  
  執行 Redis 命令，失敗會拋出錯誤。

- `redis.pcall(command, key, arg1, arg2, ...)`  
  執行 Redis 命令，失敗返回錯誤信息，不拋異常，方便錯誤處理。

---

## 錯誤處理與執行行為

- Lua 腳本執行期間，若某條指令錯誤，腳本會立即中斷並返回錯誤。
- **已執行的命令不會回滾（無事務回滾機制）**，已修改的資料保持不變。
- 可使用 Lua 的 `pcall` 進行錯誤捕獲，避免腳本整體崩潰。

---

## Lua 腳本的應用場景

- **複雜原子操作**：例如分布式鎖的加解鎖、計數器增減、條件更新等。
- **減少網路延遲**：將多條命令合併，減少客戶端與 Redis 伺服器間往返次數。
- **實現原子性事務**：保證多命令操作的整體一致性。
- **實現 CAS（compare-and-set）操作**：如條件判斷後更新資料。
- **分布式系統中的協調邏輯**：如限流、排隊、消息處理等。

---

## 執行流程與腳本管理

- Redis 初始化 Lua 執行環境，載入標準函式庫與 Redis 特定函數（如 `redis.call`）。
- 腳本執行時，Redis 會將腳本編譯成字節碼並執行。
- 腳本可通過 SHA1 校驗和管理與快取，主從複製時會同步腳本。
- 長時間運行的腳本可被 `SCRIPT KILL` 強制終止（受限條件）。

---

**參考來源:**

[1] https://help.aliyun.com/zh/redis/support/usage-of-lua-scripts \
[2] https://www.cnblogs.com/wjf-learning/p/18128977 \
[3] https://blog.csdn.net/qq_42224683/article/details/137744349 \
[4] https://redisbook.readthedocs.io/en/latest/feature/scripting.html \
[5] https://blog.csdn.net/qq_34679704/article/details/124628823 \
[6] https://www.cnblogs.com/felordcn/p/13838321.html \
[7] https://jackeyzhe.github.io/2019/06/17/Redis-Lua%E8%84%9A%E6%9C%AC%E5%A4%A7%E5%AD%A6%E6%95%99%E7%A8%8B/ \
[8] https://github.com/changsongl/lua-redis

---

[返回目錄](./../README.md)

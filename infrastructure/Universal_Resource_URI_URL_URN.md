# 統一資源標識符

> URI、URL 和 URN 是三個相關但有差異的概念

## URI（Uniform Resource Identifier，統一資源標識符）

- **定義**：用來唯一識別某個資源的一串字符，可以是抽象的或具體的識別。
- **功能**：標識資源，不一定提供存取方式。
- **組成**：包含 Scheme（協議或方案）和 Resource Identifier（資源識別符）。
- **範圍**：URI 是一個大範圍的概念，包含 URL 和 URN。
- **語法**：大多遵循 RFC 3986。
- **例子**：
  - `http://example.com/index.html`（同時是 URI 和 URL）
  - `urn:isbn:9780134092669`（同時是 URI 和 URN）

---

## URL（Uniform Resource Locator，統一資源定位符）

- **定義**：URI 的一種，除了標識資源外，還包含資源的位置和如何訪問該資源的資訊。
- **功能**：不僅識別資源，還提供定位和存取方式（如 HTTP、FTP 協議）。
- **範圍**：URL 是 URI 的子集。
- **例子**：
  - `https://www.wikipedia.org/`
  - `ftp://ftp.example.com/file.txt`

---

## URN（Uniform Resource Name，統一資源名稱）

- **定義**：URI 的另一種子集，專注於資源的持久唯一名稱，不包含定位資訊。
- **功能**：標識資源身份，但不提供如何訪問或定位資源的資訊。
- **格式**：以 `urn:` 開頭，後面跟命名空間標識符（NID）和命名空間特定字串（NSS）。
- **例子**：
  - `urn:isbn:9780134092669`（國際標準書號）
  - `urn:oasis:names:tc:SAML:2.0:assertion`

---

## 三者關係總結

- **所有的 URL 和 URN 都是 URI，但並非所有 URI 都是 URL 或 URN。**
- URI 是統一資源標識符的總稱，URL 和 URN 是其兩種不同的實現方式。
- URL 提供資源的「位置」和「存取方法」，URN 僅提供資源的「名稱」或「身份」。

---

## 簡單比喻

- **URI**：資源的「身份證」
- **URL**：資源的「住址」
- **URN**：資源的「名字」

---

## 參考維恩圖（示意）

```
URI
├── URL (定位資源)
└── URN (命名資源)
```

---

**參考來源:**

[1] https://blog.logto.io/zh-TW/unveiling-uri-url-and-urn \
[2] https://razonyang.com/zh-hant/posts/http/uri-url-urn/ \
[3] https://auth0.com/blog/url-uri-urn-differences/ \
[4] http://objcer.com/2017/06/04/The-Difference-Between-URLs-and-URIs/ \
[5] https://blog.csdn.net/LngZd/article/details/114793605 \
[6] https://awesome-doge.github.io/uri-url-urn/ \
[7] https://hackmd.io/@CynthiaChuang/URI-URL-and-URN

---

[返回目錄](./../README.md)


## II. HTTP Header

> Header là nơi chứa **siêu dữ liệu (metadata)** về request hoặc response.

### ✅ Request Header – từ client gửi lên

| Header           | Mục đích                         |
|------------------|----------------------------------|
| `Content-Type`   | Kiểu dữ liệu gửi lên (`application/json`) |
| `Accept`         | Client muốn server trả kiểu nào (`application/json`) |
| `Authorization`  | Chứa token xác thực (Bearer token) |
| `User-Agent`     | Trình duyệt hoặc app đang gọi    |
| `Cookie`         | Gửi kèm các cookies              |

### ✅ Response Header – từ server trả về

| Header           | Mục đích                                  |
|------------------|-------------------------------------------|
| `Content-Type`   | Kiểu dữ liệu trả về                       |
| `Set-Cookie`     | Thiết lập cookie mới                     |
| `Cache-Control`  | Dữ liệu có được cache hay không          |
| `Location`       | Dùng khi redirect hoặc `201 Created` để báo vị trí mới |

---

### ✅ Ví dụ:

```http
GET /users HTTP/1.1
Host: example.com
Authorization: Bearer abc123
Content-Type: application/json

III. HTTP Cookies
Cookies là các cặp key-value được lưu ở client và gửi kèm theo mỗi request.
✅ Công dụng:
Lưu trạng thái đăng nhập
Ghi nhớ tùy chọn người dùng
Xác thực người dùng giữa các request

✅ Set Cookie (từ server):
Set-Cookie: sessionId=abc123; Path=/; HttpOnly

✅ Gửi cookie (từ client):
Cookie: sessionId=abc123

✅ Spring Boot hỗ trợ @CookieValue("sessionId") để lấy cookie

IV. HTTP Parameters – Query vs Path
✅ 1. Query Parameter
GET /products?category=shoes&page=2
@GetMapping("/products")
public List<Product> findProducts(
    @RequestParam String category,
    @RequestParam int page
) { ... }

✅ 2. Path Variable
GET /users/123
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    ...
}

V. Câu hỏi phỏng vấn thường gặp
❓1. 401 khác 403 thế nào?
401 Unauthorized: Chưa đăng nhập
403 Forbidden: Đã đăng nhập nhưng không có quyền

❓2. Khi nào dùng 201?
Khi tạo mới tài nguyên thành công (POST)

❓3. @RequestParam khác @PathVariable?
@RequestParam: query string
@PathVariable: phần cụ thể trong URI

❓4. Có thể dùng cả hai không?
✅ Có. Ví dụ:
GET /users/1/orders?page=2
@GetMapping("/users/{id}/orders")
public List<Order> getOrders(
    @PathVariable Long id,
    @RequestParam int page
) { ... }

❓5. Cookie khác Header không?
Cookie: gửi kèm tự động trong mỗi request (trạng thái)
Header: phải set thủ công (token, metadata...)

VI. Tổng kết
| Thành phần    | Ý nghĩa                                                        |
| ------------- | -------------------------------------------------------------- |
| Status Code   | Phản hồi xử lý request (200, 201, 400, 500...)                 |
| Header        | Metadata của request/response (Content-Type, Authorization...) |
| Cookie        | Lưu trạng thái phiên làm việc giữa các request                 |
| Path Variable | Dữ liệu từ URL dạng `/users/1` (`@PathVariable`)               |
| Query Param   | Dữ liệu sau `?key=value` (`@RequestParam`)                     |

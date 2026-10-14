# 🌐 RESTful API Chuẩn – Cho Java Backend Fresher

---

## I. REST là gì?

> REST (Representational State Transfer) là một **kiến trúc** cho việc xây dựng API trên giao thức HTTP.

### ✅ Đặc điểm REST:
- **Stateless**: Mỗi request độc lập, không lưu trạng thái session trên server.
- **Client-Server**: Tách biệt client và server.
- **Resource-Based**: Mọi thứ là tài nguyên, định danh bằng URI.
- **Representations**: Dữ liệu trả về có thể là JSON, XML, HTML,...
- **Cacheable**: Cho phép cache để tối ưu hiệu năng.

---

## II. RESTful là gì?

> RESTful = API tuân theo nguyên tắc REST.

Ví dụ:
GET /users/1 → Lấy thông tin user có id = 1
POST /users → Tạo user mới
PUT /users/1 → Cập nhật user id = 1
DELETE /users/1 → Xóa user id = 1


---

## III. HTTP Methods và ý nghĩa

| Method     | Ý nghĩa                          | Idempotent |
|------------|----------------------------------|-------------|
| `GET`      | Lấy dữ liệu                      | ✅          |
| `POST`     | Tạo mới                          | ❌          |
| `PUT`      | Cập nhật toàn bộ                 | ✅          |
| `PATCH`    | Cập nhật một phần                | ✅          |
| `DELETE`   | Xóa dữ liệu                      | ✅          |

---

## IV. Cách đặt tên Endpoint chuẩn RESTful

| Thực hiện              | Endpoint ví dụ                | Ghi chú                   |
|------------------------|-------------------------------|---------------------------|
| Lấy tất cả             | `GET /users`                  | Không dùng động từ        |
| Lấy theo ID            | `GET /users/1`                | Không dùng `/getUser`     |
| Tạo mới                | `POST /users`                 | Body chứa thông tin       |
| Cập nhật               | `PUT /users/1`                | Toàn bộ user              |
| Cập nhật một phần      | `PATCH /users/1`              | Ví dụ: đổi password       |
| Xóa                    | `DELETE /users/1`             |                           |

> ✅ Dùng danh từ số nhiều, viết thường, phân cấp theo tài nguyên (resource).

---

## V. HTTP Status Codes phổ biến

| Nhóm | Ý nghĩa chung                          |
|------|----------------------------------------|
| 1xx  | Informational (hiếm dùng)             |
| 2xx  | ✅ Success – Thành công                 |
| 3xx  | Redirect – Chuyển hướng                |
| 4xx  | ❌ Client Error – Lỗi từ phía client   |
| 5xx  | ❌ Server Error – Lỗi phía server      |

### ✅ Các mã cụ thể bạn cần nhớ:

| Mã  | Ý nghĩa                          | Khi nào dùng?                            |
|-----|----------------------------------|------------------------------------------|
| 200 | OK                               | Trả về dữ liệu thành công                |
| 201 | Created                          | Tạo mới thành công (POST)                |
| 204 | No Content                       | Xóa thành công, không có dữ liệu trả về  |
| 400 | Bad Request                      | Dữ liệu đầu vào sai format                |
| 401 | Unauthorized                     | Chưa đăng nhập                           |
| 403 | Forbidden                        | Không đủ quyền                            |
| 404 | Not Found                        | Không tìm thấy tài nguyên                 |
| 409 | Conflict                         | Trùng dữ liệu, conflict                  |
| 500 | Internal Server Error            | Lỗi hệ thống (NullPointer, SQL, v.v.)    |

---

## VI. Request & Response Body

### ✅ Request Body (ví dụ tạo user)

```json
POST /users
{
  "name": "Alice",
  "email": "alice@gmail.com"
}
✅ Response Body
HTTP 201 Created
{
  "id": 1,
  "name": "Alice",
  "email": "alice@gmail.com"
}


VII. Versioning API
Khi cần thay đổi lớn (breaking change), nên dùng version:
GET /api/v1/users
GET /api/v2/users

Có thể version bằng:
URI (/v1/users)
Header (Accept: application/vnd.api.v1+json)

VIII. Best Practices
✅ Tuân thủ REST Method
✅ Không dùng động từ trong endpoint (/getUser ❌)
✅ Trả status code đúng
✅ Body luôn là JSON (hoặc theo chuẩn)
✅ Validation đầu vào bằng DTO + annotation
✅ Không trả lỗi 500 cho lỗi client (phân biệt 400 và 500)
✅ Dùng @ControllerAdvice để xử lý lỗi toàn cục
✅ Cung cấp thông tin lỗi rõ ràng (code, message, timestamp,...)

IX. Câu hỏi phỏng vấn thường gặp
❓1. RESTful API là gì?
Là API tuân theo nguyên tắc REST: stateless, resource-based, sử dụng HTTP method chuẩn.

❓2. POST khác PUT thế nào?
POST: tạo mới
PUT: cập nhật toàn bộ, hoặc tạo nếu chưa tồn tại (upsert)

❓3. Khi nào dùng PATCH?
Khi chỉ cập nhật một phần tài nguyên

❓4. Status code nào cho việc tạo thành công?
201 Created

❓5. Nếu gửi request sai định dạng thì trả gì?
400 Bad Request

❓6. Làm sao xử lý lỗi tập trung trong Spring Boot?
Dùng @ControllerAdvice + @ExceptionHandler để catch exception toàn cục

❓7. Tại sao nên dùng versioning?
Đảm bảo backward compatibility khi thay đổi API

X. Tổng kết
| Thành phần       | Tóm tắt                               |
| ---------------- | ------------------------------------- |
| Method           | GET, POST, PUT, DELETE, PATCH         |
| Status Code      | 200, 201, 400, 401, 403, 404, 500     |
| Endpoint         | Danh từ, phân cấp, không dùng động từ |
| Request/Response | Luôn dùng JSON, rõ ràng, chuẩn        |
| Validation       | Sử dụng DTO + annotation (`@Valid`)   |
| Error handling   | Dùng `@ControllerAdvice`              |



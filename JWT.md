# 🔐 JWT (JSON Web Token) - Hướng Dẫn Toàn Diện

## Mục tiêu
Tài liệu này mô tả **toàn bộ vòng đời của JWT** trong hệ thống authentication, bao gồm:
- Tạo token khi đăng nhập.
- Làm mới access token (refresh).
- Đăng xuất.
- Đăng xuất toàn hệ thống (logout all devices).
- Đổi mật khẩu.
- Quản lý token version.
- Cách sử dụng Redis (và khi nào không cần Redis).

---

## 1. Kiến trúc cơ bản
### 🧩 JWT gồm 3 phần:
Header.Payload.Signature
Ví dụ:
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInZlcnNpb24iOjEsImlhdCI6MTY5NTI1NDQzMywiZXhwIjoxNjk1MjU1MzMzfQ.4kQxg0lXY7F0sFhRTp0sdNAvzYB-KZlwFOLWQqAeaPU

### 🧱 Cấu trúc chi tiết
- **Header**: chứa thuật toán mã hóa (HS256, RS256, v.v.).
- **Payload**: chứa dữ liệu (claims) như userId, role, tokenVersion, thời gian tạo (`iat`) và hết hạn (`exp`).
- **Signature**: chữ ký số để đảm bảo tính toàn vẹn của token.

---
## 2. Hai loại token chính
| Loại Token | Mục đích | Thời hạn | Lưu ở đâu | Khi nào dùng |
|-------------|-----------|-----------|------------|---------------|
| **Access Token** | Dùng để truy cập API | Ngắn (5–15 phút) | Header hoặc Memory | Mỗi request API |
| **Refresh Token** | Dùng để cấp mới access token | Dài (7–30 ngày) | Cookie HTTPOnly / Redis / DB | Khi access token hết hạn |

---

## 3. Luồng xử lý
### 🟢 Login
1. User gửi username/password đến `/auth/login`.
2. Backend kiểm tra thông tin.
3. Nếu hợp lệ:
   - Sinh `accessToken` (ngắn hạn).
   - Sinh `refreshToken` (dài hạn).
   - Gán `tokenVersion` hiện tại của user (ví dụ 1).
   - Trả về:
     ```json
     {
       "accessToken": "<jwt_access>",
       "refreshToken": "<jwt_refresh>"
     }
     ```
4. `refreshToken` có thể lưu:
   - Ở **cookie HTTPOnly** (bảo mật cao nhất).
   - Hoặc **Redis** nếu muốn quản lý tập trung token.
   - Hoặc trong **DB** nếu không dùng Redis.

---

### 🔄 Refresh Token
Khi `accessToken` hết hạn:
1. Client gửi request đến `/auth/refresh` kèm `refreshToken`.
2. Backend thực hiện:
   - Giải mã `refreshToken`.
   - Kiểm tra:
     - Token có hợp lệ không (signature, exp)?
     - `tokenVersion` trong token có trùng với trong DB không?
   - Nếu hợp lệ → sinh **accessToken mới** (và có thể refresh lại refreshToken nếu sắp hết hạn).
3. Trả về `accessToken` mới cho client.

#### ⚙️ Nếu dùng Redis:
- Redis sẽ lưu danh sách `refreshToken` hợp lệ.
- Mỗi lần refresh, kiểm tra `refreshToken` trong Redis:
  - Nếu **không có** → token đã bị thu hồi (logout rồi).
  - Nếu **có** → cấp lại access token mới.

Ví dụ Redis Key:
REFRESH_TOKEN:user:1 -> <jwt_refresh_token>

---

### 🚪 Logout (1 thiết bị)

Khi user logout:
1. Client gửi request `/auth/logout`.
2. Backend xử lý:
   - Nếu dùng **Redis** → xóa key `REFRESH_TOKEN:user:<id>`.
   - Nếu không dùng Redis → chỉ đơn giản **xoá cookie** hoặc **bỏ qua token** trên client.
3. AccessToken còn lại tự hết hạn (vì thời gian ngắn).

---

### 🧨 Logout toàn hệ thống (tất cả thiết bị)
Trường hợp user login trên nhiều thiết bị khác nhau (mỗi thiết bị có refresh token riêng):
1. Tăng `tokenVersion` trong DB (`User.tokenVersion++`).
2. Khi các refresh token cũ được gửi lên → version không khớp → backend từ chối.
3. Như vậy toàn bộ refresh token cũ bị vô hiệu hoá.

→ Đây là cách **logout toàn hệ thống an toàn nhất**, không cần lưu từng token trong Redis.

---

### 🔑 Đổi mật khẩu
Tương tự **logout toàn hệ thống**, vì khi đổi mật khẩu cần đảm bảo toàn bộ token cũ không còn hiệu lực.
- Sau khi đổi mật khẩu, **tăng `tokenVersion`**.
- Tất cả token chứa `oldVersion` sẽ không dùng được nữa.

---

## 4. Token Version – Cách hoạt động
| Field | Ý nghĩa |
|--------|----------|
| `tokenVersion` | Giá trị tăng dần, lưu trong bảng `User` |
| Mục đích | Giúp vô hiệu hoá tất cả refresh token cũ |
| Khi nào tăng | Khi logout all / đổi mật khẩu / phát hiện xâm nhập |
| Kiểm tra | Khi refresh token gửi lên, backend so sánh version |

Ví dụ:
```json
// Payload refresh token
{
  "userId": 1,
  "version": 1
}
```
Nếu user.tokenVersion = 2 trong DB → token này không hợp lệ.

## 5. Có cần Redis không?
🧠 Khi KHÔNG cần Redis
Hệ thống nhỏ, ít người dùng.

Dùng tokenVersion để quản lý vô hiệu hóa token.
Refresh token lưu trong cookie hoặc DB.

⚙️ Khi NÊN dùng Redis
  Nhiều người dùng đăng nhập từ nhiều thiết bị.
  Cần revoke token theo từng session (từng thiết bị).
  Cần tốc độ đọc/ghi nhanh (Redis cực nhanh).
  Dễ dàng scale hệ thống.

Ví dụ key-value trong Redis:
REFRESH_TOKEN:user:1:device:abc123 -> <jwt_refresh_token>
TTL = 7 ngày

## 6. Các thao tác thực tế
| Thao tác            | Mô tả                                     | Liên quan đến |
| ------------------- | ----------------------------------------- | ------------- |
| **Login**           | Sinh token và lưu refresh token           | DB / Redis    |
| **Access API**      | Gửi access token qua header Authorization | -             |
| **Refresh token**   | Xin lại access token mới khi cũ hết hạn   | Redis / DB    |
| **Logout**          | Xóa refresh token / Redis                 | Redis         |
| **Logout all**      | Tăng tokenVersion                         | DB            |
| **Change password** | Tăng tokenVersion                         | DB            |
| **Token revoke**    | Xóa refresh token cụ thể trong Redis      | Redis         |

## 7. Ví dụ code pseudocode
// ✅ Refresh Token Flow
function refreshToken(req, res) {
  const token = req.cookies.refreshToken;
  const payload = jwt.verify(token, REFRESH_SECRET);

  const user = db.findUser(payload.userId);

  // Kiểm tra token version
  if (user.tokenVersion !== payload.version) {
    return res.status(401).json({ message: "Token invalid" });
  }

  // Nếu dùng Redis: kiểm tra tồn tại
  if (!redis.exists(`REFRESH_TOKEN:user:${user.id}`)) {
    return res.status(401).json({ message: "Revoked token" });
  }

  // Cấp lại token mới
  const newAccessToken = jwt.sign({ userId: user.id }, ACCESS_SECRET, { expiresIn: "15m" });
  res.json({ accessToken: newAccessToken });
}

## 8. Tổng kết – Khi nào dùng cái gì?
| Mục tiêu                      | Giải pháp                          | Có cần Redis không? |
| ----------------------------- | ---------------------------------- | ------------------- |
| Login cơ bản                  | Access + Refresh Token             | ❌ Không cần         |
| Logout toàn hệ thống          | tokenVersion trong DB              | ❌ Không cần         |
| Quản lý session từng thiết bị | Redis lưu refreshToken             | ✅ Cần               |
| Xóa token cụ thể              | Redis delete key                   | ✅ Cần               |
| Scale nhiều server            | Redis dùng chung giữa các instance | ✅ Cần               |

## 9. Tóm tắt dòng đời của token
[Login] → tạo accessToken + refreshToken
    ↓
[Access Token hết hạn] → /refresh → cấp mới accessToken
    ↓
[Logout 1 thiết bị] → xóa refreshToken khỏi Redis
    ↓
[Logout all / Đổi mật khẩu] → tăng tokenVersion (DB)
    ↓
[Tất cả token cũ hết hiệu lực]

📘 Kết luận
JWT giúp loại bỏ session truyền thống, dễ scale và phân tán.

Tuy nhiên, để quản lý an toàn cần:
  Access token ngắn hạn.
  Refresh token dài hạn.
  Cơ chế tokenVersion hoặc Redis để thu hồi token.
  HTTPOnly Cookie để tránh XSS.

Kết hợp đúng cách, bạn sẽ có một hệ thống xác thực an toàn, dễ mở rộng và bảo trì.


---
Client                Server (Spring Boot / .NET / Node.js)             Redis
   │                            │                                         │
   │── Login(username,pwd) ─────▶│                                         │
   │                            │── Generate AccessToken + RefreshToken ─▶│ (Lưu vào Redis)
   │                            │                                         │
   │←── AccessToken + RefreshToken ────────────────────────────────────────│
   │                            │                                         │
(AccessToken hết hạn)
   │── Refresh(refresh_token) ─▶│── Kiểm tra trong Redis ─────────────────▶│
   │                            │                                         │
   │                            │◀───────── Hợp lệ? ──────────────────────│
   │                            │── Tạo AccessToken mới ─────────────────▶│
   │←── AccessToken mới ────────│                                         │

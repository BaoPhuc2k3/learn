Các loại tấn công phổ biến

1. SQL Injection (SQLi)
   Mô tả: Kẻ tấn công chèn hoặc thao túng câu SQL qua input để đọc/ghi/ xóa dữ liệu.
   Ví dụ: '; DROP TABLE users; --
   Hậu quả: Lộ/đổi/xoá dữ liệu, leo thang quyền.
   Giảm thiểu: Prepared statements / parameterized queries, ORM, validate/escape input, least privilege DB user, WAF.
2. Cross-Site Scripting (XSS)
   Mô tả: Chèn mã JavaScript độc hại vào trang web để đánh cắp cookie, thực hiện hành động thay người dùng.
   Các dạng: Stored (persistent), Reflected, DOM-based.
   Ví dụ: <script>fetch('/cookie?c='+document.cookie)</script>
   Giảm thiểu: Escape output, Content Security Policy (CSP), input validation, httpOnly cookie.
3. Cross-Site Request Forgery (CSRF)
   Mô tả: Ép người dùng đã login thực hiện hành động không mong muốn bằng cách gửi request từ site khác.
   Ví dụ: Form POST tự submit với cookie session của nạn nhân.
   Giảm thiểu: CSRF tokens, SameSite cookies, kiểm tra Origin/Referer, sử dụng double-submit cookie.
4. SSRF (Server-Side Request Forgery)
   Mô tả: Server bị lừa gửi request tới internal services (metadata, DB admin).
   Hậu quả: Lộ dịch vụ nội bộ, access metadata endpoint cloud.
   Giảm thiểu: Whitelist outbound URLs, network egress rules, metadata service protection.
5. Man-in-the-Middle (MITM)
   Mô tả: Can thiệp/đọc/đổi dữ liệu trên đường truyền.
   Giảm thiểu: TLS everywhere, HSTS, certificate pinning (nếu cần), tránh insecure Wi-Fi.
6. Phishing / Social Engineering
   Mô tả: Lừa người dùng reveal credentials hoặc click link độc hại.
   Giảm thiểu: Training người dùng, MFA, email filtering, DMARC/SPF/DKIM.
7. Brute-Force / Credential Stuffing
   Mô tả: Thử nhiều password hoặc dùng leaked credentials.
   Giảm thiểu: Rate limiting, account lockout, MFA, password protection, anomaly detection.
8. DDoS (Distributed Denial of Service)
   Mô tả: Gây quá tải tài nguyên (băng thông, CPU) làm service unavailable.
   Giảm thiểu: CDNs, rate limit, autoscaling, DDoS protection providers (Cloudflare, AWS Shield).

# An toàn khi lưu JWT

1 — Tóm tắt nhanh
Không nên lưu access token trong localStorage/sessionStorage (dễ bị XSS).
Có thể lưu access token trong HttpOnly Secure cookie, nhưng cookie tự động gửi khiến bạn phải xử lý CSRF.
Thông thường tốt nhất cho web hiện đại (SPA): lưu access token trong bộ nhớ (memory) và lưu refresh token trong HttpOnly Secure SameSite cookie; refresh token được dùng để xin access token mới qua endpoint bảo mật (với CSRF protection / origin checks).

2 — Chi tiết: Các lựa chọn lưu token ở client và rủi ro
A. localStorage / sessionStorage
Ưu: dễ dùng từ JS, dễ gửi Authorization header.
Nhược: bị XSS — attacker chạy JS có thể đọc token → account bị chiếm.
Không khuyến nghị cho access token nếu site có rủi ro XSS.

B. HttpOnly + Secure Cookie
Ưu:
HttpOnly tránh JS đọc token → giảm rủi ro XSS.
Secure chỉ gửi qua HTTPS.
Có thể dùng SameSite để giảm CSRF.

Nhược:
Cookie tự động gửi theo domain → dễ bị CSRF nếu không có biện pháp chống.
Nếu access token có quyền rộng, CSRF có thể gây tác hại.
Khi dùng cookie bạn phải xử lý CSRF (CSRF token, Origin/Referer checks, SameSite, double-submit cookie).

C. Lưu token trong memory (JS variable)
Ưu: Không lưu vĩnh viễn — nếu XSS xảy ra thì attacker phải chạy lúc app đang mở để lấy token (khó hơn).
Nhược: Khi reload trang token mất → cần refresh token cơ chế an toàn.

D. Native mobile
Dùng secure storage (Keychain trên iOS, Keystore trên Android).

3 — Pattern được khuyến nghị (an toàn, thực tế)
SPA / Modern web app:
Sau login: server trả refresh token trong HttpOnly, Secure, SameSite cookie; access token trả trong body (JS nhận và lưu chỉ trong memory).
Mỗi request API: JS gửi Authorization: Bearer <access_token> header.
Khi access token hết hạn: JS gọi endpoint /refresh (cookie tự gửi refresh token) => server kiểm tra rồi trả access token mới (vẫn trả trong body).
Bảo vệ endpoint /refresh bằng Origin/Referer check và limit attempts; quay vòng / rotate refresh token; support revocation.
Server-rendered app (traditional cookie session):
Có thể dùng HttpOnly session cookie (server-side session id) — đơn giản và an toàn nếu có CSRF protection.

4 — CSRF & cookie: cách giảm thiểu khi token nằm trong cookie
SameSite=Lax hoặc SameSite=Strict (Lax thường đủ cho GET-safe + login flows).
Dùng CSRF token (double submit cookie pattern) hoặc header kiểm tra (ví dụ X-Requested-With).
Kiểm tra Origin / Referer trên các request thay đổi trạng thái (POST/PUT/DELETE).
Thiết lập cookie flags: HttpOnly; Secure; SameSite=Strict (tùy UX).
Limit scope: Path & Domain nhỏ nhất cần thiết; đặt TTL ngắn.

5 — Cấu hình cookie ví dụ (Set-Cookie header)
Set-Cookie: refresh_token=eyJ...; HttpOnly; Secure; SameSite=Strict; Path=/auth/refresh; Max-Age=2592000
Gợi ý:
HttpOnly — không thể đọc từ JS.
Secure — chỉ gửi qua HTTPS.
SameSite=Strict|Lax — giảm CSRF.
Path — giới hạn endpoint gửi cookie.
Max-Age hoặc Expires — đặt thời gian hợp lý; dùng rotate refresh token.

6 — Một số best practices thêm
Access token ngắn hạn (ví dụ 5–15 phút); refresh token dài hạn nhưng an toàn.
Không đặt quyền quá rộng trong token (use scopes).
Refresh token rotation: mỗi lần dùng refresh token, server cấp một refresh token mới và blacklist token cũ.
Có cơ chế revoke token (logout global).
Logging + anomaly detection (refresh từ IP lạ → verify).
Triển khai Content Security Policy (CSP) để giảm XSS.

7 — Kết luận ngắn
Có, bạn có thể lưu access token trong HttpOnly cookie — nhưng cookie tự động gửi làm tăng rủi ro CSRF nên phải có biện pháp chống CSRF.
An toàn hơn cho SPA: lưu access token trong memory, refresh token trong HttpOnly Secure cookie, kèm CSRF/origin checks và token rotation.

# Revoke Token JWT

Mục tiêu của “Revoke Token” là gì?
✅ Revoke token (thu hồi token) = làm cho token đã phát hành không còn hiệu lực nữa,dù nó chưa hết hạn theo thời gian (exp).
Dùng trong các tình huống:
Người dùng logout.
Token bị rò rỉ / hack.
Admin muốn force logout tất cả user (global logout).
Token refresh cũ vẫn còn tồn tại sau khi cấp mới → cần vô hiệu hóa token cũ (rotation).

⚙️ Cơ chế của JWT & vấn đề

1. JWT là stateless
   Server không lưu lại danh sách token đã phát hành.
   Token tự xác thực bằng chữ ký (signature) → chỉ cần hợp lệ & chưa hết hạn thì được chấp nhận.
   👉 Nghĩa là: nếu bị lộ token, không thể revoke được ngay trừ khi server chủ động lưu blacklist / denylist.
   💡 Các Cơ Chế Revoke Token Phổ Biến

   | Cách làm                                         | Ưu điểm                         | Nhược điểm                              | Phù hợp              |
   | -------------------------------------------------- | ---------------------------------- | ------------------------------------------- | ---------------------- |
   | **1. Blacklist / Denylist**                        | Dễ hiểu, kiểm soát tốt        | Tốn lưu trữ, cần kiểm tra mỗi request | JWT, REST API          |
   | **2. Token Versioning**                            | Không cần DB lookup mỗi request | Cần DB check khi refresh                   | JWT + user table       |
   | **3. Short-lived Access Token + Refresh Rotation** | Hiệu quả, ít rủi ro            | Phức tạp hơn chút                       | SPA / Mobile app       |
   | **4. Stateful Session (không JWT)**               | Dễ revoke (xóa session)          | Không mở rộng tốt                       | Web app truyền thống |

🔹 1. Blacklist (hoặc Denylist)
Cách hoạt động:
Khi user logout hoặc admin revoke, server lưu jti (JWT ID) hoặc token string vào DB/cache (Redis).
Mỗi lần API nhận token → kiểm tra xem token có trong blacklist không.
Nếu có → từ chối.

Khi logout:
_blacklist.Add(token, expiresAt); // lưu token và thời gian hết hạn
Redis là nơi lý tưởng để lưu (nhanh, có TTL tự xoá).

2. Token Versioning (User token version)
   Ý tưởng:
   Trong bảng user có cột token_version (hoặc revocation_key).
   Mỗi JWT chứa token_version lúc tạo ra.
   Khi logout, server chỉ cần tăng token_version trong DB.
   Token cũ (với version cũ) tự bị vô hiệu hoá.

Ví dụ:


| user_id | username | token_version |
| ------- | -------- | ------------- |
| 42      | alice    | 3             |

JWT payload:
{
"sub": 42,
"version": 3
}

Khi kiểm tra token:
var user = db.Users.Find(token.sub);
if (token.version != user.token_version)
return Unauthorized();

➡️ Khi logout, server UPDATE Users SET token_version = token_version + 1.
→ Mọi token cũ (dù còn hạn) đều invalid ngay.

3. Refresh Token Rotation (phổ biến nhất cho SPA)
   Cách hoạt động:
   Mỗi lần client gọi /refresh, server thu hồi refresh token cũ, cấp refresh token mới.
   Lưu refresh token hợp lệ trong DB hoặc Redis.
   Khi logout → xóa refresh token khỏi DB → client không thể lấy access token mới.
   → Vì access token chỉ sống ngắn (~15 phút), token cũ sẽ sớm hết hạn → revoke gần như toàn hệ thống.
   Ưu điểm: Hiệu quả, ít tốn tài nguyên, rất phổ biến trong OAuth2.

🔹 4. Global Logout
Nếu bạn cần logout tất cả user / toàn hệ thống, có vài cách:


| Trường hợp          | Cách làm                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| Stateless JWT          | Tăng`global_version` hoặc `key_id` cho toàn hệ thống, thay đổi secret → mọi JWT cũ hết hiệu lực |
| Stateful session       | Xóa toàn bộ session khỏi Redis / DB                                                                      |
| Refresh token rotation | Xóa toàn bộ refresh token trong DB                                                                        |

# So sánh stateless với statefull , jwt với session

I. Tổng quan khái niệm
🔹 Stateful Authentication (Session-based)
Server lưu trạng thái đăng nhập (session) của người dùng.
Client chỉ giữ một session ID (trong cookie).
Mỗi request → cookie gửi session ID → server tra trong session store (RAM/Redis/DB) để biết user nào.
🧠 Ví dụ:
Client: Cookie: session_id=abc123
Server: session["abc123"] = { userId: 42, role: "admin" }

→ Server phải nhớ từng phiên → stateful (có trạng thái).

🔹 Stateless Authentication (JWT-based)
Server không lưu trạng thái người dùng.
Khi login, server trả cho client 1 JWT token, trong đó đã chứa toàn bộ thông tin cần thiết (user id, role, exp, ...).
Mỗi request, client gửi token qua Authorization: Bearer <jwt>.
Server chỉ cần xác minh chữ ký token → không cần truy vấn DB.
🧠 Ví dụ:
JWT payload: { "sub": 42, "role": "admin", "exp": 1738972367 }

→ Server không cần nhớ gì → stateless.

II. Bảng so sánh đầy đủ


| Tiêu chí                                | **Stateful (Session)**                                                                | **Stateless (JWT)**                                            |
| ----------------------------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **Lưu thông tin đăng nhập ở đâu** | Server (session store)                                                                | Client (JWT token)                                             |
| **Cơ chế xác thực**                   | Tra cứu session ID trong server                                                      | Xác minh chữ ký JWT                                         |
| **Phụ thuộc vào server memory/DB**     | Có (session lưu trên server hoặc Redis)                                           | Không cần                                                    |
| **Khả năng mở rộng (scalability)**    | Khó mở rộng, cần chia sẻ session giữa server                                    | Dễ mở rộng, server nào cũng xử lý được               |
| **Hiệu năng**                           | Mỗi request phải truy vấn session store                                            | Nhanh hơn, chỉ cần verify token                             |
| **Revoke (logout)**                       | Dễ (xóa session ở server)                                                          | Khó (phải dùng blacklist hoặc versioning)                  |
| **Bảo mật XSS/CSRF**                    | Ít rủi ro XSS (vì không có token trong JS), nhưng dễ CSRF nếu cookie tự gửi | Ít CSRF nếu dùng header, nhưng dễ XSS nếu lưu token sai |
| **Dung lượng mỗi request**             | Nhỏ (chỉ session ID)                                                                | Lớn (token có payload Base64)                                |
| **Khi đổi quyền user / xóa account**  | Có hiệu lực ngay (vì kiểm tra DB/session)                                        | Token vẫn hợp lệ tới khi hết hạn (trừ khi revoke)       |
| **Khi server restart**                    | Mất session nếu không lưu persistent                                              | Không ảnh hưởng                                            |
| **Phù hợp cho**                         | Web app truyền thống (server render, login form)                                    | SPA, mobile app, API gateway, microservices                    |
| **Ví dụ thực tế**                     | ASP.NET Session, Spring Session, PHP session                                          | OAuth2 Access Token, Firebase Auth, ASP.NET JWT Auth           |

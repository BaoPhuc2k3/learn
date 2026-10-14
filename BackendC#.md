# 📘 TÀI LIỆU ÔN PHỎNG VẤN BACKEND C# & SOCIAL NETWORK PROJECT

## I. C# & .NET CORE (KIẾN THỨC NỀN TẢNG)

### 1. Phân biệt Value Type và Reference Type?
* **Value Type:** (int, bool, struct, enum) Lưu trực tiếp giá trị trên **Stack**. Truyền tham số là truyền bản sao (copy).
* **Reference Type:** (class, string, object, interface) Lưu địa chỉ bộ nhớ trên Stack, giá trị thực nằm trên **Heap**. Truyền tham số là truyền địa chỉ ô nhớ.
* **Lưu ý về String:** Mặc dù là Reference Type nhưng `string` trong C# là **Immutable** (bất biến). Khi sửa một chuỗi, nó tạo ra object mới thay vì sửa trên object cũ.

### 2. Dependency Injection (DI) & Lifetimes
* **DI là gì:** Là kỹ thuật bơm sự phụ thuộc từ bên ngoài vào class thông qua Constructor. Giúp code lỏng lẻo (loose coupling) và dễ viết Unit Test.
* **3 loại Lifetime:**
    1.  **Transient:** Tạo mới mỗi khi được yêu cầu.
    2.  **Scoped:** Tạo một lần trong mỗi Request (phổ biến nhất cho DB Context).
    3.  **Singleton:** Tạo một lần duy nhất cho toàn bộ vòng đời ứng dụng.

### 3. Async/Await và Thread Pool
* **Cơ chế:** `await` không chặn thread chính. Nó giải phóng thread xử lý để quay lại Thread Pool làm việc khác trong khi chờ I/O (DB, API).
* **Sai lầm thường gặp:** Dùng `.Result` hoặc `.Wait()` gây ra **Deadlock**. Luôn dùng `await` xuyên suốt (Async all the way).

---

## II. KIẾN THỨC DỰ ÁN MẠNG XÃ HỘI (CASE STUDY)

Dưới đây là các câu hỏi xoáy sâu vào dự án Social Network (React + .NET) của bạn:

### 1. Thiết kế chức năng "Newsfeed" (Bảng tin)
* **Bài toán:** Làm sao để hiện bài viết từ những người User đang follow?
* **Trả lời:** * *Mức độ cơ bản:* Dùng SQL `JOIN` bảng `Posts` với bảng `Followers`. 
    * *Mức độ cao cấp (Optimization):* Sử dụng **Redis**. Khi một người đăng bài (Publisher), hệ thống sẽ đẩy ID bài viết vào "Timeline" (List/Sorted Set) của tất cả người theo dõi trong Redis. Khi User vào app, chỉ cần lấy từ Redis -> Tốc độ cực nhanh.

### 2. Xử lý Real-time (Chat, Notification)
* **Công nghệ:** **SignalR** (WebSockets).
* **Cơ chế:** Khi User A gửi tin nhắn cho User B, Server nhận qua SignalR Hub, kiểm tra User B có online không rồi đẩy dữ liệu xuống trực tiếp. Nếu User B offline, lưu vào Database và gửi Push Notification.

### 3. Thiết kế Database cho "Like" và "Follow"
* **Bảng Like:** `PostId`, `UserId`. Cần đánh **Composite Index** trên cả 2 cột để tránh 1 user like 1 bài viết 2 lần và giúp truy vấn `Count()` nhanh hơn.
* **Bảng Follow:** `FollowerId`, `FollowingId`. Đây là quan hệ Many-to-Many trên cùng một bảng Users (Self-referencing).

---

## III. DATABASE & OPTIMIZATION (HỆ THỐNG CHỨNG KHOÁN/TÀI CHÍNH)

Vì bạn làm ở công ty chứng khoán, họ sẽ hỏi rất kỹ về hiệu năng:

### 1. Indexing trong SQL
* **Clustered Index:** Sắp xếp dữ liệu vật lý theo thứ tự (mặc định là Primary Key).
* **Non-Clustered Index:** Một cấu trúc riêng biệt chứa con trỏ tới dữ liệu. 
* **Lưu ý:** Đánh quá nhiều Index sẽ làm chậm thao tác `INSERT/UPDATE/DELETE`.

### 2. Xử lý Concurrency (Tranh chấp dữ liệu)
* **Ví dụ:** Hai người cùng nhấn Like khi số lượt Like đang là 99. Làm sao để lên 101 thay vì 100?
* **Giải pháp:** * Sử dụng **Optimistic Concurrency** (RowVersion/Timestamp trong EF Core).
    * Hoặc dùng câu lệnh SQL nguyên tử: `UPDATE Posts SET LikeCount = LikeCount + 1 WHERE Id = @Id`.

---

## IV. DEVOPS & INFRASTRUCTURE (THẾ MẠNH CỦA BẠN)

### 1. Quy trình CI/CD cho ứng dụng .NET
* Sử dụng Docker để đóng gói ứng dụng.
* **Multi-stage build:** Dùng image SDK để build, sau đó copy file DLL sang image Runtime (như Alpine) để giảm dung lượng image từ 800MB xuống còn 100MB.

### 2. Monitoring & Logging
* Dùng **Serilog** để log dữ liệu vào **Elasticsearch** (ELK Stack) hoặc **Seq**.
* Trong dự án mạng xã hội, việc log lại các hành vi bất thường (như spam post) là cực kỳ quan trọng để bảo mật hệ thống.

---

## V. CÂU HỎI TÌNH HUỐNG THỰC TẾ

1.  **Làm gì khi API bị chậm?** * Check SQL Execution Plan (thiếu Index?).
    * Check Network latency.
    * Check xem có lỗi N+1 trong Entity Framework không (thiếu `.Include()`).
2.  **Làm sao để bảo mật Token JWT?** * Lưu ở **HttpOnly Cookie** để chống tấn công XSS. 
    * Sử dụng **Refresh Token** để hạn chế thời gian sống của Access Token.
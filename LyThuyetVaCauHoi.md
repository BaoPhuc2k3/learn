# 🚀 BÁCH KHOA TOÀN THƯ .NET & CẨM NANG PHỎNG VẤN INTERN/FRESHER

Tài liệu này được tổng hợp và hệ thống hóa từ A-Z, đi từ Core C# đến Web API, Database, System Design và Security. Phần cuối là bộ câu hỏi phỏng vấn thực chiến giúp bạn tự tin ứng tuyển vị trí Intern/Fresher .NET.

---

## PHẦN A: TỔNG HỢP KIẾN THỨC .NET ĐẦY ĐỦ (THE COMPREHENSIVE GUIDE)

### 1. C# Core & Quản Lý Bộ Nhớ
* **Value Type vs Reference Type:**
  * **Value Type:** (`int`, `bool`, `struct`, `enum`). Lưu trực tiếp giá trị trên **Stack**. Truyền tham số là copy giá trị.
  * **Reference Type:** (`class`, `string`, `object`, `delegate`). Lưu con trỏ trên Stack, giá trị thực nằm trên **Heap** (do Garbage Collector - GC quản lý).
* **String Immutability:** `string` là Reference Type nhưng mang tính bất biến. Sửa chuỗi là tạo object mới. Cần dùng `StringBuilder` khi thao tác chuỗi trong vòng lặp.
* **Từ khóa tham số (`ref`, `out`, `in`):**
  * `ref`: Truyền tham chiếu, biến phải khởi tạo trước.
  * `out`: Truyền tham chiếu, dùng để trả ra kết quả, không cần khởi tạo trước, bắt buộc gán giá trị trong hàm.
  * `in`: Truyền tham chiếu dạng chỉ đọc (Read-only), tối ưu hiệu năng.
* **`const` vs `readonly`:** `const` gán lúc compile-time (phải gán ngay), `readonly` gán lúc runtime (có thể gán trong constructor).

### 2. OOP & Nguyên Tắc Lập Trình (SOLID)
* **4 Tính chất OOP:** Đóng gói (Encapsulation), Trừu tượng (Abstraction), Kế thừa (Inheritance), Đa hình (Polymorphism - Overload/Override).
* **Interface vs Abstract Class:** 
  * Interface: Xác định hành vi (CAN-DO), đa kế thừa. 
  * Abstract Class: Chia sẻ logic chung (IS-A), đơn kế thừa.
* **SOLID Principles:**
  * **S (Single Responsibility):** Một class chỉ làm 1 việc (VD: Tách gửi Email ra khỏi User Service).
  * **O (Open/Closed):** Mở rộng bằng code mới, đóng với việc sửa code cũ (Dùng Interface).
  * **L (Liskov Substitution):** Class con thay thế được class cha mà không làm hỏng chương trình.
  * **I (Interface Segregation):** Chia nhỏ Interface, không ép class implement hàm không dùng.
  * **D (Dependency Inversion):** Class cấp cao không phụ thuộc class cấp thấp, cả 2 phụ thuộc vào Abstraction (DI/IoC).

### 3. Delegate, Event & LINQ
* **Delegate:** Biến chứa tham chiếu đến hàm. Các delegate dựng sẵn:
  * `Action`: Hàm trả về `void`.
  * `Func`: Hàm có giá trị trả về (`TResult` nằm cuối).
  * `Predicate`: Hàm nhận 1 tham số, trả về `bool` (dùng lọc dữ liệu).
* **Event:** Dựa trên Delegate, áp dụng Publisher-Subscriber. Tránh memory leak bằng cách implement `IDisposable` (hàm `Dispose()`) và gỡ đăng ký event (`-=`).
* **LINQ (Language Integrated Query):**
  * **Deferred Execution:** Lệnh LINQ chỉ tạo "kế hoạch", chỉ thực thi khi gọi `.ToList()`, `.First()`, `Count()`, hoặc lặp `foreach`.
  * **IQueryable vs IEnumerable:** `IQueryable` dịch ra SQL chạy dưới DB (tối ưu). `IEnumerable` tải hết lên RAM rồi mới lọc.
  * **Các hàm hay dùng:** `Where` (lọc), `Select` (biến đổi/map), `OrderBy/ThenBy`, `GroupBy`, `Any/All`, `SelectMany` (làm phẳng list).

### 4. Multithreading & Async/Await
* **Thread vs Task:** `Thread` là luồng cấp thấp tốn tài nguyên. `Task` trừu tượng hóa dựa trên **ThreadPool** tái sử dụng luồng (nhẹ & tối ưu).
* **Async/Await:** Cơ chế bất đồng bộ không chặn luồng (Non-blocking). Compiler biến nó thành State Machine. Khi gặp `await`, luồng hiện tại được nhả về ThreadPool.
* **Deadlock:** Tuyệt đối không dùng `.Result` hoặc `.Wait()` trong code async. Quy tắc: *"Async all the way"*.

### 5. ASP.NET Core Web API
* **Dependency Injection (DI) Lifetimes:**
  * `Transient`: Tạo mới mỗi lần gọi.
  * `Scoped`: Tạo 1 lần mỗi HTTP Request (Dùng cho DbContext).
  * `Singleton`: Tạo 1 lần duy nhất toàn ứng dụng (Cache, Config).
* **Middleware Pipeline:** Các lớp trung gian xử lý Request/Response. Thứ tự quan trọng: `UseRouting` -> `UseAuthentication` -> `UseAuthorization` -> `UseEndpoints`.
* **HTTP Header & Status Code:**
  * **200** (OK), **201** (Created), **400** (Bad Request), **401** (Unauthorized - Sai token), **403** (Forbidden - Thiếu quyền), **404** (Not Found), **500** (Server Error).
  * Request param: `[FromQuery]`, `[FromRoute]`, `[FromBody]`.

### 6. Entity Framework Core (EF Core)
* **Code First vs Database First:** Ưu tiên Code First, dùng Migration (`dotnet ef migrations add`) để cập nhật DB.
* **Loading Data:**
  * *Eager Loading:* Dùng `.Include()` để JOIN lấy dữ liệu liên quan ngay lập tức.
  * *Lazy Loading:* Gọi đến đâu query đến đó (Nguy cơ chết người: **Lỗi N+1 Query**).
* **Tracking:** EF mặc định theo dõi entity. Với API đọc (GET), **bắt buộc** thêm `.AsNoTracking()` để giảm RAM và tăng tốc độ.
* **DbSet & DbContext:** `DbContext` là cầu nối C# & DB, quản lý Transaction và Connection.

### 7. Database, SQL Server & Redis
* **Indexing:** 
  * *Clustered Index:* Lưu dữ liệu vật lý theo thứ tự (chỉ có 1, thường là PK).
  * *Non-Clustered Index:* Lưu con trỏ (có thể có nhiều). Lạm dụng index làm chậm `INSERT/UPDATE`.
* **ACID & Isolation Levels:**
  * *ACID:* Atomicity (All or nothing), Consistency, Isolation, Durability.
  * Tránh *Dirty Read, Phantom Read* bằng cách config Isolation Level (Read Committed, Repeatable Read...).
* **Redis Cache:** Lưu dữ liệu RAM giảm tải DB. Dùng cho giỏ hàng, OTP, Session.

### 8. Bảo Mật (Security)
* **JWT (JSON Web Token):** Cấu trúc Header.Payload.Signature. 
  * *Lưu ý:* Không lưu pass trong payload. 
  * *Lưu trữ an toàn:* Access Token lưu ở memory/localStorage (rủi ro XSS). Refresh Token lưu ở `HttpOnly, Secure Cookie` (chống XSS, cần cấu hình SameSite chống CSRF).
* **Web Attacks:** 
  * *SQLi:* Chống bằng Parameterized Query / dùng ORM (EF Core).
  * *XSS:* Encode data, dùng HttpOnly Cookie.
  * *CSRF:* Dùng CSRF Token, SameSite Cookie.

---

## PHẦN B: BỘ CÂU HỎI PHỎNG VẤN INTERN / FRESHER .NET

Dưới đây là các câu hỏi nhà tuyển dụng thường dùng để test "độ sâu" tư duy của bạn, sắp xếp từ cơ bản đến nâng cao.

### Tập 1: C# Core & OOP (Bắt buộc phải qua)
1. **Phân biệt Value Type và Reference Type? `string` là kiểu gì?**
   * *Gợi ý trả lời:* Nêu Stack/Heap. Nhấn mạnh `string` là Reference Type nhưng Immutable.
2. **Từ khóa `var` là strongly-typed (kiểu tĩnh) hay dynamic-type (kiểu động)?**
   * *Đáp án "ăn điểm":* Là Strongly-typed. Nó được xác định kiểu ngay lúc Compile-time, không ảnh hưởng hiệu năng. Phân biệt với `dynamic` là bỏ qua check kiểu lúc compile.
3. **Phân biệt `IEnumerable` và `IQueryable`? Khi nào dùng cái nào?**
   * *Điểm nhấn:* `IQueryable` build ra lệnh SQL (Server-side filtering, tốt cho database). `IEnumerable` tải hết về RAM rồi mới lọc (Client-side, tốt cho in-memory list).
4. **Abstract Class và Interface khác nhau thế nào?**
   * *Thực tế:* Interface định nghĩa "hành vi" (Hợp đồng), có thể đa kế thừa. Abstract Class định nghĩa "bản chất" (IS-A), chia sẻ field/code chung, chỉ đơn kế thừa.
5. **Garbage Collector (GC) trong .NET hoạt động ra sao? Khái niệm `IDisposable`?**
   * *Gợi ý:* GC tự dọn dẹp Heap. Nhưng với resource unmanaged (File, Database connection), phải dùng `IDisposable` (hàm `Dispose()`) và khối lệnh `using` để giải phóng lập tức.

### Tập 2: ASP.NET Core Web API (Thực chiến)
6. **DI (Dependency Injection) là gì? Phân biệt Transient, Scoped, Singleton?**
   * *Trick question:* Nếu tôi inject 1 Service dạng `Transient` vào một Service dạng `Singleton`, điều gì xảy ra? *(Đáp án: Captive Dependency - Service Transient đó sẽ bị giữ lại sống mãi mãi theo Singleton, gây lỗi logic/memory leak).*
7. **Trình bày luồng chạy của Middleware? Nếu tôi đặt `UseAuthorization` trước `UseAuthentication` thì sao?**
   * *Đáp án:* Sẽ bị lỗi logic. Hệ thống sẽ cố gắng kiểm tra quyền (Authorization) trước khi biết người dùng là ai (Authentication), dẫn đến luôn bị 401/403.
8. **Phân biệt mã lỗi 401 và 403?**
   * 401 Unauthorized: Anh là ai? (Chưa login, sai token).
   * 403 Forbidden: Tôi biết anh là ai, nhưng anh không có quyền làm việc này (VD: User thường gọi API Admin).

### Tập 3: Entity Framework Core & Database (Kẻ diệt Fresher)
9. **Lỗi N+1 Query trong Entity Framework là gì? Cách khắc phục?**
   * *Đáp án:* Do Lazy Loading. Lặp qua danh sách 100 Đơn hàng và lấy Tên Khách Hàng -> Sinh ra 101 câu SQL. *Khắc phục:* Dùng Eager Loading với từ khóa `.Include()`.
10. **Khi dùng EF Core để viết API GET (chỉ đọc dữ liệu), bạn làm gì để tối ưu?**
    * *Từ khóa phép màu:* **`.AsNoTracking()`**. Tắt cơ chế theo dõi của EF, giảm tải bộ nhớ, tăng tốc độ truy vấn lên nhiều lần.
11. **Sự khác nhau giữa `.FirstOrDefault()` và `.SingleOrDefault()`?**
    * `FirstOrDefault`: Lấy phần tử đầu, không có trả null. 
    * `SingleOrDefault`: Lấy phần tử duy nhất. Nếu có **nhiều hơn 1** phần tử thỏa mãn -> Văng lỗi (Exception).

### Tập 4: Câu Hỏi Tình Huống / Hệ Thống (Lấy điểm cộng Senior)
12. **Tình huống:** *API lấy danh sách Sản phẩm của bạn tự nhiên chạy mất 5 giây. Bạn sẽ dùng các bước nào để debug và tối ưu?*
    * **Trả lời theo mindset Senior:** 
      * Bước 1: Xem log để biết nghẽn ở đâu (C#, Network hay DB).
      * Bước 2: Kiểm tra DB: Bật profiler xem câu SQL sinh ra. Đã có Index chưa? Có bị lỗi N+1 Query (thiếu Include) không? Có bị Select dư cột không?
      * Bước 3: Tối ưu C#: Đã dùng `.AsNoTracking()` chưa? Có code nào chạy đồng bộ (blocking) không?
      * Bước 4: Nếu DB đã tối ưu mà vẫn chậm do lượng truy cập cao -> Áp dụng Caching (Redis/MemoryCache).
13. **Vòng đời của JWT Token. Bạn làm thế nào để ép người dùng đăng xuất (Revoke Token)?**
    * *Kiến thức:* JWT là stateless (server không lưu). Để Revoke, phải có kĩ thuật.
    * *Giải pháp:* Dùng kĩ thuật **Token Versioning**. Thêm cột `TokenVersion` ở bảng User và ném vào Payload của JWT. Khi đổi pass/logout, tăng `TokenVersion` trong DB lên 1. Request sau gửi token cũ lên so sánh Version sẽ bị từ chối.

---
*Chúc bạn ôn tập tốt và pass phỏng vấn! Nắm vững tài liệu này, bạn đã sở hữu mindset của một Developer .NET cứng cáp.*
# 🚀 TÀI LIỆU ÔN PHỎNG VẤN INTERN / FRESHER .NET DEVELOPER (FULL CORE TO ADVANCED)

---

## MỤC LỤC
1. [Phần I: C# Core & Memory Management](#phần-i-c-core--memory-management)
2. [Phần II: OOP, SOLID & Clean Code](#phần-ii-oop-solid--clean-code)
3. [Phần III: Delegates, Events & Functional Programming in C#](#phần-iii-delegates-events--functional-programming-in-c)
4. [Phần IV: Multithreading, Task & Async/Await](#phần-iv-multithreading-task--asyncawait)
5. [Phần V: Collections, Data Structures & LINQ](#phần-v-collections-data-structures--linq)
6. [Phần VI: ASP.NET Core Web API & Architecture](#phần-vi-aspnet-core-web-api--architecture)
7. [Phần VII: Entity Framework Core (EF Core) & Database Design](#phần-vii-entity-framework-core-ef-core--database-design)
8. [Phần VIII: Database, SQL Server, Transaction & Indexing](#phần-viii-database-sql-server-transaction--indexing)
9. [Phần IX: Security, Authentication (JWT), Cache & Web Attacks](#phần-ix-security-authentication-jwt-cache--web-attacks)
10. [Phần X: Software Engineering, Git, System Design & Câu hỏi tình huống](#phần-x-software-engineering-git-system-design--câu-hỏi-tình-huống)

---

## PHẦN I: C# CORE & MEMORY MANAGEMENT

### Q1: Phân biệt chi tiết Value Type và Reference Type? Dữ liệu được lưu trữ ở đâu?
* **Value Type:** (`int`, `float`, `bool`, `char`, `struct`, `enum`).
  * **Lưu trữ:** Lưu trực tiếp **giá trị** thực tế. Thường nằm trên **Stack** (khi là biến cục bộ trong hàm) hoặc nằm trên **Heap** (khi là trường/field bên trong một `class` Reference Type).
  * **Cơ chế gán:** Sao chép toàn bộ giá trị (Copy value). Thay đổi trên bản sao không ảnh hưởng đến bản gốc.
  * **Gợi nhớ:** Mặc định không thể nhận `null` (trừ khi dùng `Nullable<T>` hay `int?`).
* **Reference Type:** (`class`, `string`, `object`, `interface`, `array`, `List<T>`, `delegate`).
  * **Lưu trữ:** Lưu **biến tham chiếu (địa chỉ ô nhớ)** trên **Stack**, còn **giá trị/đối tượng thực tế** nằm trên bộ nhớ **Heap**.
  * **Cơ chế gán:** Sao chép địa chỉ ô nhớ (Copy reference). Cả 2 biến cùng trỏ đến 1 vùng nhớ trên Heap.
* **Hình ảnh phỏng vấn:**
  > *"Value Type giống như bạn photo ra một cuốn sách trao cho người khác, họ viết gì lên đó sách của bạn không đổi. Reference Type giống như bạn gửi đường link Google Doc cho họ, bất kỳ ai sửa thì file gốc trên Cloud (Heap) cũng đổi theo."*

### Q2: Tại sao String trong C# là Reference Type nhưng lại có tính chất Immutable (Bất biến)?
* **Khái niệm:** Một khi chuỗi `string` đã được khởi tạo trên Heap, nội dung ô nhớ đó **không bao giờ có thể bị sửa đổi**.
* **Bản chất khi thao tác:** Khi nối chuỗi `str += "abc"`, CLR sẽ không sửa chuỗi cũ mà tạo ra một `string` object hoàn toàn mới trên Heap và cho biến `str` trỏ đến địa chỉ mới. Chuỗi cũ trở thành "mác rác" chờ Garbage Collector (GC) thu gom.
* **String Pool (String Constant Pool):** Giúp tiết kiệm bộ nhớ. Các chuỗi literal giống nhau (ví dụ: `string a = "hello"; string b = "hello";`) sẽ cùng trỏ tới 1 ô nhớ duy nhất trong String Pool.
* **Giải pháp tối ưu:** Dùng `StringBuilder` khi cần nối/sửa chuỗi liên tục (vòng lặp). `StringBuilder` quản lý một mảng ký tự động (mutable buffer), tránh cấp phát bộ nhớ rác trên Heap.

### Q3: Phân biệt `const` vs `readonly`?
| Tiêu chí | `const` | `readonly` |
| :--- | :--- | :--- |
| **Thời điểm gán** | **Compile-time** (Biên dịch) | **Runtime** (Khi chương trình thực thi) |
| **Khởi tạo** | Bắt buộc gán ngay khi khai báo | Khai báo ngay hoặc gán trong **Constructor** |
| **Bản chất** | Mặc định là `static`, thay thế trực tiếp giá trị vào IL Code | Có thể có giá trị khác nhau tùy thuộc vào đối tượng (qua Constructor) |
| **Áp dụng** | Chỉ dùng cho Value type & String | Dùng cho tất cả các kiểu dữ liệu |

### Q4: Truyền tham số trong C#: `ref`, `out`, `in` khác nhau như thế nào?
* **Mặc định:** Value Type truyền bản sao giá trị. Reference Type truyền bản sao của địa chỉ tham chiếu.
* **`ref`:** Truyền tham chiếu trực tiếp của ô nhớ.
  * Biến truyền vào **bắt buộc phải khởi tạo giá trị trước**.
  * Hàm có thể sửa hoặc không sửa giá trị biến đó.
* **`out`:** Truyền tham chiếu dùng để trả về dữ liệu (hỗ trợ return nhiều giá trị).
  * Biến truyền vào **không cần khởi tạo trước**.
  * Trong hàm **bắt buộc phải gán giá trị** cho biến `out` trước khi thoát khỏi hàm.
* **`in`:** Truyền tham chiếu read-only (chỉ đọc).
  * Tối ưu hiệu năng cho `struct` lớn (tránh copy dữ liệu).
  * Trong hàm **không được phép sửa đổi** giá trị của biến.

---

## PHẦN II: OOP, SOLID & CLEAN CODE

### Q1: Trình bày 4 tính chất cốt lõi của OOP và cho ví dụ thực tế?
1. **Encapsulation (Đóng gói):** Gom thuộc tính và phương thức vào trong 1 Class, giấu đi dữ liệu bên trong bằng `private`/`protected`, chỉ lộ ra các hàm tương tác qua `public` (Getters/Setters).
   * *Mục tiêu:* Bảo vệ dữ liệu khỏi bị truy cập/sửa đổi trái phép từ bên ngoài.
2. **Abstraction (Trừu tượng):** Ẩn đi chi tiết cài đặt phức tạp (logic xử lý), chỉ đưa ra giao diện chung (`Interface` / `Abstract Class`).
   * *Mục tiêu:* Giảm độ phức tạp, giúp người dùng chỉ cần quan tâm "Làm được gì" thay vì "Làm như thế nào".
3. **Inheritance (Kế thừa):** Class con kế thừa thuộc tính/phương thức của Class cha (mối quan hệ **IS-A**), giúp tái sử dụng code (dấu `:` trong C#).
4. **Polymorphism (Đa hình):** Cho phép một hành vi có nhiều cách thể hiện khác nhau.
   * **Compile-time Polymorphism:** Overloading (Nạp chồng - Cùng tên hàm, khác tham số/kiểu dữ liệu).
   * **Run-time Polymorphism:** Overriding (Ghi đè - Class con viết lại phương thức `virtual`/`abstract` của Class cha qua từ khóa `override`).

### Q2: So sánh Abstract Class và Interface? Khi nào nên dùng loại nào?
| Tiêu chí | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Kế thừa** | Đơn kế thừa (Chỉ kế thừa 1 Class) | Đa kế thừa (Implement nhiều Interface) |
| **Mối quan hệ** | **IS-A** (Là một) | **CAN-DO** (Có thể làm) |
| **Thành phần** | Có thể chứa phương thức có body, biến, field, constructor, access modifiers | Chỉ chứa khai báo signature (từ C# 8+ có default implementation) |
| **Tốc độ** | Nhanh hơn một chút | Chậm hơn một chút do tra cứu bảng vtable |
* **Khi nào dùng:**
  * Dùng **Abstract Class** khi các class con có tính chất chung huyết thống, chia sẻ code tái sử dụng hoặc trạng thái (fields).
  * Dùng **Interface** khi muốn định nghĩa chuẩn giao tiếp (contract) cho các class không cùng bản chất (vd: `IDisposable`, `ICloneable`).

### Q3: Phân tích chi tiết nguyên tắc SOLID kèm ví dụ thực tế?
* **S - Single Responsibility Principle (Đơn trách nhiệm):** Một Class chỉ nên có **một lý do duy nhất để thay đổi** (chỉ làm 1 việc).
  * *Sai:* `UserService` vừa tạo User vừa gửi Email thông báo.
  * *Đúng:* Tách việc gửi email sang `EmailService`.
* **O - Open/Closed Principle (Mở rộng / Đóng sửa đổi):** Mở rộng tính năng mới bằng cách thêm code mới, không sửa code cũ đã chạy ổn định.
  * *Thực thi:* Dùng Interface/Abstraction. Khi cần tính năng thanh toán mới (Momo, VNPay), implement `IPaymentProcessor` thay vì `if-else` trong class cũ.
* **L - Liskov Substitution Principle (Thay thế Liskov):** Class con phải có khả năng thay thế hoàn toàn cho Class cha mà không làm hỏng tính đúng đắn của chương trình.
  * *Lỗi kinh điển:* Class `Square` (Hình vuông) kế thừa `Rectangle` (Hình chữ nhật). Khi đổi chiều rộng của Square, chiều cao bị đổi theo -> làm sai logic tính diện tích Rectangle.
* **I - Interface Segregation Principle (Phân chia Interface):** Thay vì 1 Interface "ôm ôm" quá nhiều hàm, hãy chia thành nhiều Interface nhỏ và chuyên biệt. Class không phải implement các phương thức mà nó không dùng.
* **D - Dependency Inversion Principle (Đảo ngược phụ thuộc):**
  1. High-level module (logic nghiệp vụ) không nên phụ thuộc vào Low-level module (database, logger, email sender). Cả hai nên phụ thuộc vào **Abstraction (Interface)**.
  2. Abstraction không phụ thuộc vào chi tiết, chi tiết phụ thuộc vào abstraction.

---

## PHẦN III: DELEGATES, EVENTS & FUNCTIONAL PROGRAMMING IN C#

### Q1: Delegate là gì? Bản chất của Delegate dưới góc độ CLR?
* **Khái niệm:** Delegate là một biến chứa tham chiếu đến một hoặc nhiều phương thức (Type-safe function pointer).
* **Bản chất:** Khi biên dịch, C# compiler sẽ tạo ra một `class` kế thừa từ `System.MulticastDelegate`.
* **Multicast Delegate:** Delegate có thể trỏ đến nhiều phương thức cùng lúc bằng toán tử `+=`. Khi gọi, các phương thức sẽ thực thi theo đúng thứ tự được thêm vào.

### Q2: Action, Func và Predicate khác nhau như thế nào?
* Tất cả đều là các Delegate viết sẵn (Built-in Generic Delegates) của .NET:
  * **`Action<T1, T2,...>`:** Trỏ đến hàm **không có giá trị trả về** (`void`).
  * **`Func<T1, T2,..., TResult>`:** Trỏ đến hàm **có giá trị trả về** (`TResult` luôn là tham số cuối cùng).
  * **`Predicate<T>`:** Trỏ đến hàm nhận vào 1 tham số kiểu `T` và **trả về `bool`** (Thực chất là `Func<T, bool>`).

```csharp
// Action: Không trả về giá trị
Action<string> printLog = message => Console.WriteLine(message);

// Func: Nhận 2 số int, trả về int
Func<int, int, int> add = (a, b) => a + b;

// Predicate: Kiểm tra số chẵn
Predicate<int> isEven = number => number % 2 == 0;
```

### Q3: Event là gì? Khác biệt giữa Event và Delegate? Tại sao lại cần Event?
* **Khái niệm:** Event là một cơ chế dựa trên Delegate, triển khai Pattern **Publisher-Subscriber** (Người phát - Người nhận tin).
* **Khác biệt quan trọng:**
  * **Delegate:** Nếu lộ `public Delegate`, đối tượng bên ngoài có thể can thiệp bằng cách gán `myDelegate = null` (làm mất toàn bộ danh sách đăng ký) hoặc tự ý kích hoạt `myDelegate.Invoke()`.
  * **Event:** Bọc bên ngoài Delegate. Đối tượng bên ngoài **chỉ có quyền đăng ký (`+=`) hoặc hủy đăng ký (`-=`)**, không thể gán `=`, không thể tự ý kích hoạt event từ bên ngoài.
* **Nguy cơ Memory Leak với Event:** Nếu Subscriber đăng ký Event của Publisher có thời gian sống (lifetime) dài hơn Subscriber, Publisher sẽ giữ tham chiếu mạnh (strong reference) tới Subscriber -> GC không thể thu gom Subscriber.
  * **Khắc phục:** Bắt buộc phải `-=` hủy đăng ký event trong hàm `Dispose()` (khi implement `IDisposable`).

---

## PHẦN IV: MULTITHREADING, TASK & ASYNC/AWAIT

### Q1: Phân biệt Process, Thread và Task trong .NET?
* **Process (Tiến trình):** Là một chương trình đang thực thi trên OS, có vùng nhớ cách biệt hoàn toàn.
* **Thread (Luồng):** Là đơn vị thực thi nhỏ nhất bên trong Process. Các Thread trong cùng 1 Process chia sẻ chung vùng nhớ Heap. Tạo Thread thủ công (`new Thread()`) rất tốn tài nguyên (mất ~1MB RAM cho OS Stack) và chi phí Context Switching cao.
* **Task:** Trừu tượng hóa cấp cao đại diện cho một tác vụ bất đồng bộ. Task sử dụng **ThreadPool** (tập hợp các Thread được .NET quản lý sẵn) để tái sử dụng luồng, giúp tối ưu hiệu năng tối đa.

### Q2: Cơ chế Async/Await hoạt động như thế nào bên dưới Compiler?
* **Mục đích:** Giúp viết code bất đồng bộ không chặn luồng chính (Non-blocking) nhưng cú pháp trông giống như code đồng bộ tuần tự.
* **Bản chất Compiler:** Khi đánh dấu `async`, C# Compiler sẽ chuyển đổi phương thức đó thành một **State Machine (Cấu trúc máy trạng thái)** implement interface `IAsyncStateMachine`.
* **Luồng chạy:** Khi gặp từ khóa `await`:
  1. Chương trình kiểm tra xem Task đó đã hoàn thành chưa.
  2. Nếu chưa xong, luồng hiện tại (ví dụ: UI Thread hoặc Request Thread) được **giải phóng** quay lại ThreadPool để làm việc khác.
  3. Khi Task bất đồng bộ hoàn thành (I/O xong), State Machine tiếp tục chạy đoạn code phía sau `await` trên một luồng khả dụng từ ThreadPool.

### Q3: Tại sao nên tránh dùng `.Result` hoặc `.Wait()`? Gây ra lỗi gì?
* **Hậu quả:** Gây ra **Deadlock** (đặc biệt trong các ứng dụng có `SynchronizationContext` như WinForms, WPF, ASP.NET cũ).
* **Giải thích Deadlock:**
  * `.Result` sẽ khóa (block) luồng hiện tại để chờ Task hoàn thành.
  * Trong khi đó, Task khi chạy xong lại cố gắng lấy lại luồng ban đầu (`SynchronizationContext`) để thực thi đoạn code sau `await`.
  * Luồng ban đầu thì đang bận chờ Task, Task thì đang chờ luồng ban đầu -> Treo ứng dụng vĩnh viễn.
* **Quy tắc vàng:** **"Async all the way"** (Đã async thì async từ trên xuống dưới, sử dụng `await`).

---

## PHẦN V: COLLECTIONS, DATA STRUCTURES & LINQ

### Q1: So sánh `ArrayList`, `List<T>`, `HashSet<T>` và `Dictionary<TKey, TValue>`?
| Loại Collection | Cấu trúc bên dưới | Đặc điểm | Độ phức tạp tìm kiếm |
| :--- | :--- | :--- | :--- |
| **`ArrayList`** | Mảng `object[]` | Chứa mọi kiểu dữ liệu, gây **Boxing/Unboxing** làm giảm hiệu năng nghiêm trọng (Tránh dùng) | $O(n)$ |
| **`List<T>`** | Mảng động Generic `T[]` | Đảm bảo Type-safety. Tự tăng kích thước gấp đôi khi đầy | $O(n)$ (Nếu tìm theo giá trị)<br>$O(1)$ (Nếu lấy theo Index) |
| **`HashSet<T>`** | Hash Table | Tập hợp giá trị **không trùng lặp**, không có thứ tự chỉ số | **$O(1)$** |
| **`Dictionary<K,V>`** | Hash Table (Bucket + Entries) | Lưu dạng cặp Key-Value. Key là duy nhất | **$O(1)$** |

> **Khái niệm Boxing / Unboxing:**
> * **Boxing:** Chuyển đổi Value Type sang Reference Type (chuyển dữ liệu từ Stack lên Heap) -> Tốn năng lượng cấp phát bộ nhớ.
> * **Unboxing:** Ép kiểu ngược lại từ Reference Type về Value Type -> Tốn chi phí kiểm tra kiểu dữ liệu.

### Q2: LINQ là gì? Phân biệt `IEnumerable<T>` vs `IQueryable<T>`?
* **LINQ (Language Integrated Query):** Cú pháp truy vấn dữ liệu đồng nhất trong C#.
* **So sánh kinh điển:**
| Tiêu chí | `IEnumerable<T>` | `IQueryable<T>` |
| :--- | :--- | :--- |
| **Đối tượng** | Dữ liệu In-Memory (Bộ nhớ RAM) như `List`, `Array` | Dữ liệu Out-of-Memory (Database) qua ORM |
| **Cơ chế biên dịch** | Chạy bằng các hàm Delegate / Lambda trong C# | Biên dịch thành **Expression Tree**, sau đó ORM dịch ra câu lệnh **SQL** |
| **Nơi lọc dữ liệu** | Kéo toàn bộ dữ liệu về RAM rồi mới lọc (**Client-side filtering**) | Lọc trực tiếp dưới Database trước khi trả về (**Server-side filtering**) |

### Q3: Deferred Execution (Thực thi trì hoãn) trong LINQ là gì?
* **Định nghĩa:** Các câu lệnh LINQ (như `Where`, `Select`, `OrderBy`) **chưa chạy ngay** tại thời điểm khai báo. Chúng chỉ tạo ra một kế hoạch truy vấn.
* **Thời điểm thực thi thật:** Khi dữ liệu được duyệt qua (qua vòng lặp `foreach`) hoặc khi gọi các hàm chuyển đổi/tổng hợp như `.ToList()`, `.ToArray()`, `.First()`, `.Count()`.

```csharp
var numbers = new List<int> { 1, 2, 3 };

// Câu lệnh LINQ chưa thực thi ở đây
var query = numbers.Where(x => x > 1);

numbers.Add(4); // Thêm phần tử mới

// Lúc này mới thực thi -> Kết quả ra 2, 3, 4
foreach (var n in query)
{
    Console.WriteLine(n);
}
```

---

## PHẦN VI: ASP.NET CORE WEB API & ARCHITECTURE

### Q1: Dependency Injection (DI) là gì? Trình bày 3 Service Lifetimes trong ASP.NET Core?
* **DI là gì:** Là một kỹ thuật thực thi nguyên tắc Dependency Inversion. Thay vì class tự khởi tạo các phụ thuộc (`new MyRepository()`), các phụ thuộc sẽ được IoC Container "bơm" (inject) vào thông qua Constructor.
* **3 loại Lifetime (Vòng đời):**
  1. **Transient (`AddTransient`):** Container tạo ra một Instance **mới mỗi khi được yêu cầu**. Phù hợp với các dịch vụ nhẹ, không lưu trạng thái.
  2. **Scoped (`AddScoped`):** Container tạo ra một Instance **duy nhất cho mỗi HTTP Request**. Mọi class trong cùng 1 request dùng chung instance này. Phù hợp cho `DbContext`.
  3. **Singleton (`AddSingleton`):** Container tạo ra **duy nhất một Instance** cho toàn bộ vòng đời ứng dụng (từ khi app start đến khi shutdown). Phù hợp cho Caching, Configuration.

### Q2: Middleware trong ASP.NET Core là gì? Luồng xử lý (HTTP Pipeline) chạy như thế nào?
* **Khái niệm:** Middleware là các đoạn code trung gian được xếp thành một chuỗi (Pipeline) để xử lý Request đi vào và Response đi ra.
* **Sơ đồ vận hành:** Request đi qua M1 -> M2 -> M3 -> Endpoint Handler -> quay ngược lại M3 -> M2 -> M1 -> Client.
* **Các từ khóa:**
  * `app.Use()`: Thực thi middleware và gọi `next.Invoke()` để chuyển sang middleware tiếp theo.
  * `app.Run()`: Middleware cuối cùng (Short-circuit), dừng pipeline không gọi tiếp.
* **Thứ tự quan trọng:** `UseRouting()` -> `UseAuthentication()` -> `UseAuthorization()` -> `MapControllers()`. (Nếu đặt Authentication sau Authorization, app sẽ cho phép truy cập mà không xác thực!).

```
[HTTP Request]
   │
   ▼
┌─────────────────────────┐
│  Middleware 1 (Logging) │
└──────────┬──────────────┘
           │ next()
           ▼
┌─────────────────────────┐
│  Middleware 2 (Auth)    │
└──────────┬──────────────┘
           │ next()
           ▼
┌─────────────────────────┐
│  Controller / Endpoint  │
└─────────────────────────┘
```

---

## PHẦN VII: ENTITY FRAMEWORK CORE (EF CORE) & DATABASE DESIGN

### Q1: Phân biệt Code First và Database First?
* **Code First:** Viết các Class C# (Entities) trước -> Dùng lệnh Migration (`dotnet ef migrations add`) để EF Core tự tạo/cập nhật bảng trong Database. Dễ quản lý phiên bản DB qua Git.
* **Database First:** Đã có sẵn Database dưới SQL Server -> Dùng lệnh Scaffolding (`dotnet ef dbcontext scaffold`) để sinh ngược ra các Class C# và DbContext.

### Q2: Phân biệt Eager Loading, Lazy Loading và Explicit Loading?
* **Eager Loading:** Load Entity chính cùng với toàn bộ dữ liệu liên quan trong **1 câu truy vấn JOIN duy nhất** bằng hàm `.Include()` và `.ThenInclude()`. (Khuyên dùng).
* **Lazy Loading:** Dữ liệu liên quan chưa được load ngay. Khi truy cập vào property liên quan, EF Core mới tự động gửi thêm câu lệnh SQL xuống DB để lấy dữ liệu.
  * **Nguy cơ N+1 Query:** Nếu lặp qua 100 Đơn hàng (Orders) và truy cập `order.Customer`, EF Core sẽ gửi $1 + 100 = 101$ câu SQL xuống DB -> Làm sập server!
* **Explicit Loading:** Dữ liệu liên quan không tự load. Lập trình viên phải chủ động gọi `.Entry(order).Reference(o => o.Customer).Load()` khi cần.

### Q3: Tối ưu hiệu năng EF Core với `AsNoTracking()`?
* **Mặc định (Tracking):** Khi query dữ liệu, DbContext sẽ lưu bản sao của Entity vào **Change Tracker** để theo dõi sự thay đổi. Khi gọi `SaveChanges()`, nó tự động sinh câu `UPDATE`.
* **Khi dùng `AsNoTracking()`:** Tắt tính năng Change Tracker.
  * **Lợi ích:** Tiết kiệm bộ nhớ RAM, bỏ chi phí so sánh dữ liệu, tốc độ query nhanh hơn gấp nhiều lần.
  * **Sử dụng:** Luôn dùng `AsNoTracking()` cho các API **chỉ đọc (Read-only)**.

---

## PHẦN VIII: DATABASE, SQL SERVER, TRANSACTION & INDEXING

### Q1: So sánh Clustered Index và Non-Clustered Index trong SQL Server?
| Tiêu chí | Clustered Index | Non-Clustered Index |
| :--- | :--- | :--- |
| **Sắp xếp dữ liệu** | Sắp xếp và lưu trữ **dữ liệu vật lý** thực tế trên đĩa cứng theo thứ tự Index | Tạo một cấu trúc cây B-Tree riêng biệt, chứa Key và **con trỏ (RID/Clustered Key)** trỏ tới dữ liệu thực |
| **Số lượng** | **Chỉ có 1** Clustered Index cho mỗi bảng (Thường là Primary Key) | Có thể tạo **nhiều** Non-Clustered Index trên một bảng |
| **Hình ảnh** | Giống như số trang của một cuốn sách | Giống như trang Mục lục ở cuối cuốn sách |

> **Lưu ý phỏng vấn:** Đánh quá nhiều Index sẽ giúp câu lệnh `SELECT` nhanh hơn, nhưng làm các thao tác `INSERT`, `UPDATE`, `DELETE` bị **chậm đi** vì SQL Server phải tính toán và cập nhật lại toàn bộ cây Index!

### Q2: Thuộc tính ACID trong Database Transaction là gì?
* **A - Atomicity (Tính nguyên tử):** Tất cả các câu lệnh trong Transaction phải thành công hoàn toàn, hoặc không có câu lệnh nào được lưu (**All or Nothing**). Lỗi là `ROLLBACK`.
* **C - Consistency (Tính nhất quán):** Dữ liệu trước và sau Transaction phải tuân thủ đúng mọi ràng buộc (Constraints, Foreign Key, Unique).
* **I - Isolation (Tính cách ly):** Các Transaction chạy đồng thời không được can thiệp lẫn nhau.
* **D - Durability (Tính bền vững):** Khi Transaction đã `COMMIT`, dữ liệu sẽ được lưu vĩnh viễn vào ổ đĩa, kể cả khi mất điện đột ngột.

### Q3: Phân tích 4 Isolation Levels trong Transaction và các hiện tượng tương ứng?
Các hiện tượng tranh chấp dữ liệu:
1. **Dirty Read:** Trans A sửa dữ liệu nhưng chưa COMMIT, Trans B vào đọc dữ liệu rác đó. Sau đó Trans A ROLLBACK -> Trans B giữ dữ liệu sai.
2. **Non-Repeatable Read:** Trong 1 Trans, đọc 1 dòng 2 lần ra 2 giá trị khác nhau (do Trans khác `UPDATE` ở giữa).
3. **Phantom Read:** Trong 1 Trans, chạy câu lệnh tìm kiếm 2 lần ra số lượng dòng khác nhau (do Trans khác `INSERT/DELETE` ở giữa).

| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
| :--- | :---: | :---: | :---: |
| **Read Uncommitted** | ✅ Có bị | ✅ Có bị | ✅ Có bị |
| **Read Committed** *(Default SQL Server)* | ❌ Không | ✅ Có bị | ✅ Có bị |
| **Repeatable Read** | ❌ Không | ❌ Không | ✅ Có bị |
| **Serializable** *(An toàn nhất - Chậm nhất)* | ❌ Không | ❌ Không | ❌ Không |

---

## PHẦN IX: SECURITY, AUTHENTICATION (JWT), CACHE & WEB ATTACKS

### Q1: Cấu trúc của JWT (JSON Web Token)? Luồng Authentication hoạt động ra sao?
* **Cấu trúc 3 phần dạng String:** `Header.Payload.Signature` (Mã hóa Base64Url).
  * **Header:** Chứa loại token (`JWT`) và thuật toán ký (`HS256`, `RS256`).
  * **Payload:** Chứa các giá trị `Claims` (User ID, Role, Expiration time `exp`). *Lưu ý: Không lưu dữ liệu nhạy cảm như Password vào Payload vì client dễ dàng giải mã Base64Url!*
  * **Signature:** Chữ ký tạo bởi: `HMACSHA256(Header + Payload, SecretKey)`. Giúp Server kiểm tra tính toàn vẹn, chống sửa đổi token.

### Q2: Luồng Refresh Token & Hủy Token (Revocation)?
* **Access Token:** Thời gian sống ngắn (5-15 phút), gửi kèm HTTP Header `Authorization: Bearer <token>` mỗi khi gọi API.
* **Refresh Token:** Thời gian sống dài (7-30 ngày), dùng để xin cấp lại Access Token mới mà không bắt người dùng đăng nhập lại.
* **Cách lưu an toàn:** Access Token lưu trên bộ nhớ tạm (Memory JS), Refresh Token lưu trong **Cookie HttpOnly, Secure, SameSite** để chống tấn công XSS.
* **Cơ chế Token Versioning (Hủy toàn bộ token khi đổi mật khẩu/logout all):**
  * Lưu cột `TokenVersion` (int) trong bảng `User` dưới DB.
  * Payload của Refresh Token chứa `version`.
  * Khi User chọn "Đổi mật khẩu" hoặc "Logout khỏi tất cả thiết bị", tăng `User.TokenVersion += 1` dưới DB.
  * Mọi Refresh Token cũ mang version cũ sẽ bị từ chối ngay lập tức khi gửi lên `/refresh`.

### Q3: Phân biệt các cuộc tấn công Web phổ biến và cách phòng ngừa?
1. **SQL Injection (SQLi):** Kẻ tấn công chèn chuỗi SQL độc hại vào ô input.
   * *Phòng chống:* Sử dụng **Parameterized Queries** hoặc dùng ORM như EF Core (EF Core tự động dùng Parameterized Query).
2. **Cross-Site Scripting (XSS):** Chèn đoạn mã JavaScript độc hại vào website để trộm Cookie/Token.
   * *Phòng chống:* Encode dữ liệu đầu ra, đặt Cookie flag `HttpOnly` (JS không đọc được cookie này).
3. **Cross-Site Request Forgery (CSRF):** Ép trình duyệt của nạn nhân tự động gửi request có chứa Cookie xác thực sang trang web khác.
   * *Phòng chống:* Dùng CSRF Token, cấu hình `SameSite=Strict` hoặc `Lax` cho Cookie, kiểm tra Header `Origin`/`Referer`.

---

## PHẦN X: SOFTWARE ENGINEERING, GIT, SYSTEM DESIGN & CÂU HỎI TÌNH HUỐNG

### Q1: So sánh `git merge` vs `git rebase`? Khi nào nên dùng loại nào?
* **`git merge`:** Gộp nhánh bằng cách tạo ra một **Merge Commit** mới.
  * *Ưu điểm:* Giữ nguyên lịch sử gốc, an toàn, dễ theo dõi các nhánh song song.
  * *Nhược điểm:* Lịch sử commit bị đan xen, chằng chịt.
* **`git rebase`:** Bốc toàn bộ các commit của nhánh hiện tại và đặt lên trên đầu của nhánh đích (viết lại lịch sử commit).
  * *Ưu điểm:* Lịch sử commit thẳng hàng, cực kỳ sạch sẻ.
  * *Nhược điểm:* Đổi hash commit. **Cực kỳ nguy hiểm nếu rebase trên các nhánh public đã push lên server (như `main`/`develop`)**.
* **Quy tắc:** *"Rebase local commits before pushing, Merge public branches."*

### Q2: Xử lý tình huống: "API của bạn chạy rất chậm (High Latency). Bạn sẽ từng bước điều tra và tối ưu như thế nào?"
*(Đây là câu hỏi phân loại ứng viên cực hay trong phỏng vấn)*

**Các bước trả lời chuẩn Senior/Tech Lead:**
1. **Bước 1: Giám sát và Định vị (Locate issue)**
   * Dùng công cụ Logging/APM (như Application Insights, Seq, ELK) để xác định điểm nghẽn (Bottleneck) nằm ở đâu: Network, CPU/RAM Server, Database hay Third-party API.
2. **Bước 2: Kiểm tra tầng Database (Nếu nghẽn DB - 80% nguyên nhân từ đây)**
   * Bật **SQL Server Profiler** hoặc kiểm tra **Execution Plan** của câu lệnh SQL.
   * Kiểm tra xem câu SQL có bị thiếu Index không (`Index Scan` thay vì `Index Seek`).
   * Kiểm tra xem EF Core có bị lỗi **N+1 Query** không (quên `.Include()`).
   * Kiểm tra xem có đang lấy dư thừa cột không (chuyển sang dùng `.Select()` để lấy đúng các trường cần thiết).
3. **Bước 3: Tối ưu code C#**
   * Kiểm tra xem có đang dùng code đồng bộ blocking (`.Result`, `.Wait()`) không -> Chuyển hoàn toàn sang `async/await`.
   * Sử dụng `AsNoTracking()` cho các API đọc dữ liệu.
4. **Bước 4: Áp dụng Caching**
   * Với dữ liệu ít thay đổi nhưng đọc nhiều (như Danh mục sản phẩm, Cấu hình): Áp dụng Caching (**`IMemoryCache`** hoặc **`Redis`**).

---

## 💡 BỘ CÂU HỎI NHANH "KILLER QUESTIONS" DÀNH CHO FRESHER

1. **Hỏi:** Biến `var` trong C# là dynamic-type hay strongly-typed?
   * **Đáp:** Là **Strongly-typed**! `var` chỉ là từ khóa giúp Compiler tự suy luận kiểu dữ liệu tại thời điểm Biên dịch (Compile-time), không làm giảm hiệu năng.
2. **Hỏi:** `IEnumerable` có dùng được vòng lặp `for` không?
   * **Đáp:** Không! `IEnumerable` chỉ hỗ trợ duyệt một chiều qua `IEnumerator` bằng vòng lặp `foreach`. Muốn dùng `for` phải ép kiểu sang `List` hoặc `Array` để lấy Index.
3. **Hỏi:** `FirstOrDefault()` khác gì `SingleOrDefault()`?
   * **Đáp:** `FirstOrDefault()` lấy phần tử đầu tiên khớp điều kiện (nếu không có trả về null). `SingleOrDefault()` bắt buộc tập hợp chỉ có **duy nhất 1 phần tử** khớp điều kiện; nếu có từ 2 phần tử trở lên khớp điều kiện sẽ **ném ra Exception**!
4. **Hỏi:** `using` statement trong C# thực chất dịch ra khối code nào?
   * **Đáp:** Dịch ra khối `try-finally`, trong đó khối `finally` sẽ gọi hàm `.Dispose()` của đối tượng implement `IDisposable`.
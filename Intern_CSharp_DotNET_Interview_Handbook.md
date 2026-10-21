# CẨM NANG PHỎNG VẤN INTERN C#/.NET — TỪ CƠ BẢN ĐẾN CHUYÊN SÂU

> Góc nhìn Senior .NET Developer · Lý thuyết, code thực tế, tư duy thiết kế và cách trả lời phỏng vấn.
>
> **Mục tiêu:** Hiểu bản chất C#, vì sao một tính năng tồn tại, sử dụng khi nào, tránh khi nào, ưu/nhược điểm và cách giải thích quyết định kỹ thuật.

## Mục lục

- [Phần I. Giới thiệu bản thân và dự án](#phần-i-giới-thiệu-bản-thân-và-dự-án)
- [Phần II. OOP](#phần-ii-oop--lập-trình-hướng-đối-tượng)
- [Phần III. Value Type, Reference Type và bộ nhớ](#phần-iii-c--value-type-reference-type-và-bộ-nhớ)
- [Phần IV. Các từ khóa quan trọng](#phần-iv-các-từ-khóa-quan-trọng-trong-c)
- [Phần V. Access modifiers](#phần-v-access-modifiers)
- [Phần VI. Class, Struct, Enum](#phần-vi-class-struct-enum)
- [Phần VII. Extension Method](#phần-vii-extension-method)
- [Phần VIII. Kiến thức nền mở rộng](#phần-viii-những-kiến-thức-nền-tảng-hay-bị-hỏi-thêm)
- [Phần IX. SOLID và DI](#phần-ix-solid-và-dependency-injection)
- [Phần X. ASP.NET Core Web API](#phần-x-aspnet-core-web-api)
- [Phần XI. EF Core và SQL Server](#phần-xi-entity-framework-core-và-sql-server)
- [Phần XII. Bảo vệ dự án CV](#phần-xii-bảo-vệ-dự-án-trong-cv)
- [Phần XIII. Câu hỏi và đáp án](#phần-xiii-bộ-câu-hỏi-phỏng-vấn-đào-sâu)
- [Phần XIV. Sai lầm thường gặp](#phần-xiv-những-sai-lầm-khi-phỏng-vấn-intern)
- [Phần XV. Checklist](#phần-xv-checklist-cuối-cùng-trước-buổi-phỏng-vấn)

**Nguồn và phạm vi:** Theo ảnh danh sách ôn tập: giới thiệu bản thân, dự án, OOP (Polymorphism, Encapsulation, Abstraction, Inheritance, Override/Overload), value/reference type, `const`/`readonly`/`static`, biến, hàm, `struct`/`enum`/`class`, extension method. Nội dung mở rộng là kiến thức tổng hợp để ôn phỏng vấn, không phải danh mục được ghi trực tiếp trong ảnh. Các dự án nêu theo CV cung cấp: Boarding House Management System (ASP.NET Core MVC, SQL Server); Restaurant Management System (ASP.NET Core Web API, EF Core, JWT, SignalR, ReactJS). Ví dụ giả lập dự án để giải thích không chứng minh chính xác implementation của repository.

### Lộ trình 14 ngày

- [ ] Ngày 1: Giới thiệu bản thân, bảo vệ dự án.
- [ ] Ngày 2–3: OOP, SOLID.
- [ ] Ngày 4: Value/Reference Type, memory, GC.
- [ ] Ngày 5: `const`, `readonly`, `static`, biến, hàm.
- [ ] Ngày 6: Class, Struct, Enum, Interface, Abstract.
- [ ] Ngày 7–8: Extension Method, Generic, LINQ, Async.
- [ ] Ngày 9–11: ASP.NET Core, EF Core, SQL, JWT, SignalR.
- [ ] Ngày 12–14: Mock interview và luyện code.

---

# PHẦN I. GIỚI THIỆU BẢN THÂN VÀ DỰ ÁN

## 1. Giới thiệu bản thân thế nào để gây ấn tượng?

Nhà tuyển dụng muốn biết: giao tiếp có mạch lạc không; thực sự làm gì; có phù hợp Intern không. Công thức 60–90 giây: **Giới thiệu → Kiến thức chính → Dự án tiêu biểu → Điều đã học → Mục tiêu internship**.

### Kịch bản gợi ý

> Em chào anh/chị. Em là Lê Bảo Phúc, sinh viên ngành Công nghệ thông tin tại Đại học Phenikaa.
>
> Em định hướng theo Backend Development với C# và ASP.NET Core. Trong quá trình học, em đã thực hiện các dự án cá nhân để rèn luyện kiến thức về lập trình hướng đối tượng, cơ sở dữ liệu và phát triển ứng dụng web.
>
> Dự án đầu tiên của em là hệ thống quản lý nhà trọ, được xây dựng bằng ASP.NET Core MVC và SQL Server. Qua dự án này, em học cách thiết kế cơ sở dữ liệu quan hệ, xây dựng chức năng CRUD và xử lý luồng dữ liệu trong mô hình MVC.
>
> Dự án tiếp theo là hệ thống quản lý nhà hàng, sử dụng ASP.NET Core Web API, Entity Framework Core, JWT và SignalR. Ở dự án này, em tập trung vào xây dựng RESTful API, sử dụng DTO để trao đổi dữ liệu, phân quyền theo vai trò và gửi thông báo đơn hàng theo thời gian thực.
>
> Qua hai dự án, em nhận thấy mình cần tiếp tục cải thiện kỹ năng thiết kế hệ thống, tối ưu truy vấn và viết code dễ bảo trì. Em mong muốn có cơ hội thực tập trong môi trường chuyên nghiệp để được tham gia quy trình phát triển phần mềm thực tế, học hỏi từ các anh/chị và đóng góp vào sản phẩm của đội ngũ.

Điều chỉnh lời giới thiệu cho đúng những gì có thể chứng minh bằng source code.

## 2. Chuẩn bị bảo vệ dự án

Phải trả lời được: (1) giải quyết vấn đề gì? (2) công nghệ/kiến trúc? (3) trực tiếp viết module nào? (4) request đi qua đâu? (5) bug khó nhất và cách sửa? (6) làm lại sẽ cải thiện gì?

**Luồng tạo đơn hàng minh họa** (không xác nhận rằng dự án hiện tại triển khai y hệt):

```text
ReactJS / Client
    │ HTTP POST + JSON + JWT nếu cần
    ▼
ASP.NET Core Web API
Routing → Authentication/Authorization → Controller → Validation
    │
    ▼
Entity Framework Core → Database
    │ Sau khi thay đổi dữ liệu thành công
    ▼
SignalR / KitchenHub → Các client được phép nhận thông báo
```

**Vì sao dùng SignalR thay polling?** Server chủ động push sự kiện, giảm gọi API định kỳ và cải thiện độ trễ cập nhật; đổi lại phải quản lý connection, reconnect, authorization, message loss. REST API vẫn xử lý resource và trạng thái bền vững.

**Lưu database thành công nhưng gửi SignalR thất bại?** Đơn đã lưu không nên bị coi là thất bại chỉ vì thông báo lỗi. Nếu cần delivery đáng tin cậy hơn, cân nhắc transactional outbox, worker và retry; database transaction không tự bảo đảm gửi SignalR thành công.

---

# PHẦN II. OOP — LẬP TRÌNH HƯỚNG ĐỐI TƯỢNG

## 3. OOP là gì?

OOP (Object-Oriented Programming) tổ chức chương trình quanh các đối tượng có **state** và **behavior**. `class` là bản thiết kế, object/instance là thực thể tạo từ class.

```csharp
public class MenuItem
{
    public int Id { get; set; }
    public string Name { get; set; } = "";
    public decimal Price { get; set; }

    public decimal CalculateTotal(int quantity)
    {
        return Price * quantity;
    }
}

var coffee = new MenuItem
{
    Id = 1,
    Name = "Cà phê",
    Price = 30000m
};
decimal total = coffee.CalculateTotal(2); // 60000
```

| Thành phần | Ý nghĩa |
|---|---|
| `MenuItem` | Class |
| `coffee` | Biến tham chiếu đến instance |
| `Id`, `Name`, `Price` | Properties |
| `CalculateTotal()` | Method |
| `new MenuItem` | Tạo instance |

**Ưu:** quản lý độ phức tạp, tái sử dụng, abstraction, đóng gói. **Nhược:** lạm dụng inheritance, class/interface có thể tạo overengineering; một số bài toán phù hợp procedural/functional hơn.

## 4. Encapsulation — Tính đóng gói

### 4.1. Bản chất

Đóng gói giữ dữ liệu và hành vi trong một đơn vị, đồng thời **kiểm soát cách truy cập và thay đổi trạng thái**. Không chỉ là field `private` và getter/setter.

### 4.2. Ví dụ chưa tốt

```csharp
public class Order
{
    public string Status { get; set; } = "Pending";
}

var order = new Order();
order.Status = "Anything"; // Không bảo vệ nghiệp vụ
```

### 4.3. Ví dụ đóng gói tốt hơn

```csharp
public enum OrderStatus { Pending, Confirmed, Cancelled }

public class Order
{
    public int Id { get; private set; }
    public OrderStatus Status { get; private set; } = OrderStatus.Pending;

    public void Confirm()
    {
        if (Status != OrderStatus.Pending)
            throw new InvalidOperationException("Chỉ được xác nhận đơn đang chờ.");
        Status = OrderStatus.Confirmed;
    }

    public void Cancel()
    {
        if (Status != OrderStatus.Pending)
            throw new InvalidOperationException("Chỉ được hủy đơn đang chờ.");
        Status = OrderStatus.Cancelled;
    }
}
```

`private set` hạn chế quyền ghi; `Confirm()`/`Cancel()` bảo vệ quy tắc nghiệp vụ. Với hệ thống thực tế còn cần authorization, concurrency và consistency ở database.

**Công cụ:** access modifier, property, method, constructor, interface.

| Ưu điểm | Chi phí / hạn chế |
|---|---|
| Bảo vệ invariant | Phải thiết kế API cập nhật |
| Giảm coupling | Có thể thêm boilerplate |
| Dễ đổi implementation | Không thay thế authorization |
| Test logic dễ hơn | Getter/setter thuần túy chưa phải đóng gói tốt |

**Phỏng vấn:** `private set` có đủ không? — Không, còn cần đảm bảo các điều kiện nghiệp vụ. Vì sao không dùng public field? — Khó kiểm soát validation, behavior và tương thích API.

## 5. Inheritance — Tính kế thừa

Inheritance cho phép class dẫn xuất nhận các thành viên có thể kế thừa từ class cha, bổ sung/tùy chỉnh hành vi.

```csharp
public class Employee
{
    public string Name { get; set; } = "";
    public void CheckIn() => Console.WriteLine($"{Name} checked in");
}

public class Chef : Employee
{
    public void Cook() => Console.WriteLine("Preparing food...");
}
```

**IS-A:** `Chef` là `Employee` → inheritance. **HAS-A:** `OrderService` sử dụng repository → composition; không nên viết `OrderService : OrderRepository` chỉ để dùng lại code.

**Single inheritance:** C# class chỉ có một base class trực tiếp, có thể implement nhiều interface:

```csharp
public interface IPrintable { void Print(); }
public interface IExportable { void Export(); }
public class Invoice : IPrintable, IExportable
{
    public void Print() { }
    public void Export() { }
}
```

**Constructor chaining:**

```csharp
public class Employee
{
    public string Name { get; }
    public Employee(string name) => Name = name;
}
public class Chef : Employee
{
    public string Specialty { get; }
    public Chef(string name, string specialty) : base(name)
        => Specialty = specialty;
}
```

Constructor không được kế thừa, nhưng constructor con có thể gọi constructor cha qua `base(...)`.

**Ưu:** tái sử dụng, IS-A, polymorphism. **Nhược:** coupling cha/con, dễ có hierarchy quá sâu, dễ vi phạm LSP. Khi chỉ cần sử dụng hành vi mà không có IS-A, ưu tiên composition.

## 6. Polymorphism — Tính đa hình

Cho phép cùng một contract/lời gọi tạo hành vi khác nhau. Thường phỏng vấn **overloading (phân giải compile time)** và **overriding (runtime virtual dispatch)**; ngoài ra còn interface/generic polymorphism.

### Overloading

```csharp
public class PriceCalculator
{
    public decimal Calculate(decimal price) => price;
    public decimal Calculate(decimal price, int quantity) => price * quantity;
    public decimal Calculate(decimal price, int quantity, decimal discountPercent)
        => price * quantity * (1 - discountPercent / 100);
}
```

Overload khác danh sách tham số, **không thể chỉ đổi return type**:

```csharp
// Không hợp lệ nếu cùng class/cùng signature:
// int GetValue() => 1;
// string GetValue() => "Hello";
```

### Overriding

```csharp
public abstract class PaymentMethod
{
    public abstract void Pay(decimal amount);
}
public class CashPayment : PaymentMethod
{
    public override void Pay(decimal amount)
        => Console.WriteLine($"Thanh toán tiền mặt: {amount}");
}
public class CardPayment : PaymentMethod
{
    public override void Pay(decimal amount)
        => Console.WriteLine($"Thanh toán thẻ: {amount}");
}
PaymentMethod payment = new CardPayment();
payment.Pay(100000m); // Thanh toán thẻ: 100000
```

| Tiêu chí | Overload | Override |
|---|---|---|
| Ý nghĩa | Nhiều signature cùng tên | Tùy biến hành vi kế thừa |
| Parameters | Khác | Phù hợp chữ ký gốc |
| `virtual`/`abstract` | Không yêu cầu | Base member phải cho override |
| `override` | Không | Có |
| Cơ chế | Compile-time overload resolution | Runtime dispatch |
| Inheritance | Không bắt buộc | Có |

### `virtual`, `override`, `new`

```csharp
public class Parent
{
    public virtual void Show() => Console.WriteLine("Parent");
}
public class Child : Parent
{
    public override void Show() => Console.WriteLine("Child");
}
Parent x = new Child();
x.Show(); // Child
```

Che thành viên với `new` (ví dụ độc lập):

```csharp
public class Parent
{
    public void Show() => Console.WriteLine("Parent");
}
public class Child : Parent
{
    public new void Show() => Console.WriteLine("Child");
}
Parent x = new Child();
x.Show(); // Parent
Child y = new Child();
y.Show(); // Child
```

`override` tham gia virtual dispatch; `new` là name hiding. Thực tế dùng `IPaymentProcessor` để bổ sung các cách thanh toán không phải duy trì if/else dài; đổi lại cần đăng ký DI và chọn implementation chính xác.

## 7. Abstraction — Tính trừu tượng

Abstraction chỉ phơi bày những khả năng bên dùng cần biết, che bớt chi tiết thực thi.

```csharp
public interface IOrderService
{
    Task<int> CreateOrderAsync(CreateOrderRequest request);
}

public class OrdersController : ControllerBase
{
    private readonly IOrderService _orderService;
    public OrdersController(IOrderService orderService)
        => _orderService = orderService;
}
```

### Interface

Định nghĩa hợp đồng, class implement theo cách riêng. C# hiện đại cho phép **default interface implementations** và nhiều loại member khác, không nên nói interface luôn không có body.

```csharp
public interface INotificationSender
{
    Task SendAsync(string message);
}
public class EmailSender : INotificationSender
{
    public Task SendAsync(string message)
    {
        Console.WriteLine($"Email: {message}");
        return Task.CompletedTask;
    }
}
public class SignalRNotificationSender : INotificationSender
{
    public Task SendAsync(string message)
    {
        Console.WriteLine($"SignalR: {message}");
        return Task.CompletedTask;
    }
}
```

### Abstract Class

Không thể tạo instance trực tiếp; chứa state, constructor, method có body và abstract method:

```csharp
public abstract class ReportGenerator
{
    public string Title { get; }
    protected ReportGenerator(string title) => Title = title;
    public void PrintTitle() => Console.WriteLine(Title);
    public abstract string Generate();
}
public class SalesReport : ReportGenerator
{
    public SalesReport() : base("Sales Report") { }
    public override string Generate() => "Sales data";
}
```

| Tiêu chí | Interface | Abstract Class |
|---|---|---|
| Mục đích | Contract/capability | Base type + shared state/behavior |
| Tạo instance trực tiếp | Không | Không |
| Instance fields | Không | Có |
| Constructor instance | Không | Có |
| Có thể implement/kế thừa nhiều? | Nhiều interface | Chỉ một base class |
| Method có body | Có thể (C# hiện đại) | Có |
| DI | Rất phổ biến | Có thể |

**Encapsulation vs Abstraction:** Encapsulation kiểm soát truy cập/trạng thái, abstraction tạo hợp đồng hoặc mô hình đơn giản cho client. `Order.Confirm()` bảo vệ invariant; `IOrderService` giấu implementation tạo đơn.

---

# PHẦN III. C# — VALUE TYPE, REFERENCE TYPE VÀ BỘ NHỚ

## 8. Value Type và Reference Type

### Value Type

Biến chứa trực tiếp giá trị kiểu đó; phép gán thông thường copy giá trị.

```csharp
int a = 10;
int b = a;
b = 20;
Console.WriteLine(a); // 10
Console.WriteLine(b); // 20
```

Ví dụ: `int`, `long`, `float`, `double`, `decimal`, `bool`, `char`, `struct`, `enum`, `DateTime`, `Guid`.

### Reference Type

Biến giữ tham chiếu đến object; phép gán copy **tham chiếu**, không clone object.

```csharp
public class Product { public string Name { get; set; } = ""; }
Product a = new Product { Name = "Coffee" };
Product b = a;
b.Name = "Tea";
Console.WriteLine(a.Name); // Tea
```

```text
Value:
  a --> [10]         b --> [20]   (hai giá trị riêng)
Reference:
  a ----\
         > [Product { Name = "Tea" }] (cùng object)
  b ----/
```

| | Value Type | Reference Type |
|---|---|---|
| Biến chứa | Giá trị | Tham chiếu |
| Gán | Copy value | Copy reference |
| Null | `Nullable<T>` khi thích hợp | Runtime có thể null |
| Ví dụ | `int`, `struct`, `enum` | `class`, `string`, array, delegate |
| State shared qua gán | Không | Có thể |
| Allocation | Theo ngữ cảnh | Object class thông thường trên managed heap |

### Value Type có luôn trên stack?

**Không.** Có thể nằm trong stack frame, trong object trên heap, trong array hoặc register. JIT/runtime chọn cách bố trí. `int Quantity` thuộc một class `Order` là value type nhưng không có nghĩa nằm riêng trên stack. Phân biệt dựa trên **value/reference semantics**, không dựa duy nhất vào stack/heap.

### `string` là reference type nhưng immutable

```csharp
string a = "Hello";
string b = a;
b = "World";
Console.WriteLine(a); // Hello
```

Gán `b` đến chuỗi khác không sửa object "Hello". String có equality theo nội dung và không cho sửa ký tự trên instance.

### Boxing/Unboxing

```csharp
int number = 10;
object boxed = number;       // Boxing: bản giá trị boxed
int restored = (int)boxed;  // Unboxing

object obj = 10;
// long wrong = (long)obj;  // InvalidCastException: boxed int != boxed long
long correct = (int)obj;
```

Boxing thường tạo allocation và sao chép giá trị, nên tránh khi xử lý dữ liệu tần suất cao nếu không cần thiết.

---

# PHẦN IV. CÁC TỪ KHÓA QUAN TRỌNG TRONG C#

## 9. `const`, `readonly`, `static`

Ba khái niệm không hoàn toàn cùng chiều: `const` là constant compile-time; `readonly` giới hạn gán **field**; `static` quy định thành viên thuộc về type. Có `static readonly`, không viết `const static` cho field.

### `const`

```csharp
public class AppConstants
{
    public const int MaxLoginAttempts = 5;
    public const string ApplicationName = "Restaurant Management";
}
Console.WriteLine(AppConstants.MaxLoginAttempts);
```

Phải gán compile-time constant tại khai báo; có static ngầm định. Không hợp lệ:

```csharp
// public const DateTime CreatedAt = DateTime.Now;
// public const int RandomValue = new Random().Next();
```

### `readonly`

Gán trong initializer hoặc constructor thích hợp:

```csharp
public class OrderService
{
    private readonly Guid _instanceId;
    public OrderService() { _instanceId = Guid.NewGuid(); }
}
```

**Không làm object immutable:**

```csharp
public class Order { public string Status { get; set; } = "Pending"; }
public class OrderManager
{
    private readonly Order _order = new();
    public void Update()
    {
        _order.Status = "Confirmed"; // Hợp lệ
        // _order = new Order(); // Không hợp lệ
    }
}
```

### `static`

```csharp
public class OrderStatistics
{
    public static int CreatedCount { get; private set; }
    public OrderStatistics() => CreatedCount++;
}
var a = new OrderStatistics();
var b = new OrderStatistics();
Console.WriteLine(OrderStatistics.CreatedCount); // 2
```

Code trên minh họa shared state nhưng không thread-safe. Tăng count đồng thời bằng `Interlocked`:

```csharp
using System.Threading;
public class OrderStatistics
{
    private static int _createdCount;
    public OrderStatistics() => Interlocked.Increment(ref _createdCount);
    public static int CreatedCount => Volatile.Read(ref _createdCount);
}
```

### `static readonly`

```csharp
public static class SystemSettings
{
    public static readonly Guid InstanceId = Guid.NewGuid();
    public static readonly DateTime StartedAt = DateTime.UtcNow;
}
```

```csharp
public class AppConfiguration
{
    public static readonly string EnvironmentName;
    static AppConfiguration()
    {
        EnvironmentName = Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT")
            ?? "Production";
    }
}
```

ASP.NET Core app config biến đổi theo môi trường thường phù hợp `IConfiguration` hoặc Options Pattern hơn static fields.

| | `const` | `readonly` | `static` |
|---|---|---|---|
| Vai trò | Compile-time constant | Hạn chế gán field | Member thuộc type |
| Giá trị runtime | Không (trừ constant hợp lệ) | Có | Có |
| Instance field | Không | Có | Không |
| Mỗi instance khác nhau | Không | Có | Không cho cùng một closed type |
| Kết hợp `static readonly` | Không áp dụng | Có | Có |

**Bẫy public const giữa assembly:** Giá trị có thể được nhúng vào assembly caller lúc compile. Nếu library A đổi `public const int MaxItems = 10` thành `20`, assembly B cũ chưa rebuild có thể còn `10`. `static readonly` hữu ích hơn với public values có thể thay đổi (vẫn xét compatibility).

**Chọn:** const = hằng bất biến; readonly = injected fields/state chỉ gán lúc khởi tạo; static readonly = giá trị chung tính runtime; static method = behavior không phụ thuộc instance. Không lưu `DbContext`, current user hoặc mutable order state vào mutable global static.

## 10. Biến trong C#

Biến có kiểu, scope, lifetime, khả năng thay đổi.

```csharp
int quantity = 2;
decimal price = 35000m;
string name = "Coffee";
bool isAvailable = true;

public class ProductService
{
    private readonly decimal _taxRate = 0.08m; // field
    public decimal Calculate(decimal price) // parameter
    {
        decimal tax = price * _taxRate; // local variable
        return price + tax;
    }
}
```

Local variable phải được gán theo definite-assignment rules trước khi đọc.

### `var`, `object`, `dynamic`

```csharp
var number = 10;   // Compile-time inferred int
// number = "Hello"; // Compile error

dynamic value = 10;
value = "Hello"; // Runtime binding cho member access
// value.NotExist(); // Có thể lỗi runtime

object obj = "Hello";
Console.WriteLine(((string)obj).Length);
```

| | `var` | `object` | `dynamic` |
|---|---|---|---|
| Kiểu compile | Suy luận cụ thể | `object` | `dynamic` |
| Member checking | Compile time | Compile time | Chủ yếu runtime |
| Gán kiểu khác | Theo kiểu suy luận | Có thể | Có thể |
| Dùng | LINQ/code gọn | Heterogeneous APIs | Dynamic interop |

**Nullable:**

```csharp
int? quantity = null; // Nullable<int>
if (quantity.HasValue) Console.WriteLine(quantity.Value);
int result = quantity ?? 0;
string? name = null;
```

Nullable reference annotations là thông tin hỗ trợ static analysis, không biến `string` thành `Nullable<string>`.

## 11. Hàm và phương thức

```csharp
public decimal CalculateTotal(decimal unitPrice, int quantity)
{
    return unitPrice * quantity;
}
```

`public` = access; `decimal` = return type; `CalculateTotal` = method name; đối số khai báo = parameters.

### Static vs instance

```csharp
public class Calculator
{
    public static int Add(int a, int b) => a + b;
    public int Multiply(int a, int b) => a * b;
}
int sum = Calculator.Add(2, 3);
var calc = new Calculator();
int product = calc.Multiply(2, 3);
```

### Pass-by-value, `ref`, `out`, `in`

**Mặc định C# pass-by-value, kể cả reference type: copy giá trị tham chiếu.**

```csharp
public class Product { public string Name { get; set; } = ""; }
static void Change(Product p) => p.Name = "Tea";
static void Replace(Product p) => p = new Product { Name = "New" };
var product = new Product { Name = "Coffee" };
Change(product);
Console.WriteLine(product.Name); // Tea
Replace(product);
Console.WriteLine(product.Name); // Tea, không bị thay object
```

`ref` cho phép sửa chính biến caller, phải khởi tạo trước:

```csharp
static void Increase(ref int number) => number += 1;
int count = 5;
Increase(ref count);
Console.WriteLine(count); // 6
```

`out` để xuất kết quả, method phải gán trước khi return bình thường:

```csharp
if (int.TryParse("123", out int parsed)) Console.WriteLine(parsed);
```

`in` là readonly-by-reference parameter:

```csharp
static decimal Calculate(in decimal price) => price * 1.1m;
```

Không mặc định coi `in` nhanh hơn; với mutable struct có thể có defensive copies.

| | Caller khởi tạo? | Callee gán lại? | Ý nghĩa |
|---|---|---|---|
| Mặc định | Có giá trị hợp lệ | Trên bản copy | Value |
| `ref` | Có | Có, tác động caller | Reference to variable |
| `out` | Không cần | Bắt buộc gán trước return | Output |
| `in` | Có | Không | Readonly by reference |

### Optional/named/params

```csharp
public decimal Calculate(decimal price, int quantity = 1) => price * quantity;
Calculate(50000m);
Calculate(50000m, 3);

CreateOrder(customerId: 10, tableId: 5); // Ví dụ named args khi method tồn tại

public static int Sum(params int[] values) => values.Sum();
int total = Sum(1, 2, 3, 4);
```

Thay optional default value trong public API có thể ảnh hưởng versioning do default được áp dụng phía caller lúc compile. Method tốt: tên rõ, single responsibility hợp lý, input/output dễ hiểu, side effects có chủ đích, không ôm quá nhiều logic.

---

# PHẦN V. ACCESS MODIFIERS

## 12. `public`, `private`, `protected`, `internal`

| Modifier | Phạm vi |
|---|---|
| `public` | Code được phép tham chiếu type/member |
| `private` | Bên trong type chứa |
| `protected` | Type chứa và derived types |
| `internal` | Cùng assembly |
| `protected internal` | Cùng assembly **hoặc** derived type ở assembly khác |
| `private protected` | Type chứa hoặc derived type ở cùng assembly |

Class member mặc định private; top-level type mặc định internal (khi không chỉ định modifier).

```csharp
public class BaseEmployee
{
    private int _salary;
    protected string Department = "Kitchen";
}
public class Chef : BaseEmployee
{
    public void Show()
    {
        Console.WriteLine(Department);
        // _salary: không thể truy cập trực tiếp
    }
}
```

`protected` là một phần contract với lớp con, không nên mở rộng chỉ cho tiện.

```text
RestaurantManagement.sln
├── Restaurant.Api
├── Restaurant.Application
└── Restaurant.Infrastructure
```

```csharp
internal class SqlOrderRepository { }
```

`internal` giới hạn trong cùng assembly; có ngoại lệ được cấu hình như `InternalsVisibleTo`. **Mẹo:** `protected internal` = OR; `private protected` bị giới hạn trong cùng assembly.

---

# PHẦN VI. CLASS, STRUCT, ENUM

## 13. Class

Class là reference type gồm properties, fields, methods, constructors, events và các thành viên khác.

```csharp
public class Customer
{
    public int Id { get; }
    public string Name { get; private set; }

    public Customer(int id, string name)
    {
        if (string.IsNullOrWhiteSpace(name))
            throw new ArgumentException("Customer name is required.");
        Id = id;
        Name = name;
    }

    public void ChangeName(string newName)
    {
        if (string.IsNullOrWhiteSpace(newName))
            throw new ArgumentException("Invalid name.");
        Name = newName;
    }
}
```

Constructor cùng tên class, không có return type, có thể overload/chain bằng `this(...)` hay `base(...)`:

```csharp
public class Product
{
    public string Name { get; }
    public decimal Price { get; }
    public Product(string name) : this(name, 0m) { }
    public Product(string name, decimal price)
    {
        Name = name;
        Price = price;
    }
}
```

Field vs property: field chứa dữ liệu; property định nghĩa accessor:

```csharp
private decimal _price;
public decimal Price
{
    get => _price;
    set
    {
        if (value < 0) throw new ArgumentOutOfRangeException(nameof(value));
        _price = value;
    }
}
public string Name { get; set; } = ""; // Auto-property
```

`init` hỗ trợ gán ở object initialization nhưng không bảo đảm deep immutability:

```csharp
public class ProductDto { public string Name { get; init; } = ""; }
var p = new ProductDto { Name = "Coffee" };
// p.Name = "Tea"; // Không hợp lệ sau initialization
```

## 14. Struct

Struct là value type, thích hợp biểu diễn giá trị nhỏ, rõ semantics, thường immutable, không cần identity riêng.

```csharp
public readonly struct Money
{
    public decimal Amount { get; }
    public string Currency { get; }
    public Money(decimal amount, string currency)
    {
        Amount = amount;
        Currency = currency;
    }
}
var a = new Money(50000m, "VND");
var b = a; // Copy value
```

**Khi dùng:** value semantics, dữ liệu tương đối nhỏ, immutable, dùng thường xuyên khi có lý do design/performance. Không đổi `Order` hay `Customer` thành struct chỉ vì muốn tránh heap.

Struct có constructor; C# hiện đại cho phép explicit parameterless constructor theo quy định. `default(T)` vẫn theo zero initialization chứ không nhất thiết gọi constructor tự định nghĩa.

Struct không kế thừa user-defined class/struct; có base `System.ValueType` trong type system và implement interface được.

```csharp
public interface IPrintable { void Print(); }
public struct Ticket : IPrintable
{
    public void Print() => Console.WriteLine("Ticket");
}
```

## 15. Class vs Struct

| | Class | Struct |
|---|---|---|
| Ngữ nghĩa | Reference | Value |
| Phép gán | Copy reference | Copy value |
| Base class tùy ý | Có | Không |
| Implement interface | Có | Có |
| Null | Runtime reference có thể null | `Nullable<T>` |
| Identity | Tốt cho entity | Tốt cho value objects |
| Mutation | Có thể | Có thể nhưng nên thận trọng |
| Ví dụ | Entity, service | Money, coordinate |

**Struct luôn nhanh hơn?** Không. Struct lớn copy nhiều có thể tốn CPU; boxing có thể cấp phát; class lại có GC overhead. Benchmark khi cần.

Mutable struct dễ khiến hiểu nhầm bản copy:

```csharp
public struct Counter { public int Value { get; set; } }
Counter a = new Counter { Value = 1 };
Counter b = a;
b.Value = 10;
Console.WriteLine(a.Value); // 1
```

## 16. Enum

Enum là value type mô tả các integral named constants:

```csharp
public enum OrderStatus
{
    Pending = 0,
    Confirmed = 1,
    Preparing = 2,
    Completed = 3,
    Cancelled = 4
}
OrderStatus status = OrderStatus.Pending;
if (status == OrderStatus.Pending) Console.WriteLine("Order is pending");
```

**Ưu:** rõ nghĩa, type safety, quản lý trạng thái hữu hạn. **Rủi ro:** enum không phải closed set tuyệt đối:

```csharp
OrderStatus status = (OrderStatus)999;
bool valid = Enum.IsDefined(status);
```

Nếu database lưu enum dạng số, nên gán mã explicit và tránh thay đổi để không làm sai dữ liệu cũ.

`[Flags]` cho các bit flags có thể kết hợp, không dùng cho trạng thái loại trừ lẫn nhau:

```csharp
[Flags]
public enum Permissions { None = 0, Read = 1, Write = 2, Delete = 4 }
Permissions p = Permissions.Read | Permissions.Write;
bool canWrite = p.HasFlag(Permissions.Write);
```

---

# PHẦN VII. EXTENSION METHOD

## 17. Extension Method

Cho phép gọi static method bằng instance syntax trên type đã có mà không sửa source/inherit type đó. LINQ dùng rất nhiều.

```csharp
public static class StringExtensions
{
    public static bool IsValidEmail(this string value)
        => !string.IsNullOrWhiteSpace(value) && value.Contains('@');
}
string email = "test@example.com";
bool isValid = email.IsValidEmail();
// Tương đương về ý nghĩa:
bool alsoValid = StringExtensions.IsValidEmail(email);
```

`Contains('@')` là ví dụ cú pháp, **không phải email validation production**.

**Không override, không dynamic dispatch.** Extension resolution dựa vào kiểu compile-time và những extension đang scope:

```csharp
public class Animal { }
public class Dog : Animal { }
public static class AnimalExtensions
{
    public static void Speak(this Animal a) => Console.WriteLine("Animal");
    public static void Speak(this Dog d) => Console.WriteLine("Dog");
}
Animal animal = new Dog();
animal.Speak(); // Animal
```

Instance method áp dụng được có ưu tiên hơn extension cùng tên:

```csharp
public class Product
{
    public void Print() => Console.WriteLine("Instance");
}
public static class ProductExtensions
{
    public static void Print(this Product p) => Console.WriteLine("Extension");
}
new Product().Print(); // Instance
```

**DI registration extension:**

```csharp
using Microsoft.Extensions.DependencyInjection;
public static class ServiceRegistration
{
    public static IServiceCollection AddApplicationServices(this IServiceCollection services)
    {
        services.AddScoped<IOrderService, OrderService>();
        return services;
    }
}
// Program.cs
builder.Services.AddApplicationServices();
```

**LINQ extensions:**

```csharp
var prices = new[] { 10, 20, 30 };
var result = prices.Where(x => x > 10).Select(x => x * 2).ToList();
```

| Ưu | Nhược |
|---|---|
| API đọc tự nhiên, fluent | Helper quá nhiều, khó tìm |
| Không sửa class gốc | Không virtual dispatch |
| LINQ/DI rất phù hợp | Có thể trùng tên/import namespace |

Không dùng extension để che giấu nghiệp vụ phức tạp cần state, database hoặc nhiều dependency; cân nhắc service qua DI.

---

# PHẦN VIII. NHỮNG KIẾN THỨC NỀN TẢNG HAY BỊ HỎI THÊM

## 18. Stack, Heap và Garbage Collector

Stack quản lý các call frames/thông tin thực thi, một số local values; managed heap cấp phát phần lớn reference objects/boxed values. Không đồng nhất value type = stack và reference type = heap. JIT có thể dùng registers, tối ưu allocation.

**GC** thu hồi managed memory của object không còn reachable từ GC roots (static references, live local references, handles...). Ra khỏi scope không có nghĩa lập tức bị GC.

| Generation | Ý nghĩa |
|---|---|
| Gen 0 | Object mới, thường ngắn hạn |
| Gen 1 | Trung gian |
| Gen 2 | Object lâu đời |

Large Object Heap có cơ chế đặc thù liên quan.

**`IDisposable`/`using`:** GC không thay thế deterministic cleanup của file, socket, handles.

```csharp
using var stream = File.OpenRead("data.txt");

await using var asyncStream = new FileStream(
    "data.txt", FileMode.Open, FileAccess.Read, FileShare.Read,
    bufferSize: 4096, useAsync: true);
```

`Dispose()`/`DisposeAsync()` giải phóng tài nguyên theo hợp đồng IDisposable/IAsyncDisposable, còn GC quản lý managed memory.

## 19. Collections

| Collection | Đặc tính | Tình huống |
|---|---|---|
| `T[]` | Fixed length | Dữ liệu có số lượng cố định |
| `List<T>` | Dynamic capacity | Danh sách |
| `Dictionary<TKey,TValue>` | Hash lookup | Tra cứu ID |
| `HashSet<T>` | Unique | Loại trùng |
| `Queue<T>` | FIFO | Queue công việc |
| `Stack<T>` | LIFO | Undo |
| `ConcurrentDictionary<K,V>` | Concurrent | Shared data đa luồng |

```csharp
int[] numbers = new int[3];
List<int> list = new();
list.Add(10);
list.Add(20);

var menu = new Dictionary<int, string> { [1] = "Coffee", [2] = "Tea" };
Console.WriteLine(menu[1]);
if (menu.TryGetValue(3, out string? item)) Console.WriteLine(item);
```

Array cố định length. `List<T>` khi tăng capacity có thể allocation và copy. Dictionary lookup trung bình gần O(1) không phải bảo đảm O(1) mọi trường hợp; truy cập key vắng bằng indexer gây `KeyNotFoundException`.

`IEnumerable<T>` duyệt; `ICollection<T>` thêm Count/Add/Remove theo contract; `IList<T>` thêm index; implementation có thể readonly. Chọn API theo khả năng cần: enumerate → `IEnumerable<T>`, index → `IReadOnlyList<T>`, mutation → collection contract phù hợp.

## 20. Generic

Generics tăng type safety, tái sử dụng và có thể tránh boxing không cần thiết:

```csharp
public class ApiResponse<T>
{
    public bool Success { get; set; }
    public string Message { get; set; } = "";
    public T? Data { get; set; }
}
var response = new ApiResponse<string>
{
    Success = true,
    Message = "OK",
    Data = "Order created"
};
// ApiResponse<int>, ApiResponse<OrderDto>, ApiResponse<List<OrderDto>>
```

```csharp
public static T GetFirst<T>(IEnumerable<T> items) => items.First();
public static T Create<T>() where T : new() => new T();
```

Constraints như `class`, `struct`, interface, base class, `notnull`, `new()`. So với API trả `object`, generic giữ thông tin kiểu tại compile time, giảm casting và rủi ro runtime errors.

## 21. LINQ

```csharp
var products = new List<Product>
{
    new() { Id = 1, Name = "Coffee", Price = 30000m },
    new() { Id = 2, Name = "Tea", Price = 20000m },
    new() { Id = 3, Name = "Juice", Price = 40000m }
};
var result = products
    .Where(p => p.Price >= 30000m)
    .OrderBy(p => p.Price)
    .Select(p => p.Name)
    .ToList(); // Coffee, Juice
```

| Method | Chức năng |
|---|---|
| `Where` | Filter |
| `Select` | Projection |
| `OrderBy`/`OrderByDescending` | Sort |
| `FirstOrDefault` | First/default |
| `SingleOrDefault` | Zero or exactly one (throw khi nhiều) |
| `Any`/`All` | Kiểm tra điều kiện |
| `Count` | Đếm |
| `GroupBy` | Group |
| `Join` | Join |
| `Skip`/`Take` | Pagination |
| `Distinct` | Unique |

```csharp
var first = products.FirstOrDefault(p => p.Price > 0);
var unique = products.SingleOrDefault(p => p.Id == 1);
```

`SingleOrDefault` không thay cho unique constraint ở database.

**Deferred execution:**

```csharp
var numbers = new List<int> { 1, 2, 3 };
var query = numbers.Where(x => x > 2);
numbers.Add(4);
foreach (var n in query) Console.WriteLine(n); // 3, 4
var snapshot = numbers.Where(x => x > 2).ToList(); // Materialize tại thời điểm này
```

**`IEnumerable<T>` vs `IQueryable<T>`:** `IEnumerable` cho enumeration; LINQ-to-Objects xử lý trong ứng dụng. `IQueryable` có expression/query provider, EF Core có thể dịch sang SQL:

```csharp
var products = await dbContext.Products
    .Where(p => p.Price > 30000m)
    .ToListAsync(); // WHERE ở database nếu provider dịch được

var all = await dbContext.Products.ToListAsync();
var filtered = all.Where(p => p.Price > 30000m); // Lọc trong memory
```

Ưu tiên filtering, sorting, projection, paging trước materialization khi provider hỗ trợ.

## 22. Exception Handling

```csharp
try
{
    int result = int.Parse("abc");
}
catch (FormatException ex)
{
    Console.WriteLine(ex.Message);
}
finally
{
    Console.WriteLine("Completed");
}
```

`throw;` giữ trace thích hợp cho exception đang xử lý; `throw ex;` thay đổi stack trace, thường tránh:

```csharp
catch (Exception)
{
    throw;
}
```

Exceptions cho tình huống bất thường, không thay routine control flow: `int.TryParse` tốt hơn try/catch quanh mỗi lần parse để validate thông thường.

Web API production không expose raw stack trace. Trả structured problem details, ví dụ:

```json
{
  "type": "https://httpstatuses.com/400",
  "title": "Bad Request",
  "status": 400,
  "detail": "Số lượng món phải lớn hơn 0."
}
```

## 23. Async/Await và Task

`Task` biểu diễn operation async, `Task<T>` có kết quả. `async` cho phép dùng `await`; `await` không nhất thiết block thread trong khi chờ async I/O.

```csharp
public async Task<Product?> GetProductAsync(int id)
{
    return await _dbContext.Products
        .FirstOrDefaultAsync(p => p.Id == id);
}
```

**Async không tự tạo thread mới.** Đừng bọc DB synchronous call bằng `Task.Run()` chỉ để giả async:

```csharp
// Không nên trong ASP.NET Core:
// await Task.Run(() => _dbContext.Products.ToList());
// Nên:
await _dbContext.Products.ToListAsync();
```

`Task.WhenAll` hữu ích với những operations độc lập:

```csharp
Task<string> a = GetDataAAsync();
Task<string> b = GetDataBAsync();
await Task.WhenAll(a, b);
Console.WriteLine(a.Result);
Console.WriteLine(b.Result);
```

**Không chạy đồng thời nhiều EF queries trên cùng `DbContext`**: EF Core không hỗ trợ multiple concurrent operations trên một context instance.

```csharp
public async Task<List<Product>> GetProductsAsync(CancellationToken ct)
{
    return await _dbContext.Products.ToListAsync(ct);
}
```

Cancellation là cooperative request, không bắt buộc operation ngừng tức thì. Tránh `async void` trừ event handlers thích hợp; caller khó await/quan sát exception.

```csharp
public async Task ProcessAsync() => await SaveAsync();
// Tránh: public async void ProcessAsync() { await SaveAsync(); }
```

---

# PHẦN IX. SOLID VÀ DEPENDENCY INJECTION

## 24. SOLID

| | Nguyên tắc |
|---|---|
| S — SRP | Một module có một lý do chính để thay đổi |
| O — OCP | Mở rộng mà hạn chế sửa code ổn định |
| L — LSP | Derived type thay thế base type mà giữ contract |
| I — ISP | Không bắt client phụ thuộc thành viên không cần |
| D — DIP | High-level module phụ thuộc abstraction, không gắn chặt implementation |

**SRP:** Không nên để một service duy nhất tạo đơn, gửi mail, xuất Excel, thao tác nhiều hạ tầng. Tách trách nhiệm có ý nghĩa, không phải cứ một method một class.

**OCP:**

```csharp
public interface IDiscountPolicy { decimal CalculateDiscount(decimal amount); }
public class RegularDiscount : IDiscountPolicy
{
    public decimal CalculateDiscount(decimal amount) => 0m;
}
public class VipDiscount : IDiscountPolicy
{
    public decimal CalculateDiscount(decimal amount) => amount * 0.1m;
}
```

Thêm policy mà hạn chế sửa chuỗi điều kiện lớn. Tránh overengineering trước khi có nhu cầu.

**LSP:** Nếu base `Bird.Fly()` hứa bay mà `Penguin.Fly()` luôn `NotSupportedException`, thiết kế contract chưa phù hợp; có thể mô hình khả năng bằng `IFlyable`. Tương tự payment processor không nên vi phạm pre/postconditions mà caller dựa vào.

**ISP:**

```csharp
// Thay vì IEmployee bắt Cook, Deliver, ManagePayroll cho mọi người:
public interface ICook { void Cook(); }
public interface IDeliver { void Deliver(); }
```

**DIP:**

```csharp
public interface IOrderRepository
{
    Task<Order?> GetByIdAsync(int id);
}
public class OrderService
{
    private readonly IOrderRepository _repository;
    public OrderService(IOrderRepository repository) => _repository = repository;
}
```

## 25. Dependency Injection

DI cung cấp dependencies từ bên ngoài thay vì tự `new` implementation bên trong:

```csharp
// Coupled:
public class BadOrderService
{
    private readonly SqlOrderRepository _repository = new SqlOrderRepository();
}

// Constructor injection:
public class OrderService
{
    private readonly IOrderRepository _repository;
    public OrderService(IOrderRepository repository) => _repository = repository;
}
```

```csharp
builder.Services.AddScoped<IOrderRepository, SqlOrderRepository>();
builder.Services.AddScoped<IOrderService, OrderService>();
```

| Lifetime | Ý nghĩa |
|---|---|
| Transient | Instance mới khi resolve bình thường |
| Scoped | Một instance trong scope; request scope thường là HTTP request |
| Singleton | Một instance cho container |

`AddDbContext` thông thường đăng ký scoped. **Captive dependency:** Singleton giữ scoped `DbContext` là lỗi lifetime; với worker sử dụng scope factory hoặc DbContext factory. **DI là kỹ thuật, DIP là nguyên tắc** — không đồng nghĩa.

---

# PHẦN X. ASP.NET CORE WEB API

## 26. HTTP và REST

Request gồm method, URL, headers, body (khi có). Response gồm status, headers, body.

| HTTP | Thường dùng | Ví dụ |
|---|---|---|
| GET | Đọc | `GET /api/orders/1` |
| POST | Tạo | `POST /api/orders` |
| PUT | Thay thế | `PUT /api/orders/1` |
| PATCH | Sửa một phần | `PATCH /api/orders/1` |
| DELETE | Xóa | `DELETE /api/orders/1` |

GET, PUT, DELETE có semantics idempotent theo chuẩn HTTP; POST không bảo đảm mặc định. Idempotent = lặp request giống nhau có hiệu ứng dự kiến lên server tương tự một lần, không bắt buộc identical responses.

| Code | Diễn giải |
|---|---|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Chưa authenticated hợp lệ |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 500 | Server Error |

**401 vs 403:** 401 thiếu credentials hợp lệ; 403 từ chối quyền truy cập.

### Controller ví dụ

```csharp
[ApiController]
[Route("api/products")]
public class ProductsController : ControllerBase
{
    private readonly AppDbContext _db;
    public ProductsController(AppDbContext db) => _db = db;

    [HttpGet("{id:int}")]
    public async Task<ActionResult<ProductDto>> Get(int id)
    {
        var product = await _db.Products
            .Where(p => p.Id == id)
            .Select(p => new ProductDto(p.Id, p.Name, p.Price))
            .FirstOrDefaultAsync();
        if (product is null) return NotFound();
        return Ok(product);
    }
}
public record ProductDto(int Id, string Name, decimal Price);
```

Controller trực tiếp DbContext là một lựa chọn cho app nhỏ; nghiệp vụ phức tạp có thể tách application service.

### DTO

DTO = Data Transfer Object giúp bảo vệ API contract, tránh expose entity/secret, giảm over-posting và hỗ trợ versioning:

```csharp
public class User
{
    public int Id { get; set; }
    public string Email { get; set; } = "";
    public string PasswordHash { get; set; } = "";
}
public record UserResponse(int Id, string Email);
```

Đánh đổi là mapping và quản lý DTO. Validation:

```csharp
public class CreateProductRequest
{
    [Required] public string Name { get; set; } = "";
    [Range(0.01, 100000000)] public decimal Price { get; set; }
}
```

`[ApiController]` thường trả 400 khi model validation fails. Business validation (uniqueness, state transitions) vẫn phải xử lý riêng.

## 27. Middleware

HTTP pipeline gồm các middleware có thể chạy trước/sau `next` hoặc short-circuit. Thứ tự rất quan trọng:

```csharp
var app = builder.Build();
app.UseHttpsRedirection();
app.UseAuthentication();
app.UseAuthorization();
app.MapControllers();
app.Run();
```

Các middleware khác: exception handling, CORS, routing, rate limiting, static files. Thứ tự phụ thuộc app setup/hosting.

## 28. Authentication, Authorization, JWT

**Authentication:** ai? **Authorization:** được làm gì?

JWT compact có `header.payload.signature` (ví dụ JWS signed). Payload thường chỉ Base64URL encoded, **không được bảo mật khỏi việc đọc**. Không đặt password/secrets vào token claims.

```text
Credentials qua HTTPS
→ Server kiểm tra tài khoản
→ Phát hành access token/claims
→ Client gửi Authorization: Bearer <token>
→ Server kiểm tra signature, issuer, audience, expiration...
→ Authorization kiểm tra role/claim/policy
```

```csharp
[Authorize(Roles = "Admin")]
[HttpDelete("{id:int}")]
public async Task<IActionResult> Delete(int id)
{
    return NoContent(); // Ví dụ skeleton; code thực tế phải xử lý xóa
}
```

**JWT an toàn tuyệt đối?** Không; phụ thuộc transport HTTPS, signature/key, validation, storage, access controls. **Thu hồi JWT?** Self-contained token thường vẫn hiệu lực đến expiration nếu không có revocation mechanism; dùng short-lived tokens, refresh rotation, denylist/session control theo yêu cầu. **JWT vs Session?** JWT là token format, session là session-state concept; có thể phối hợp.

## 29. SignalR

ASP.NET Core SignalR cho server push real-time, ưu tiên WebSockets khi thích hợp, có fallback tùy điều kiện.

```csharp
public class KitchenHub : Hub
{
    public async Task JoinKitchen(string restaurantId)
    {
        // TODO: Phải xác thực và kiểm tra quyền restaurantId
        await Groups.AddToGroupAsync(Context.ConnectionId, $"kitchen-{restaurantId}");
    }
}
```

Không tin `restaurantId` từ client khi chưa authorize.

```csharp
public class OrderNotifier
{
    private readonly IHubContext<KitchenHub> _hub;
    public OrderNotifier(IHubContext<KitchenHub> hub) => _hub = hub;

    public Task NotifyNewOrderAsync(int restaurantId, int orderId)
    {
        return _hub.Clients.Group($"kitchen-{restaurantId}")
            .SendAsync("NewOrder", new { orderId });
    }
}
```

SignalR không thay thế REST và không phải durable message queue. Cần reconnect, sync API sau mất kết nối; nếu cần delivery guarantee phải có persistent events, retry/idempotency/ack theo thiết kế.

---

# PHẦN XI. ENTITY FRAMEWORK CORE VÀ SQL SERVER

## 30. EF Core

ORM map .NET objects ↔ relational database, hỗ trợ LINQ, change tracking, migrations, DI.

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; } = "";
    public decimal Price { get; set; }
}
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }
    public DbSet<Product> Products => Set<Product>();
}
var products = await dbContext.Products
    .Where(p => p.Price > 20000m)
    .ToListAsync();
```

| Ưu | Hạn chế |
|---|---|
| Bớt SQL boilerplate | Query vẫn có thể rất chậm |
| LINQ type safety | Phải hiểu SQL generated |
| Tracking/migrations | Overhead, migration management |
| Tốt với ASP.NET Core | Không thay thế SQL knowledge |

## 31. Change tracking và `AsNoTracking`

```csharp
var product = await dbContext.Products.FirstAsync(p => p.Id == 1);
product.Price = 50000m;
await dbContext.SaveChangesAsync();
```

Read-only:

```csharp
var products = await dbContext.Products
    .AsNoTracking()
    .Select(p => new ProductDto(p.Id, p.Name, p.Price))
    .ToListAsync();
```

Tracking giúp update, có overhead. No-tracking tránh theo dõi entity instances trả về; nhưng projection chỉ DTO scalars như trên thường vốn không chứa tracked entity nên không cam kết tăng tốc đáng kể trong mọi trường hợp.

## 32. N+1

Một query lấy 100 orders, sau đó mỗi order lại query lấy items = 101 queries, tốn round trips. Có thể dùng DTO projection, eager loading, điều chỉnh query:

```csharp
var orders = await dbContext.Orders
    .Include(o => o.OrderItems)
    .ToListAsync();
```

`Include` nhiều collections có thể dẫn đến cartesian explosion; cân nhắc `AsSplitQuery`, paging, projection, kiểm tra generated SQL.

## 33. Transaction

Một `SaveChanges()` thông thường transactional khi provider hỗ trợ:

```csharp
dbContext.Orders.Add(order);
dbContext.OrderItems.AddRange(items);
await dbContext.SaveChangesAsync();
```

Manual transaction khi thực sự cần nhiều bước:

```csharp
await using var tx = await dbContext.Database.BeginTransactionAsync();
try
{
    // Thao tác ghi database
    await dbContext.SaveChangesAsync();
    await tx.CommitAsync();
}
catch
{
    await tx.RollbackAsync();
    throw;
}
```

Cân nhắc isolation, retries/execution strategies, transaction duration; không tự động mở manual transaction cho mọi trường hợp.

## 34. ACID / Concurrency

| | Ý nghĩa |
|---|---|
| Atomicity | Commit/rollback thống nhất nhóm thao tác |
| Consistency | Giữ constraints theo transaction |
| Isolation | Kiểm soát tương tác giữa transactions đồng thời |
| Durability | Dữ liệu commit bền vững theo DB guarantees |

Hai client cùng cập nhật một order có thể ghi đè trạng thái. Một giải pháp là optimistic concurrency token (`rowversion` trên SQL Server):

```csharp
public class Order
{
    public int Id { get; set; }
    [Timestamp]
    public byte[] RowVersion { get; set; } = [];
}
```

EF Core có thể ném `DbUpdateConcurrencyException` khi nhận ra xung đột update; xử lý bằng reload/retry hoặc báo user theo nghiệp vụ.

## 35. SQL

**Primary Key** duy nhất và NOT NULL. **Foreign Key** enforce reference integrity.

```sql
CREATE TABLE Orders
(
    Id INT PRIMARY KEY,
    CustomerId INT NOT NULL,
    CreatedAt DATETIME2 NOT NULL
);
CREATE TABLE OrderItems
(
    Id INT PRIMARY KEY,
    OrderId INT NOT NULL,
    Quantity INT NOT NULL,
    FOREIGN KEY (OrderId) REFERENCES Orders(Id)
);
```

**INNER JOIN** trả match; **LEFT JOIN** giữ rows bên trái:

```sql
SELECT o.Id, oi.Quantity
FROM Orders o
INNER JOIN OrderItems oi ON o.Id = oi.OrderId;

SELECT o.Id, oi.Quantity
FROM Orders o
LEFT JOIN OrderItems oi ON o.Id = oi.OrderId;
```

**Index:**

```sql
CREATE INDEX IX_Orders_CustomerId ON Orders(CustomerId);
```

Giúp một số filter/join/order nhưng tốn storage và write maintenance, không nên index mọi cột.

**SQL Injection:** Không ghép chuỗi input thành query:

```csharp
// Rủi ro:
string sql = "SELECT * FROM Users WHERE Name = '" + userInput + "'";

// LINQ provider sẽ xử lý tham số hóa khi dùng đúng:
var user = await dbContext.Users.FirstOrDefaultAsync(u => u.Name == userInput);
```

Với raw SQL (`FromSqlRaw`, ...), vẫn phải parameterize và không nối input không đáng tin cậy.

---

# PHẦN XII. BẢO VỆ DỰ ÁN TRONG CV

## 36. Boarding House Management System

Theo CV: ASP.NET Core MVC, SQL Server; quản lý phòng, đăng ký, phân quyền cơ bản Admin/User.

**MVC là gì?** Model biểu diễn dữ liệu/domain; View render UI (Razor); Controller nhận HTTP request và điều phối xử lý.

**Bấm Thêm phòng:** Browser gửi HTTP → routing/model binding/validation → controller → thao tác dữ liệu/service → lưu DB → return View/Redirect theo thiết kế. Cần validate dữ liệu và quyền server-side.

**Tại sao redirect sau POST?** Post/Redirect/Get giảm resubmission khi refresh browser; không phải mọi POST đều redirect, API có contract khác.

**Bảo vệ Admin:** Server-side authorization, không chỉ ẩn nút Admin trong HTML. Có thể tự gửi HTTP request nếu chỉ ẩn UI.

## 37. Restaurant Management System

Theo CV: POS, QR ordering, dashboard; Web API, EF Core, JWT role auth, SignalR KitchenHub, ReactJS.

1. **Web API thay vì server-render MVC?** React client cần giao tiếp backend qua APIs, hỗ trợ tách frontend/backend, nhưng thêm CORS, deployment, auth và versioning concerns.
2. **DTO?** Kiểm soát API payload và tránh lộ entity/secret.
3. **JWT thực tế ở đâu?** Chỉ ra login endpoint, credential validation, token creation, issuer/audience/claims/lifetime, bearer middleware, `[Authorize]`, cách React gửi token. Phải kiểm tra source trước khi nhận mình triển khai đủ.
4. **KitchenHub?** Client kết nối Hub, được authorize/group đúng, backend gửi event, React lắng nghe rồi update hoặc gọi API; xử lý reconnect/missed events.
5. **Hai nhân viên đồng thời sửa order?** State transitions, transaction, optimistic concurrency, conflict handling; EF Core không giải quyết trọn nghiệp vụ tự động.
6. **Làm lại dự án?** Tách trách nhiệm nơi có logic phức tạp, test, centralized error handling, concurrency, tối ưu dựa trên benchmark; không thêm architecture chỉ vì xu hướng.

**Ví dụ trả lời:**

> Em muốn tổ chức rõ hơn trách nhiệm giữa Controller, nghiệp vụ và truy cập dữ liệu tại những module có logic phức tạp. Em cũng muốn bổ sung unit tests, integration tests, xử lý lỗi tập trung, kiểm tra concurrency khi thay đổi trạng thái đơn hàng và đo hiệu năng các query quan trọng trước khi tối ưu. Em không muốn thêm architecture phức tạp chỉ vì xu hướng, mà dựa trên nhu cầu thực tế của dự án.

---

# PHẦN XIII. BỘ CÂU HỎI PHỎNG VẤN ĐÀO SÂU

## 38. Mini Mock Interview — 12 câu trắc nghiệm có đáp án

> Phần này được chuyển từ giao diện trắc nghiệm tương tác sang văn bản tĩnh: đầy đủ câu hỏi, 4 lựa chọn, đáp án và giải thích.

**Câu 1.** Hai biến cùng tham chiếu một object class. Thay đổi property của object qua biến thứ hai thì sao?

- A. Biến thứ nhất không bị ảnh hưởng
- B. Cả hai nhìn thấy sự thay đổi
- C. Compiler báo lỗi
- D. Tạo object mới tự động

**Đáp án: B.** Phép gán reference type sao chép tham chiếu. Hai biến có thể cùng trỏ đến một object.

**Câu 2.** Phát biểu nào đúng về readonly field tham chiếu tới một `List<int>`?

- A. List không thể Add
- B. Không thể gán lại field sau khởi tạo hợp lệ nhưng có thể Add phần tử
- C. Giống const
- D. Luôn là static

**Đáp án: B.** Readonly hạn chế phép gán vào field chứ không làm immutable object được tham chiếu.

**Câu 3.** Trong một lời gọi virtual method đã được override, implementation được chọn theo yếu tố nào?

- A. Chỉ kiểu khai báo biến
- B. Kiểu runtime của object
- C. Tên namespace
- D. Access modifier của caller

**Đáp án: B.** Virtual dispatch chọn implementation phù hợp dựa trên runtime type.

**Câu 4.** Overloading có thể phân biệt chỉ bằng return type không?

- A. Có
- B. Không
- C. Chỉ trong abstract class
- D. Chỉ với async

**Đáp án: B.** Return type đơn thuần không đủ tạo overload hợp lệ.

**Câu 5.** C# class có thể làm việc nào?

- A. Kế thừa trực tiếp hai class
- B. Implement nhiều interface
- C. Kế thừa một struct
- D. Thay đổi base class lúc runtime

**Đáp án: B.** C# hỗ trợ single class inheritance nhưng có thể implement nhiều interface.

**Câu 6.** Giải thích nào đúng nhất về Value Type?

- A. Luôn trên stack
- B. Luôn nằm trong CPU register
- C. Có value semantics; phép gán thông thường copy giá trị
- D. Không bao giờ boxing

**Đáp án: C.** Vị trí lưu trữ phụ thuộc runtime context; value semantics là đặc điểm nền tảng.

**Câu 7.** Nếu biến Animal chứa Dog, extension overload theo Animal và Dog, lời gọi qua biến Animal ưu tiên loại nào?

- A. Dog
- B. Animal
- C. Ngẫu nhiên
- D. Không compile được

**Đáp án: B.** Extension overload resolution tĩnh theo compile-time type.

**Câu 8.** Scoped service trong ASP.NET Core thường có vòng đời nào?

- A. Một instance trong mỗi request scope
- B. Một instance cho toàn bộ ứng dụng
- C. Mới trong mỗi property access
- D. Một instance cho mọi máy chủ

**Đáp án: A.** HTTP request thường có dependency injection scope riêng.

**Câu 9.** `FirstOrDefault` khác `SingleOrDefault` thế nào?

- A. Hoàn toàn giống nhau
- B. SingleOrDefault báo lỗi nếu nhiều kết quả
- C. FirstOrDefault luôn nhanh hơn
- D. SingleOrDefault luôn trả phần tử cuối

**Đáp án: B.** SingleOrDefault kiểm tra có tối đa một phần tử hợp lệ.

**Câu 10.** `AsNoTracking` được sử dụng chủ yếu để làm gì?

- A. Tự tạo index
- B. Không theo dõi các entity được trả về trong query
- C. Tự rollback
- D. Tắt kết nối database

**Đáp án: B.** No-tracking queries thường thích hợp cho đọc dữ liệu.

**Câu 11.** `async/await` có luôn tạo một thread mới không?

- A. Luôn luôn
- B. Chỉ trên Linux
- C. Không nhất thiết
- D. Chỉ trên Windows

**Đáp án: C.** I/O async có thể không cần giữ thread bận trong khi đợi.

**Câu 12.** HTTP 403 thường biểu thị điều gì?

- A. Không tìm thấy tài nguyên
- B. Server lỗi
- C. Quyền truy cập bị từ chối
- D. Tạo thành công

**Đáp án: C.** 403 = Forbidden, khác 401 liên quan authentication.

## 39. 30 câu tự luận Senior có thể dùng

| Câu hỏi | Trọng tâm |
|---|---|
| 1. Bốn tính chất OOP là gì? | Định nghĩa, ví dụ |
| 2. Encapsulation khác Abstraction? | Bản chất |
| 3. Override khác Overload? | Compile vs runtime |
| 4. virtual, abstract, new, override? | Kế thừa |
| 5. Interface vs Abstract Class? | Thiết kế |
| 6. Composition vs Inheritance? | Coupling |
| 7. const vs readonly vs static? | Init và scope |
| 8. Value type luôn trên stack? | Memory |
| 9. String là value/reference? | Immutability |
| 10. Boxing/Unboxing? | Runtime conversions |
| 11. Class vs Struct? | Semantics |
| 12. Enum có thể mang giá trị chưa khai báo? | Enum behavior |
| 13. ref/out/in? | Parameter passing |
| 14. var vs dynamic? | Binding |
| 15. Extension method override được không? | Static resolution |
| 16. IEnumerable vs IQueryable? | EF/LINQ |
| 17. LINQ deferred execution? | Timing |
| 18. async có tạo thread mới? | I/O |
| 19. Scoped vs Singleton? | DI |
| 20. DbContext không thread-safe? | Concurrency |
| 21. DTO vs Entity? | API design |
| 22. 401 vs 403? | Auth |
| 23. JWT mã hóa không? | Token security |
| 24. SignalR vs polling? | Real-time |
| 25. N+1 query? | Performance |
| 26. Transaction? | Consistency |
| 27. Index lợi hại? | Optimization |
| 28. Unit testing để làm gì? | Testability |
| 29. Tạo đơn bị gửi trùng? | Idempotency/concurrency |
| 30. Thiết kế lại dự án? | Judgment |

---

# PHẦN XIV. NHỮNG SAI LẦM KHI PHỎNG VẤN INTERN

| Chưa tốt | Chính xác hơn |
|---|---|
| Value Type = stack; Reference Type = heap | Semantics là gốc; vị trí bộ nhớ tùy context |
| Encapsulation chỉ private | Bảo vệ invariant bằng API |
| Interface không thể có body | C# hiện đại có default interface implementations |
| Readonly làm object immutable | Field không gán lại; object vẫn mutable |
| Async làm mọi thứ nhanh hơn | Async giúp scalability khi chờ I/O |
| JWT mã hóa nên an toàn | Signed JWT thường chỉ encoded payload |
| EF Core tự tối ưu mọi query | Phải xem SQL, query plan, index, tracking |
| SignalR luôn gửi thành công | Reconnect, đồng bộ trạng thái, missed events |
| Càng nhiều interface càng sạch | Abstraction khi có giá trị, tránh overengineering |

## 40. Khi không biết câu trả lời

Không giả vờ đã triển khai. Nói rõ phạm vi biết và cách kiểm chứng.

**Ví dụ interviewer hỏi transactional outbox:**

> Em chưa có kinh nghiệm trực tiếp triển khai transactional outbox, nhưng theo hiểu biết của em, pattern này được dùng để xử lý vấn đề giữa việc commit database và phát hành sự kiện. Thay vì ghi database rồi gửi sự kiện như hai bước độc lập, hệ thống lưu business data và outbox event trong cùng transaction. Sau đó một process khác đọc outbox và thực hiện gửi. Em cũng hiểu rằng consumer thường cần xử lý trùng lặp khi retry. Đây là hướng em muốn tìm hiểu và áp dụng khi dự án cần độ tin cậy cao hơn.

---

# PHẦN XV. CHECKLIST CUỐI CÙNG TRƯỚC BUỔI PHỎNG VẤN

- [ ] Giới thiệu bản thân trong 60–90 giây mà không đọc CV.
- [ ] Giải thích được bốn tính chất OOP bằng ví dụ Order/Payment.
- [ ] Viết ví dụ override, overload, virtual, new.
- [ ] Phân biệt interface, abstract class, inheritance, composition.
- [ ] Giải thích value/reference type, string, boxing, stack/heap.
- [ ] Phân biệt const, readonly, static, static readonly.
- [ ] Giải thích class, struct, enum và access modifiers.
- [ ] Viết extension method và hiểu giới hạn.
- [ ] Nắm ref, out, in, generic, collections.
- [ ] Giải thích LINQ, IEnumerable, IQueryable.
- [ ] Hiểu async/await, Task, CancellationToken.
- [ ] Trình bày DI lifetimes và SOLID.
- [ ] Giải thích HTTP request đi qua ASP.NET Core API.
- [ ] Hiểu DTO, EF tracking, SQL joins, indexes, transaction.
- [ ] Giải thích JWT authentication và role authorization.
- [ ] Trình bày KitchenHub và cập nhật realtime.
- [ ] Mở source code và giải thích module đã viết.
- [ ] Chuẩn bị một bug thực tế và cách debug.
- [ ] Chuẩn bị cải tiến kỹ thuật nếu làm lại dự án.
- [ ] Luyện phỏng vấn thành tiếng ít nhất hai lượt.

## 41. Phương pháp luyện 4 bước

1. **Giải thích** khái niệm không nhìn tài liệu.
2. **Viết và chạy code**: nhất là override/new, reference assignment, readonly.
3. **So sánh và đánh đổi**: khi dùng, khi không, maintainability/performance.
4. **Liên hệ dự án**: chỉ ra source code thật, luồng chạy, điểm cải thiện.

Ví dụ Encapsulation: đừng chỉ nói “che giấu dữ liệu”; hãy giải thích vì sao Order.Status không thể tùy tiện đổi, Confirm() bảo vệ trạng thái ra sao và concurrency giữa hai request được giải quyết thế nào.

**Nhớ:** Với Intern, khả năng giải thích chính xác khái niệm cơ bản, minh họa bằng code và liên hệ code dự án thường có giá trị hơn thuộc lòng nhiều thuật ngữ kiến trúc nâng cao.

## Tài liệu tham khảo và đối chiếu

- [C# documentation — Microsoft Learn](https://learn.microsoft.com/dotnet/csharp/)
- [C# language reference](https://learn.microsoft.com/dotnet/csharp/language-reference/)
- [ASP.NET Core documentation](https://learn.microsoft.com/aspnet/core/)
- [Entity Framework Core](https://learn.microsoft.com/ef/core/)
- [ASP.NET Core SignalR](https://learn.microsoft.com/aspnet/core/signalr/introduction)
- [GitHub repository được ghi trong CV: RestaurantManagement.API](https://github.com/BaoPhuc2k3/RestaurantManagement.API)

> **Ghi chú:** Đây là tài liệu học/ôn tập. Các snippet trong những mục khác nhau có thể khai báo lại cùng tên class (`Product`, `Order`, `Parent`...) và một số snippet là pseudocode/skeleton, vì vậy không dán nguyên toàn bộ các ví dụ vào cùng một project để compile; hãy chạy từng ví dụ trong context phù hợp và thêm namespace/using/dependencies cần thiết.

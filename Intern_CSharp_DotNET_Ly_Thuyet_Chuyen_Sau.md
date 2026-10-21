# GIÁO TRÌNH LÝ THUYẾT CHUYÊN SÂU PHỎNG VẤN INTERN C#/.NET

> **Tài liệu thứ hai — học bản chất để trả lời phỏng vấn, không chỉ ghi nhớ định nghĩa.**  
> Độc lập với [Cẩm nang tổng hợp](./Intern_CSharp_DotNET_Interview_Handbook.md). Các đoạn code là ví dụ minh họa riêng lẻ; trừ khi được ghi rõ, chúng không phải các file được ghép thành một chương trình chạy độc lập.

## Cách sử dụng giáo trình

Với **mỗi khái niệm**, hãy tự trả lời theo năm lớp: **(1) định nghĩa đúng, (2) cơ chế hoạt động, (3) ví dụ, (4) khi nào dùng và đánh đổi, (5) một lỗi/bẫy thực tế**. Hãy đọc một chủ đề, đóng tài liệu và nói thành tiếng 2–3 phút; sau đó tự viết ví dụ mà không sao chép.

**Nguồn phạm vi:** Các đề mục *giới thiệu bản thân; dự án đã làm; polymorphism; encapsulation, getter/setter và access modifiers; abstraction, interface/abstract; inheritance và override/overload; value/reference type; const/readonly/static, biến/hàm; struct/enum/class; extension methods* đến từ **ảnh chủ đề phỏng vấn**. Hai dự án *quản lý nhà trọ* và *quản lý nhà hàng* là nội dung **CV cung cấp**. Các phần CLR, garbage collector, SOLID, DI, LINQ, async, HTTP, EF Core, SQL, JWT, SignalR, testing là **kiến thức đào sâu bổ sung** để chuẩn bị hỏi xoáy; không có nghĩa nhà tuyển dụng đã cam kết hỏi các phần này. Ví dụ code dưới đây là ví dụ giảng giải, không khẳng định là implementation trong repository cá nhân.

## Mục lục

1. [Cách giới thiệu bản thân và kể dự án có chiều sâu](#1-cách-giới-thiệu-bản-thân-và-kể-dự-án-có-chiều-sâu)
2. [OOP: gốc rễ, class, object và bốn tính chất](#2-oop-gốc-rễ-class-object-và-bốn-tính-chất)
3. [Encapsulation và Access Modifiers](#3-encapsulation-và-access-modifiers)
4. [Abstraction, Interface và Abstract Class](#4-abstraction-interface-và-abstract-class)
5. [Inheritance, Polymorphism, Overload, Override](#5-inheritance-polymorphism-overload-override)
6. [C# type system: Value, Reference, Stack, Heap, Boxing](#6-c-type-system-value-reference-stack-heap-boxing)
7. [const, readonly, static; biến, property, constructor, method](#7-const-readonly-static-biến-property-constructor-method)
8. [Class, Struct, Enum, Record và immutability](#8-class-struct-enum-record-và-immutability)
9. [Extension Method, Generic, Delegate, Event](#9-extension-method-generic-delegate-event)
10. [Collection, LINQ và IQueryable](#10-collection-linq-và-iqueryable)
11. [Exception, GC, IDisposable và async/await](#11-exception-gc-idisposable-và-asyncawait)
12. [SOLID, DI, ASP.NET Core và REST](#12-solid-di-aspnet-core-và-rest)
13. [EF Core, SQL, Transaction và Concurrency](#13-ef-core-sql-transaction-và-concurrency)
14. [Authentication, JWT, SignalR và an toàn](#14-authentication-jwt-signalr-và-an-toàn)
15. [Testing, Git, Debugging và trả lời tình huống](#15-testing-git-debugging-và-trả-lời-tình-huống)
16. [Ngân hàng câu hỏi có mẫu trả lời dài](#16-ngân-hàng-câu-hỏi-có-mẫu-trả-lời-dài)
17. [Kế hoạch ôn tập và checklist](#17-kế-hoạch-ôn-tập-và-checklist)

---

# 1. Cách giới thiệu bản thân và kể dự án có chiều sâu

## 1.1. Người phỏng vấn đánh giá điều gì?

Một phần giới thiệu tốt không phải là đọc lại mọi dòng CV. Nhà tuyển dụng muốn xác định: bạn có hiểu vai trò mình ứng tuyển không; kỹ năng nào có bằng chứng; bạn đã đóng góp đến đâu; bạn có thể phân tích vấn đề, nhận feedback và học hỏi không. Với vị trí Intern, **trung thực về mức độ hiểu biết** quan trọng hơn liệt kê nhiều công nghệ.

Cấu trúc gợi ý 60–90 giây: **đang học gì → định hướng backend C#/.NET → dự án MVC → dự án API/SignalR → kiến thức đã rút ra → mong muốn học trong môi trường thực tế**. Câu trả lời nên được nói tự nhiên, không đọc như văn bản.

**Mẫu trả lời:**

> Em là sinh viên CNTT, định hướng Backend với C# và ASP.NET Core. Em đã làm một dự án quản lý nhà trọ sử dụng ASP.NET Core MVC và SQL Server để học routing, controller, view, CRUD và thiết kế dữ liệu quan hệ. Sau đó em phát triển phần backend cho một hệ thống quản lý nhà hàng với Web API, EF Core, DTO, JWT và SignalR; em cũng tích hợp một số giao diện React gọi API. Qua các dự án, em thấy rõ hơn sự khác biệt giữa làm chức năng chạy được và làm chức năng dễ bảo trì, có kiểm soát lỗi và bảo mật. Em mong muốn được cải thiện code review, testing, thiết kế API và phối hợp nhóm trong kỳ thực tập.

Đừng khẳng định bạn đã giải quyết concurrency, áp dụng Clean Architecture đúng nghĩa hoặc có hệ thống production nếu bạn chưa làm được. Nếu CV ghi *Clean Architecture* ở mục kỹ năng nhưng mô tả một dự án trực tiếp Model–Controller, hãy sẵn sàng giải thích **bạn biết nguyên tắc ở mức nào** và **dự án thực tế áp dụng ở mức nào**.

## 1.2. Cách phân tích mỗi dự án theo kỹ thuật

Dùng khuôn **Bối cảnh → Kiến trúc → Luồng dữ liệu → Quyết định → Khó khăn → Điều sẽ cải tiến**. Để bảo vệ dự án quản lý nhà hàng, bạn phải có thể mở source và chỉ ra:

1. Route nhận `POST /api/orders`, request DTO và validation ở đâu?
2. Dữ liệu đơn được map sang entity và lưu bằng `DbContext` như thế nào?
3. Làm sao biết user được quyền tạo/đổi trạng thái đơn? JWT được phát hành và validate ở đâu?
4. Thông báo SignalR được gửi ở đâu, đến client nào; nếu gửi thất bại thì sao?
5. React lấy danh sách đơn lần đầu bằng API ra sao, nhận sự kiện mới rồi cập nhật gì?
6. Nếu thêm món không tồn tại, giá âm, quantity bằng 0 hoặc request trùng thì hệ thống phản ứng thế nào?

Đó là **câu hỏi để bạn tự kiểm tra code**, không phải những tính năng đã được xác minh trong source. Hãy trả lời đúng theo triển khai của mình, sau đó mới đề xuất kiến trúc tốt hơn.

**Tình huống phỏng vấn:** "Tại sao lưu đơn xong lại cần SignalR?" Trả lời: database là source of truth; SignalR phát một tín hiệu thời gian thực để màn hình bếp cập nhật mà không cần polling liên tục. Bản thân SignalR không đảm bảo client online hoặc nhận được mọi message; khi reconnect client nên tải lại trạng thái bằng API. Nếu độ tin cậy thông báo là nghiệp vụ quan trọng, có thể cân nhắc outbox/event processing, nhưng đó là thiết kế nâng cao chứ không nhất thiết đã dùng.

---

# 2. OOP: gốc rễ, class, object và bốn tính chất

## 2.1. Vấn đề mà OOP giải quyết

Khi một chương trình gồm nhiều chức năng liên quan đến khách hàng, sản phẩm, đơn hàng, nếu đặt toàn bộ dữ liệu vào biến toàn cục và xử lý trong những hàm rời rạc, bất kỳ phần nào cũng có thể sửa trạng thái ngoài ý muốn. OOP cung cấp một cách **mô hình hóa domain thành các đối tượng có dữ liệu và hành vi**, giúp tổ chức trách nhiệm và các quan hệ. Tuy nhiên, OOP không thay thế tư duy thuật toán, thiết kế dữ liệu hoặc nguyên tắc tách module.

**Class** là định nghĩa về một loại object: thành viên, constructor và hành vi. **Object/instance** là một thực thể cụ thể được tạo theo định nghĩa ấy. **State** là trạng thái quan sát được (ví dụ `Status`, `Total`); **behavior** là hành động (ví dụ `Confirm`, `Cancel`). **Identity** là tính phân biệt hai thực thể, ngay cả khi chúng có giá trị field bằng nhau.

```csharp
public class Order
{
    public int Id { get; }
    public string CustomerName { get; }
    public decimal Total { get; private set; }

    public Order(int id, string customerName)
    {
        if (string.IsNullOrWhiteSpace(customerName))
            throw new ArgumentException("Customer required");
        Id = id;
        CustomerName = customerName;
    }

    public void AddAmount(decimal amount)
    {
        if (amount <= 0) throw new ArgumentOutOfRangeException(nameof(amount));
        Total += amount;
    }
}

var first = new Order(1, "An");
first.AddAmount(25000m);
var alias = first;  // Cùng object
var second = new Order(1, "An"); // Object khác
Console.WriteLine(ReferenceEquals(first, alias));  // True
Console.WriteLine(ReferenceEquals(first, second)); // False
```

Đừng suy ra rằng vì `Id` giống nhau thì hai reference trỏ tới cùng instance. Identity ở database và identity của object trong RAM là hai khái niệm liên quan nhưng khác nhau.

## 2.2. Bốn tính chất OOP — tổng quan chính xác

- **Encapsulation:** Gom trạng thái và hành vi liên quan, kiểm soát quyền truy cập và bảo vệ invariant.
- **Abstraction:** Phơi bày contract/mô hình cần thiết và ẩn đi chi tiết triển khai không quan trọng đối với caller.
- **Inheritance:** Derived class nhận và có thể chuyên biệt hóa những thành viên có thể kế thừa từ base class, diễn tả quan hệ *is-a* phù hợp.
- **Polymorphism:** Nhiều implementation/cách xử lý được sử dụng qua một giao diện/contract hoặc tên thao tác chung.

Không nên chỉ nói "đóng gói là private, trừu tượng là interface, kế thừa là dấu hai chấm, đa hình là override": đó mới là *cú pháp*, chưa mô tả được bản chất.

## 2.3. OOP và anemic domain model

Nếu mọi class chỉ chứa getter/setter và toàn bộ quy tắc nghiệp vụ nằm trong service, ta có thể đang sử dụng **anemic domain model**. Cách này không phải luôn sai — các ứng dụng CRUD nhỏ có thể đơn giản và dễ theo dõi — nhưng với domain có quy tắc chuyển trạng thái, đặt invariant trong entity hoặc domain service phù hợp có thể giúp tránh bỏ sót validation.

**Ưu:** module rõ ràng, dễ phối hợp, abstraction cho dependency. **Nhược:** có nguy cơ tạo quá nhiều layer, interface, inheritance không có lợi ích và code khó theo dõi. Quan trọng là giải thích vì sao thiết kế phù hợp **mức độ phức tạp thực tế**.

---

# 3. Encapsulation và Access Modifiers

## 3.1. Encapsulation không đồng nghĩa giấu hết dữ liệu

Một object đúng nghĩa không nhất thiết có mọi property `private`. Mục tiêu là cho caller đủ khả năng thực hiện hành động hợp lệ mà không làm hỏng trạng thái. Ví dụ đơn `Cancelled` không thể chuyển thành `Paid` chỉ bởi một controller gán chuỗi vào `Status`.

```csharp
public enum OrderStatus { Pending, Confirmed, Cancelled }

public sealed class Order
{
    public OrderStatus Status { get; private set; } = OrderStatus.Pending;

    public void Confirm()
    {
        if (Status != OrderStatus.Pending)
            throw new InvalidOperationException("Only pending orders can be confirmed");
        Status = OrderStatus.Confirmed;
    }

    public void Cancel()
    {
        if (Status != OrderStatus.Pending)
            throw new InvalidOperationException("Only pending orders can be cancelled");
        Status = OrderStatus.Cancelled;
    }
}
```

**Invariant** là điều kiện luôn phải đúng đối với một đối tượng trong các trạng thái hợp lệ (ví dụ tiền không âm, trạng thái chuyển đúng luật). Nếu cho bên ngoài set trực tiếp `Status`, mọi caller phải tự nhớ kiểm tra quy tắc, dẫn đến duplication và bug. Chuyển trạng thái qua method tập trung quy tắc ở một nơi.

**Đào sâu:** `private set` có đủ bảo vệ database không? Không. Các request chạy đồng thời có thể đọc cùng một trạng thái cũ; validation trong RAM không thay thế optimistic concurrency token, transaction hoặc conditional update trong database.

## 3.2. Field vs Property vs Method

```csharp
public class Product
{
    private decimal _price; // field: dữ liệu nội bộ

    public decimal Price // property: public API có logic kiểm tra
    {
        get => _price;
        private set
        {
            if (value < 0) throw new ArgumentOutOfRangeException(nameof(value));
            _price = value;
        }
    }

    public Product(decimal price) => Price = price;
    public void ChangePrice(decimal newPrice) => Price = newPrice;
}
```

**Field** là ô lưu dữ liệu. **Property** là member cho cú pháp đọc/ghi có thể chứa accessor logic; auto-property có backing field do compiler tạo. **Method** diễn tả một hành động với tên nghiệp vụ và thường là nơi tốt hơn để thay đổi trạng thái có ràng buộc phức tạp.

Một property `public get; private set;` cho phép đọc từ bên ngoài nhưng giới hạn vị trí được gán; một read-only interface không tự làm dữ liệu sâu bên trong immutable.

## 3.3. Các access modifiers và phạm vi

| Modifier | Thành viên được truy cập từ đâu? | Ứng dụng |
|---|---|---|
| `public` | Mọi code truy cập được type/member hợp lệ | Hợp đồng API cho client/library |
| `private` | Bên trong containing type | Field và helper nội bộ |
| `protected` | Type chứa và derived types theo quy tắc C# | Điểm mở rộng trong base class |
| `internal` | Cùng assembly (trừ cơ chế đặc biệt như `InternalsVisibleTo`) | Che implementation trong library |
| `protected internal` | Cùng assembly **hoặc** derived type ngoài assembly | API cho internal code và extensions |
| `private protected` | Containing/derived types trong cùng assembly | Kế thừa nhưng giới hạn assembly |

**Assembly** thường tương ứng với output `.dll`/`.exe` của project; *namespace* không phải assembly. Hai class cùng namespace ở hai project khác nhau không đương nhiên truy cập được member `internal` của nhau.

**Điểm tinh tế:** `protected` không có nghĩa "truy cập từ mọi instance của base class trong code lớp con". C# còn ràng buộc cách truy cập protected instance member từ bên ngoài assembly, nên giải thích bằng *loại truy cập* chứ không đơn giản "lớp con thấy mọi thứ".

## 3.4. Ưu điểm và trade-off

- **Ưu:** ràng buộc business rule; thay đổi implementation mà không sửa caller; ngăn nhiều loại invalid state; test nghiệp vụ dễ hơn.
- **Chi phí:** phải thiết kế public API; có thể sinh boilerplate; không thay thế validation HTTP, authorization, transaction hoặc database constraints.
- **Khi dùng:** tất cả entity có invariant, lớp thư viện muốn che implementation, stateful components.
- **Khi không phức tạp hóa:** DTO dùng để truyền dữ liệu thường có public/init properties theo nhu cầu serializer; không cần tạo `ChangeName()` cho mỗi DTO đơn giản.

**Mẫu trả lời phỏng vấn (60 giây):**

> Encapsulation là việc tổ chức dữ liệu cùng hành vi liên quan trong object và kiểm soát cách bên ngoài thay đổi trạng thái để luôn thỏa business rules. C# hỗ trợ thông qua private fields, properties, access modifiers và methods. Chẳng hạn Order có Status với private setter, muốn xác nhận phải gọi Confirm(), nơi kiểm tra trạng thái hiện tại. Nhờ đó các controller không tự ý gán trạng thái sai. Điểm em lưu ý là đóng gói không tự xử lý vấn đề hai request đồng thời; điều đó còn cần concurrency control ở database.

**Câu hỏi nối tiếp:** Getter/setter công khai có phải encapsulation không? — Có mức đóng gói về mặt cú pháp, nhưng nếu setter mở toàn bộ mutable state thì chưa bảo vệ invariant. `internal` khác `protected`? — `internal` theo assembly, `protected` theo inheritance.

---

# 4. Abstraction, Interface và Abstract Class

## 4.1. Abstraction giải quyết vấn đề gì?

Giả sử controller tạo đơn cần lưu vào database. Nếu controller tự xây connection string, câu SQL, mở connection rồi gửi SignalR, nó phụ thuộc quá nhiều chi tiết. Khi thay đổi phương thức lưu, controller cũng phải thay. Abstraction cung cấp hợp đồng phù hợp: caller yêu cầu "tạo đơn", còn chi tiết nằm phía dưới.

```csharp
public interface IOrderService
{
    Task<int> CreateAsync(CreateOrderRequest request, CancellationToken ct);
}

public sealed class OrdersController : ControllerBase
{
    private readonly IOrderService _service;
    public OrdersController(IOrderService service) => _service = service;

    [HttpPost("api/orders")]
    public async Task<ActionResult<int>> Create(CreateOrderRequest request, CancellationToken ct)
        => Ok(await _service.CreateAsync(request, ct));
}
```

Ví dụ chỉ minh họa dependency; trong API thực tế có thể trả `201 Created`, validate request và kiểm tra authorization. Phụ thuộc abstraction không có nghĩa mọi service phải có interface: interface nên giúp tách boundary, test hoặc hỗ trợ nhiều implementation thật sự.

## 4.2. Interface: contract, không nhất thiết chỉ là method signature

Interface khai báo một tập member/contract. Một type có thể implement nhiều interface. Trong C# hiện đại, interface còn hỗ trợ default interface methods, static abstract members cho một số generic scenarios, nên phát biểu "interface tuyệt đối không có code" là sai.

```csharp
public interface INotificationSender
{
    Task SendAsync(int userId, string message, CancellationToken ct);
}

public class SignalRNotificationSender : INotificationSender
{
    public Task SendAsync(int userId, string message, CancellationToken ct)
    {
        // Ví dụ minh họa: triển khai thật dùng IHubContext và kiểm tra quyền
        return Task.CompletedTask;
    }
}
```

Không thể `new INotificationSender()`; runtime cần implementation cụ thể. `IServiceCollection` có thể ánh xạ contract sang concrete class khi DI container resolve.

## 4.3. Abstract class

Abstract class không khởi tạo trực tiếp được, nhưng chứa field, constructor, property, common implementation, virtual và abstract method.

```csharp
public abstract class PaymentProcessor
{
    protected PaymentProcessor(string providerName) => ProviderName = providerName;
    protected string ProviderName { get; }

    public void LogStart() => Console.WriteLine($"Start: {ProviderName}");
    public abstract Task PayAsync(decimal amount);
}

public sealed class CashPayment : PaymentProcessor
{
    public CashPayment() : base("Cash") { }
    public override Task PayAsync(decimal amount)
    {
        if (amount <= 0) throw new ArgumentOutOfRangeException(nameof(amount));
        return Task.CompletedTask;
    }
}
```

Một abstract class vẫn có thể có method hoàn chỉnh. Abstract method buộc non-abstract derived class phải implement. Abstract class thích hợp khi các derived types thực sự cùng **is-a** và cần state/implementation chung.

## 4.4. Interface vs Abstract Class — trả lời kỹ

| Góc nhìn | Interface | Abstract class |
|---|---|---|
| Mục đích | Khả năng/hợp đồng sử dụng | Base model có state và hành vi chung |
| Kế thừa nhiều | Type implement nhiều interfaces | Class chỉ có một direct base class |
| Instance state | Không có instance fields | Có instance fields |
| Constructor instance | Không | Có |
| Member implementation | Có thể có default implementation theo phiên bản C# | Có thể có ordinary, virtual, abstract methods |
| Phù hợp | `INotificationSender`, `IRepository` khi có lý do | `PaymentProcessor` nếu có workflow/state chung |

**Bẫy:** Không phải interface luôn linh hoạt hơn abstract class. Default interface implementation có quy tắc dispatch riêng; thay đổi public contract có thể ảnh hưởng binary/source compatibility. Abstract class có thể bảo vệ extension points tốt hơn nếu cần shared protected state, nhưng đưa state vào base class cũng gây coupling.

**Encapsulation vs Abstraction:** Abstraction hỏi "caller cần biết điều gì?", encapsulation hỏi "caller được phép tác động ra sao để trạng thái không hỏng?". Chúng phối hợp nhưng không đồng nhất.

**Mẫu trả lời:**

> Em chọn interface khi cần mô tả một capability, tách module dùng khỏi cách triển khai, hoặc có thể có nhiều implementation như gửi email và SignalR. Em chọn abstract class khi các lớp có quan hệ kế thừa thật sự và chia sẻ state hay thuật toán chung. Không phải lúc nào cũng bắt buộc tạo interface cho mọi class; với project đơn giản, một concrete class có trách nhiệm rõ ràng có thể là lựa chọn hợp lý hơn.

---

# 5. Inheritance, Polymorphism, Overload, Override

## 5.1. Inheritance và nguyên tắc IS-A

`Chef : Employee` là quan hệ *Chef is an Employee* hợp lý nếu domain thực sự nhìn Chef như một nhân viên. `OrderService : SqlRepository` không hợp lý: service **dùng** repository, không **là** repository.

```csharp
public class Employee
{
    public string Name { get; }
    public Employee(string name) => Name = name;
    public virtual string GetRole() => "Employee";
}

public class Chef : Employee
{
    public Chef(string name) : base(name) { }
    public override string GetRole() => "Chef";
}
```

Constructor của base không được "kế thừa" thành constructor của derived, nhưng derived constructor gọi base constructor qua `base(...)`. Một class có tối đa một direct base class, nhưng thực thi nhiều interface.

**Rủi ro:** Fragile base class: sửa một behavior trong base làm nhiều lớp con sai; inheritance hierarchy quá sâu; override làm yếu đi tiền điều kiện hoặc thay đổi hậu điều kiện, phá **Liskov Substitution Principle**. Composition thường linh hoạt khi chỉ cần tái sử dụng một capability.

## 5.2. Runtime Polymorphism

```csharp
Employee employee = new Chef("Minh");
Console.WriteLine(employee.GetRole()); // Chef
```

Kiểu compile-time của biến là `Employee`, kiểu runtime object là `Chef`. `GetRole` virtual, nên call site dùng virtual dispatch tìm most-derived override phù hợp.

**Vì sao có lợi?** Code sử dụng chỉ biết contract chung:

```csharp
void PrintRole(Employee employee) => Console.WriteLine(employee.GetRole());
```

Caller có thể truyền các derived types khác nhau mà không tạo chuỗi `if(type == ...)`. Đổi lại cần bảo đảm mọi implementation tuân thủ contract và tránh dùng inheritance chỉ để giảm code lặp.

## 5.3. Overload: compile-time overload resolution

```csharp
public decimal Total(decimal price) => price;
public decimal Total(decimal price, int quantity) => price * quantity;
public decimal Total(decimal price, int quantity, decimal discountPercent)
    => price * quantity * (1m - discountPercent / 100m);
```

Cùng tên, khác parameter list. Không thể overload chỉ dựa vào return type. Compiler phải xét các conversion, optional/named arguments và các quy tắc chọn overload; phát biểu "compiler chỉ đếm số tham số" là quá đơn giản.

Ví dụ:

```csharp
static void Print(object x) => Console.WriteLine("object");
static void Print(string x) => Console.WriteLine("string");
Print("abc"); // string: candidate cụ thể hơn trong ví dụ này
```

## 5.4. Override và `new` (method hiding)

```csharp
class Parent
{
    public virtual string Speak() => "Parent";
}
class Child : Parent
{
    public override string Speak() => "Child";
}
Parent a = new Child();
Console.WriteLine(a.Speak()); // Child
```

`override` cần base virtual/abstract/override member hợp lệ. `sealed override` có thể chặn các derived types tiếp tục override slot đó.

```csharp
class Base
{
    public string Who() => "Base";
}
class Derived : Base
{
    public new string Who() => "Derived";
}
Base x = new Derived();
Console.WriteLine(x.Who()); // Base
Derived y = new Derived();
Console.WriteLine(y.Who()); // Derived
```

`new` khai báo method hiding; nó **không thay thế virtual dispatch**. Vì vậy nói "`new` cũng là override" là sai.

## 5.5. `abstract`, `virtual`, `override`, `sealed`, `new` — phân biệt

| Từ khóa | Vai trò | Ví dụ thực tế |
|---|---|---|
| `abstract` | Không có implementation member tại declaration; class cụ thể phải implement | Payment provider bắt buộc `Pay` |
| `virtual` | Có implementation mặc định, có thể override | `GetDisplayName()` |
| `override` | Thay thế implementation trong slot virtual | `CardPayment.Pay()` |
| `sealed override` | Override cuối cùng, chặn override tiếp | Cố định một logic bảo mật thuộc virtual chain |
| `new` | Ẩn member từ base theo static binding | Tên trùng nhưng không muốn override |

**Mẫu trả lời:**

> Overloading là một tên method có nhiều signature, compiler chọn overload phù hợp dựa trên kiểu đối số. Overriding là derived class cung cấp implementation cho virtual/abstract member của base, runtime chọn implementation tùy object thực tế. `new` chỉ hide member, nên gọi qua biến kiểu base có thể vẫn sử dụng member base. Trong dự án, em sẽ chọn polymorphism khi có những chiến lược xử lý cùng contract, chẳng hạn các phương thức thanh toán.

---

# 6. C# type system: Value, Reference, Stack, Heap, Boxing

## 6.1. Value semantics và reference semantics

Value type khi assign thông thường copy giá trị. Reference type khi assign copy **reference** đến object; hai biến có thể chia sẻ object mutable.

```csharp
int a = 5;
int b = a;
b = 10;
Console.WriteLine(a); // 5

public class Box { public int Value { get; set; } }
var first = new Box { Value = 5 };
var second = first;
second.Value = 10;
Console.WriteLine(first.Value); // 10
```

Reference **được truyền theo giá trị** nếu không có `ref`/`out`/`in`:

```csharp
static void Replace(Box box) => box = new Box { Value = 99 };
static void Mutate(Box box) => box.Value = 99;
var x = new Box { Value = 1 };
Replace(x);
Console.WriteLine(x.Value); // 1 (chỉ gán lại bản copy của reference)
Mutate(x);
Console.WriteLine(x.Value); // 99 (thay object chung)
```

## 6.2. Stack/Heap — tránh trả lời sai

Stack thường chứa call frame và một số local values; managed heap chứa object allocations được GC theo dõi. Nhưng compiler/JIT có thể đặt values trong registers, embed value fields trong heap object, tối ưu một số allocation. **Định nghĩa value type dựa vào semantics, không dựa vào địa chỉ bộ nhớ.**

```csharp
class Container { public int Count { get; set; } }
var c = new Container(); // Object thông thường trên managed heap
c.Count = 7;             // Count là value type field/property backing storage của object
```

Một struct có thể nằm bên trong một class trên heap. Một object reference có thể nằm trên stack/register; object và biến chứa reference không phải cùng một thứ.

## 6.3. `string` immutable nhưng là reference type

```csharp
string x = "Hello";
string y = x;
y = y + " World";
Console.WriteLine(x); // Hello
```

`string` object bất biến; phép nối tạo giá trị chuỗi mới theo semantics (compiler/runtime có thể tối ưu). `string.Equals` so nội dung trong trường hợp mặc định phù hợp; `ReferenceEquals` so identity. String interning có thể khiến các literal dùng chung instance nhưng **không được dựa vào đó để đánh giá nội dung chuỗi**.

**Khi thao tác nối nhiều lần:** dùng `StringBuilder` nếu benchmark hoặc workload cho thấy việc tạo nhiều chuỗi tạm tốn chi phí; không phải mọi phép nối đơn giản đều cần StringBuilder.

## 6.4. Boxing/Unboxing

```csharp
int number = 123;
object boxed = number;      // boxing copy int vào boxed object
int restored = (int)boxed; // unboxing và copy value
// long error = (long)boxed; // InvalidCastException: boxed type thực là int
long ok = (int)boxed;       // unbox int trước, rồi numeric conversion
```

Boxing có thể phát sinh heap allocation và áp lực GC. Generic collections như `List<int>` thường tránh boxing phần tử khi so với collection dựa trên `object`. Nhưng truyền struct qua interface cũng có thể boxing tùy tình huống; hiệu năng luôn cần đo trong workload thực tế.

## 6.5. Nullable value và nullable reference

`int?` là `Nullable<int>`: có `HasValue` và `Value`. `string?` dưới nullable annotations diễn tả ý định compile-time về khả năng null, không tạo `Nullable<string>` runtime type.

```csharp
int? quantity = null;
int safeQuantity = quantity ?? 0;
string? nickname = null;
Console.WriteLine(nickname?.Length ?? 0);
```

**Bẫy:** Null-forgiving `!` như `nickname!.Length` chủ yếu tắt cảnh báo nullable của compiler, **không** ngăn `NullReferenceException` tại runtime nếu biến thật sự null.

---

# 7. const, readonly, static; biến, property, constructor, method

## 7.1. `const`: compile-time constant

```csharp
public const int DaysPerWeek = 7;
public const string AppName = "Restaurant";
```

Phải gán ngay tại declaration, constant expression hợp lệ; const field mặc định mang ý nghĩa static. `DateTime.UtcNow`, `Guid.NewGuid()`, config runtime không thể là `const`. Một public const dùng qua assembly khác thường được inline vào code caller; thay đổi library mà không compile lại client có nguy cơ giữ giá trị cũ.

## 7.2. `readonly`: hạn chế gán field, không khóa object

```csharp
public class Example
{
    private readonly List<string> _names = new();
    public void Add(string name) => _names.Add(name); // Hợp lệ
    // public void Reset() => _names = new(); // Không hợp lệ
}
```

Instance readonly field được gán ở declaration hoặc constructor phù hợp; static readonly được gán ở initializer hoặc static constructor. Với reference field, object có thể vẫn thay đổi.

## 7.3. `static`: thuộc type thay vì instance

```csharp
public static class TaxMath
{
    public static decimal AddTax(decimal subtotal, decimal rate)
        => subtotal * (1 + rate);
}
```

Static members chia sẻ theo type (chi tiết generic static state có thể khác nhau giữa closed constructed generic types). Mutable static fields có thể gặp race condition trong web app; không đặt "CurrentUser" của từng request vào static variable. `static readonly` hữu ích với giá trị khởi tạo runtime, nhưng không dùng nó để thay mọi configuration cần reload.

**So sánh ngắn:** `const` nói về compile-time value; `readonly` nói về khả năng *gán lại field*; `static` nói về *ownership của member*. Chúng không cùng một trục nên `static readonly` hợp lệ.

## 7.4. Local, field, property, parameter và lifetime

```csharp
public class PriceService
{
    private readonly decimal _taxRate; // instance field
    public PriceService(decimal taxRate) => _taxRate = taxRate; // constructor param
    public decimal Total(decimal price) // method param
    {
        decimal tax = price * _taxRate; // local variable
        return price + tax;
    }
}
```

Local variable có lexical scope và quy tắc definite assignment. Instance field sống cùng object khi object còn reachable; static field thuộc type/lifetime của AppDomain/AssemblyLoadContext trong ngữ cảnh runtime, không phải mặc định chỉ sống "trong một request".

## 7.5. `var`, `object`, `dynamic`

```csharp
var count = 10;       // int compile-time, không tự thành dynamic
object anything = 10; // kiểu static của biến là object; int bị boxing ở ví dụ này
dynamic late = 10;    // binding nhiều member operations tại runtime
```

`var` suy luận kiểu tĩnh từ initializer; `object` là type root; `dynamic` trì hoãn kiểm tra một số operation và dễ có runtime binder exception. Dùng `dynamic` có chủ đích khi cần interop/dynamic APIs, không dùng vì không biết type.

## 7.6. Methods, overload, optional/named/params

```csharp
static decimal Total(decimal price, int quantity = 1) => price * quantity;
var a = Total(100m);                  // 100
var b = Total(quantity: 3, price: 100m); // 300
static int Sum(params int[] values) => values.Sum();
```

Optional parameters tạo default argument theo compile-time tại caller, nên public API versioning cần chú ý. `params` cho phép truyền dãy arguments linh hoạt; modern C# cũng mở rộng hỗ trợ collection-based params trong ngữ cảnh phù hợp.

## 7.7. Pass-by-value vs `ref`, `out`, `in`

```csharp
static void Increase(ref int n) => n++;
static bool Parse(string s, out int result) => int.TryParse(s, out result);
static decimal Apply(in decimal value) => value * 2;

int n = 1;
Increase(ref n);              // n = 2
bool ok = Parse("42", out int parsed); // parsed = 42
```

- Mặc định pass-by-value: copy value hoặc copy reference tùy kiểu của đối số.
- `ref`: biến caller phải assigned; callee có thể thay đổi biến đó.
- `out`: callee phải gán result trước khi trả bình thường; caller không cần gán trước.
- `in`: readonly by-reference parameter, hữu ích có chọn lọc với struct lớn; đôi khi có defensive copies.

**Câu phỏng vấn:** "Tại sao `Product` đổi Name bên trong method mà người gọi thấy thay đổi, dù không có `ref`?" — Vì hai bên giữ references đến cùng object mutable; **không** có nghĩa C# tự truyền mọi reference type bằng `ref`.

---

# 8. Class, Struct, Enum, Record và immutability

## 8.1. Class: reference identity, lifecycle

Class phù hợp với entity có identity và lifecycle như `Order`, `Customer`. Nó có constructor, members, có thể kế thừa class và implement interfaces. Thông thường object class được cấp phát trên managed heap, nhưng cách JIT tối ưu không phải yếu tố định nghĩa ngôn ngữ.

## 8.2. Struct: value semantics

```csharp
public readonly struct Money
{
    public decimal Amount { get; }
    public string Currency { get; }
    public Money(decimal amount, string currency)
    {
        if (amount < 0) throw new ArgumentOutOfRangeException(nameof(amount));
        Amount = amount;
        Currency = currency;
    }
}
var a = new Money(100m, "VND");
var b = a; // copy value
```

Struct là value type, không kế thừa tùy ý từ class/struct do bạn định nghĩa, nhưng implement interface. `readonly struct` hạn chế mutation đối với instance members và có thể cải thiện hiểu biết về value semantics. Với struct lớn, copy thường xuyên có thể tốn chi phí; chọn struct vì **ý nghĩa giá trị** trước, rồi đo performance nếu quan trọng.

**Bẫy:** `default(Money)` vẫn tạo giá trị mặc định (Amount=0, Currency=null mặc dù property type không nullable theo annotation) vì zero-initialization. Constructor bảo vệ invariant không tự ngăn được `default` struct. Đó là lý do value objects dưới dạng struct cần thiết kế cho default case hoặc chọn class/record phù hợp.

## 8.3. Enum: named integral constants, không phải closed union

```csharp
public enum OrderStatus { Pending = 0, Confirmed = 1, Cancelled = 2 }
OrderStatus state = (OrderStatus)999; // compile được
Console.WriteLine(Enum.IsDefined(state)); // False
```

Khi lưu enum dưới dạng số trong database, phải giữ mapping ổn định; gán explicit values nếu trạng thái được persist. `[Flags]` dùng cho bit combinations như `Read=1, Write=2, Delete=4`, không dành cho các trạng thái loại trừ nhau.

## 8.4. Record và value equality

```csharp
public record ProductDto(int Id, string Name);
var x = new ProductDto(1, "Coffee");
var y = new ProductDto(1, "Coffee");
Console.WriteLine(x == y); // True (value equality theo record components)
var z = x with { Name = "Tea" };
```

`record` mặc định là reference type (`record class`); `record struct` là value type. Record thích hợp với DTO và value-like data nhưng không tự bảo đảm deep immutability. Nếu một record chứa mutable collection, record equality cũng không tự so sánh sâu từng item của collection.

## 8.5. Immutability: state không thay sau tạo

Immutable objects dễ suy luận, thích hợp cho value objects và một số dữ liệu truyền giữa boundaries. Nhưng immutable update thường tạo object/copy mới; với dữ liệu lớn hoặc hot path cần đánh giá allocation. `init` hạn chế việc gán property sau initialization; `readonly` field hạn chế gán field; cả hai không đồng nghĩa deep immutable.

**Mẫu trả lời struct vs class:**

> Class có reference semantics và phù hợp entity có identity, trạng thái thay đổi theo lifecycle. Struct có value semantics, khi gán thông thường copy giá trị, phù hợp value objects nhỏ như tọa độ hoặc thông tin tiền tệ có thiết kế cẩn thận. Struct không tự động luôn nằm trên stack hoặc luôn nhanh hơn; kích thước, boxing, copy và tình huống sử dụng ảnh hưởng hiệu năng. Vì vậy em chọn dựa theo domain semantics trước.

---

# 9. Extension Method, Generic, Delegate, Event

## 9.1. Extension Method: cú pháp instance cho static method

```csharp
public static class MoneyExtensions
{
    public static string ToVndText(this decimal amount)
        => $"{amount:N0} VND";
}
Console.WriteLine(150000m.ToVndText());
```

Đây là một **static method** trong static class, với `this` ở parameter đầu. Namespace chứa extension phải được import/đúng scope. Extension method không thực sự sửa type gốc, không tự truy cập private members và không có virtual dispatch theo runtime type như override.

```csharp
class Animal { }
class Dog : Animal { }
static class SpeakExtensions
{
    public static string Speak(this Animal _) => "Animal";
    public static string Speak(this Dog _) => "Dog";
}
Animal pet = new Dog();
Console.WriteLine(pet.Speak()); // Animal
```

Overload resolution dựa trên compile-time type. Nếu instance member phù hợp tồn tại, instance method thường thắng extension method. C# mới có thêm extension members syntax trong một số phiên bản; để phỏng vấn Intern, biết cú pháp static extension truyền thống và bản chất binding là nền tảng.

**Ứng dụng:** `Where`, `Select`, `AddApplicationServices()`, helper chuyển định dạng dữ liệu. **Tránh:** extension method có nhiều side effects, thao tác network/database kín đáo gây khó đoán, tên xung đột hoặc biến business workflow thành helper khó test.

## 9.2. Generic: code tổng quát mà vẫn type-safe

```csharp
public sealed class Result<T>
{
    public bool Success { get; init; }
    public T? Data { get; init; }
}
var ok = new Result<int> { Success = true, Data = 123 };
```

`T` là type parameter; compiler kiểm tra type khi dùng. Generic giúp tránh cast rủi ro và nhiều trường hợp boxing. Constraints (`where T : class`, `struct`, `new()`, interface/base class) giới hạn những type hợp lệ. Không nên tạo `Repository<T>` cho mọi entity chỉ vì mọi bảng đều CRUD: nhiều entity có business query riêng cần API riêng.

## 9.3. Delegate, Func, Action

Delegate là type biểu diễn reference đến method có signature tương thích.

```csharp
Func<int, int, int> add = (a, b) => a + b;
Action<string> log = message => Console.WriteLine(message);
Predicate<int> positive = x => x > 0;
Console.WriteLine(add(2, 3)); // 5
```

- `Func<T..., TResult>` có giá trị trả về.
- `Action<T...>` trả `void`.
- `Predicate<T>` trả bool (signature được chuẩn hóa).

Delegate hỗ trợ callback, strategy và LINQ expressions. Delegate có thể multicast, nhưng nếu nhiều subscribers và return value thì chỉ return value của invocation cuối được thấy theo cơ chế gọi multicast thông thường; cần xử lý ngoại lệ và semantics cẩn thận.

## 9.4. Event

Event dùng để phát tín hiệu subscription theo pattern .NET. Publisher kiểm soát invocation; subscriber đăng ký/unregister. Một event subscription có thể giữ strong reference, gây memory leak logic nếu subscriber sống ngắn mà không unsubscribe ở lifecycle thích hợp.

```csharp
public class OrderTracker
{
    public event EventHandler? Changed;
    public void NotifyChanged() => Changed?.Invoke(this, EventArgs.Empty);
}
```

**Phân biệt:** Delegate là type/callback abstraction; event giới hạn cách subscriber tương tác với danh sách handler bên ngoài publisher. SignalR event tên `NewOrder` trên client không đồng nghĩa C# `event` trong code mặc dù đều có ý tưởng phát tín hiệu.

---

# 10. Collection, LINQ và IQueryable

## 10.1. Collection types và độ phức tạp

| Kiểu | Đặc điểm | Tình huống |
|---|---|---|
| `T[]` | Fixed length, random access O(1) | Kích thước biết trước |
| `List<T>` | Dynamic array, index O(1) trung bình; append amortized O(1) | Danh sách cần thêm phần tử |
| `Dictionary<K,V>` | Hash-based, lookup trung bình O(1) | Tìm nhanh theo khóa |
| `HashSet<T>` | Membership trung bình O(1), no duplicates | Loại trùng, kiểm tra tồn tại |
| `Queue<T>` | FIFO | Lần lượt xử lý công việc |
| `Stack<T>` | LIFO | Undo, parsing |
| `ConcurrentDictionary<K,V>` | Concurrent access | Shared concurrent map |

"O(1)" là độ phức tạp kỳ vọng/trung bình trong nhiều trường hợp, không cam kết mọi dữ liệu và cấu hình hash đều O(1). Không nên dùng `Dictionary` cho mọi dataset nếu thao tác chính là duyệt theo thứ tự.

## 10.2. LINQ: projection/filter/aggregation

```csharp
var products = new List<(string Name, decimal Price)>
{
    ("Coffee", 30000m), ("Tea", 20000m), ("Juice", 40000m)
};
var names = products
    .Where(p => p.Price >= 30000m)
    .OrderBy(p => p.Price)
    .Select(p => p.Name)
    .ToList(); // ["Coffee", "Juice"]
```

`Where` lọc; `Select` tạo projection; `OrderBy` sắp xếp; `Any` hỏi sự tồn tại; `Count` đếm; `GroupBy` gom nhóm. Đừng lẫn `Select` với `SelectMany`: `SelectMany` làm phẳng kết quả sequence lồng nhau.

## 10.3. Deferred execution

```csharp
var nums = new List<int> { 1, 2, 3 };
var query = nums.Where(x => x >= 3);
nums.Add(4);
Console.WriteLine(string.Join(",", query)); // 3,4
```

Nhiều sequence operators được thực thi khi enumerate (`foreach`, `ToList`, `Count`, v.v.), không nhất thiết khi khai báo query. Rủi ro là enumerate nhiều lần khiến logic tốn tài nguyên, thay đổi dữ liệu source hoặc query database bị thực thi lại. `ToList()` materialize kết quả tại thời điểm gọi nhưng dùng memory để giữ toàn bộ danh sách.

## 10.4. IQueryable, expression tree và EF Core

`IEnumerable<T>` là contract enumerate. `IQueryable<T>` bổ sung query provider và expression tree để provider có thể dịch truy vấn sang nguồn bên ngoài, ví dụ SQL.

```csharp
IQueryable<Product> query = db.Products.Where(p => p.Price > 10000m);
var rows = await query.Select(p => new ProductDto(p.Id, p.Name)).ToListAsync();
```

Nếu EF Core provider dịch được predicate/projection sang SQL, database chỉ trả dữ liệu cần thiết. Nếu gọi `ToListAsync()` quá sớm rồi mới lọc, đã tải nhiều data lên application memory. Không phải mọi method C# đều dịch thành SQL; EF Core có ràng buộc client evaluation và có thể throw khi biểu thức không hỗ trợ dịch ở vị trí quan trọng.

**Mẫu trả lời:**

> Em phân biệt `IEnumerable` là tập kết quả có thể duyệt, còn `IQueryable` giúp query provider biểu diễn và dịch truy vấn. Với EF Core, em cố gắng đặt `Where`, `Select`, `OrderBy`, `Skip/Take` ở query trước `ToListAsync` để database xử lý nhiều nhất có thể. Nhưng không tối ưu mù quáng: em sẽ xem SQL sinh ra, index và execution plan nếu query chậm.

---

# 11. Exception, GC, IDisposable và async/await

## 11.1. Exception là lỗi bất thường, không phải một kiểu if/else khác

```csharp
try
{
    var value = int.Parse(input);
}
catch (FormatException)
{
    Console.WriteLine("Not an integer");
}
finally
{
    Console.WriteLine("Parse attempt ended");
}
```

Nếu tình huống parse fail là bình thường, ưu tiên `TryParse`. `catch (Exception)` rồi nuốt lỗi khiến bug khó debug. Nếu bắt lỗi để log rồi propagate, dùng `throw;` thay vì `throw ex;` để giữ stack trace phù hợp. Không đưa stack trace và secret vào HTTP response production.

## 11.2. GC và generations

CLR GC tự thu hồi managed objects không còn reachable từ GC roots. Gen 0, Gen 1, Gen 2 giúp tối ưu giả định nhiều object có vòng đời ngắn. Large Object Heap (LOH) chứa các object lớn theo ngưỡng/cơ chế runtime; đừng học thuộc ngưỡng như một hằng số API bất biến cho mọi runtime.

**GC không bảo đảm khi nào một object được dọn**; không dùng finalizer làm cơ chế release connection chủ động. Một reference bị giữ trong static collection/event subscription có thể khiến object còn reachable dù về mặt business đã không còn cần.

## 11.3. `IDisposable`, `using`, `await using`

```csharp
using var stream = File.OpenRead("data.json");
// stream.Dispose được đảm bảo theo scope exit semantics
```

`Dispose` kiểm soát vòng đời resources như file/network handles, pool resources. `await using` gọi `DisposeAsync` cho resource hỗ trợ `IAsyncDisposable`. GC và Dispose bổ sung nhau: GC dọn memory, disposal giúp release resource đúng lúc.

## 11.4. Async/await — state machine và bất đồng bộ I/O

`async` cho phép `await`; compiler chuyển method thành logic state-machine để tiếp tục sau khi Task hoàn thành. `await` không có nghĩa "tạo thread mới". I/O async cho phép request thread không phải block trong lúc chờ network/database.

```csharp
public async Task<ProductDto?> GetAsync(int id, CancellationToken ct)
{
    return await _db.Products
        .Where(p => p.Id == id)
        .Select(p => new ProductDto(p.Id, p.Name))
        .FirstOrDefaultAsync(ct);
}
```

`Task<T>` thể hiện operation có kết quả; `CancellationToken` truyền yêu cầu hủy có tính hợp tác. `Task.WhenAll` xử lý nhiều operations độc lập concurrently, nhưng không chạy hai EF Core operations cùng lúc trên cùng một `DbContext`. Không dùng `Task.Run(() => db.Products.ToList())` để "biến query synchronous thành async tốt".

**Tại sao gọi `.Result`/`.Wait()` nguy hiểm?** Chúng block caller; có thể dẫn tới thread starvation và trong những synchronization contexts nhất định gây deadlock. ASP.NET Core thông thường không có synchronization context kiểu UI/ASP.NET cổ điển, nhưng sync-over-async vẫn ảnh hưởng scalability và là pattern nên tránh.

**Mẫu trả lời:**

> Async/await giúp em viết code bất đồng bộ dễ đọc như code tuần tự. Khi chờ database I/O, thread xử lý không cần đứng chờ trong suốt operation, từ đó server có thể phục vụ nhiều request hơn. Async không tự động làm một query nhanh hơn và cũng không mặc định tạo thread. Em dùng các API async thật như `ToListAsync()`, truyền CancellationToken và tránh đồng thời thao tác trên cùng DbContext.

---

# 12. SOLID, DI, ASP.NET Core và REST

## 12.1. SOLID với lý do thực tế

**S — Single Responsibility:** một module có một lý do chính để thay đổi, ví dụ `OrderService` không kiêm rendering HTML và quản lý JWT key. Không đồng nghĩa chỉ được một method.

**O — Open/Closed:** mở rộng behavior qua strategy/plugin phù hợp thay vì liên tục chỉnh code stable. Nhưng không nên tạo interface cho khả năng mở rộng chưa có căn cứ.

**L — Liskov Substitution:** implementation con giữ contract quan sát được của abstraction; một `IPaymentProcessor` không được làm người gọi bất ngờ theo cách phá điều kiện đã cam kết.

**I — Interface Segregation:** contract nhỏ đúng nhu cầu, không buộc class implement các method không dùng.

**D — Dependency Inversion:** high-level policy phụ thuộc abstraction, cụ thể hóa ở composition root thay vì dính trực tiếp vào low-level details.

## 12.2. DI: ai tạo dependency?

```csharp
public interface IClock { DateTime UtcNow { get; } }
public sealed class SystemClock : IClock { public DateTime UtcNow => DateTime.UtcNow; }
public sealed class ReceiptService
{
    private readonly IClock _clock;
    public ReceiptService(IClock clock) => _clock = clock;
}
// Program.cs
builder.Services.AddSingleton<IClock, SystemClock>();
builder.Services.AddScoped<ReceiptService>();
```

DI container tạo và gắn dependency, giúp test bằng fake clock. Nhưng DI **không đồng nhất** với DIP: bạn có thể inject một concrete object và vẫn có coupling lớn. Cũng không nên truyền `IServiceProvider` đi khắp code để resolve service tùy ý nếu constructor injection diễn tả dependencies tốt hơn.

**Lifetimes:** `Transient` tạo instance mới theo resolution; `Scoped` tái sử dụng trong một scope, thường một request; `Singleton` giữ một instance trên container. Inject scoped `DbContext` vào singleton có thể là captive dependency; background worker cần scope/factory riêng.

## 12.3. ASP.NET Core request lifecycle

Một HTTP request được server nhận, đi qua middleware (ví dụ exception handling, HTTPS, authentication/authorization theo cấu hình), routing chọn endpoint, model binding/validation chuẩn bị input, controller/service xử lý, response được serialize và trả về. Thứ tự middleware có ý nghĩa: authentication nên có trước authorization ở cấu hình thông thường.

**MVC vs Web API:** MVC phục vụ server-rendered view, controller có thể return Razor views. Web API thường return structured data như JSON cho React/mobile clients. Cả hai đều nằm trong ASP.NET Core ecosystem, có thể cùng sử dụng model binding, validation và DI. Không nên phát biểu MVC bắt buộc chỉ có HTML hoặc Web API không bao giờ dùng MVC framework features.

## 12.4. REST và HTTP semantics

| Method | Ý nghĩa | Idempotent theo HTTP semantics? |
|---|---|---|
| GET | Đọc resource | Có (và safe theo chuẩn) |
| POST | Xử lý/tạo subordinate resource theo endpoint | Không mặc định |
| PUT | Thay thế resource state | Có |
| PATCH | Chỉnh một phần | Không được đảm bảo chung |
| DELETE | Xóa resource | Có |

Idempotent nghĩa là nhiều request giống nhau có **intended effect** lên server state như một request; không bắt buộc response status giống hệt. Trong production, retry POST thanh toán/tạo đơn cần idempotency key hoặc de-duplication strategy nếu không muốn tạo trùng.

**Status codes:** 200 OK, 201 Created, 204 No Content, 400 Bad Request, 401 Unauthorized (thường thiếu credentials hợp lệ), 403 Forbidden (không đủ quyền), 404 Not Found, 409 Conflict, 500 Internal Server Error. Authentication và authorization là hai khái niệm khác nhau.

## 12.5. DTO và validation boundary

DTO giới hạn dữ liệu đi qua API, tách contract JSON khỏi database entity. Không trả `PasswordHash` chỉ vì entity có property đó. Server phải validate request và business rules; client validation chỉ giúp UX. Dùng model binding/DataAnnotations cho input constraints thông thường, còn state transition rules thuộc business layer/domain và database constraints giữ tính nhất quán lâu dài.

---

# 13. EF Core, SQL, Transaction và Concurrency

## 13.1. EF Core ORM là gì?

ORM map data giữa .NET objects và relational database. `DbContext` vừa là entry point để query/update vừa quản lý change tracking/unit-of-work behavior. `DbSet<T>` là access point cho entity type, không tự đồng nghĩa "một table đúng nghĩa" trong mọi mapping scenario.

```csharp
var product = await db.Products.FirstOrDefaultAsync(p => p.Id == id);
if (product is not null)
{
    product.Price = 25000m;
    await db.SaveChangesAsync();
}
```

Để kiểm tra query thật, xem SQL logging/`ToQueryString()` ở ngữ cảnh phù hợp. EF Core làm lập trình thuận tiện hơn nhưng không loại bỏ yêu cầu hiểu SQL, index, isolation và locks.

## 13.2. Tracking và AsNoTracking

Tracked entity có thể được phát hiện thay đổi và lưu qua `SaveChanges`. Read-only queries thường cân nhắc `AsNoTracking` để giảm overhead. Nếu projection chỉ trả scalar DTO, việc thêm `AsNoTracking` có thể không làm khác biệt lớn vì entity instance không nằm trong result. Không claim mọi truy vấn `AsNoTracking` đều nhanh hơn đáng kể.

## 13.3. N+1 và query optimization

N+1 là một query lấy list, rồi N query tải related data từng phần tử. Có thể giảm bằng projection, eager loading (`Include`) hoặc query có cấu trúc phù hợp. `Include` nhiều collections có thể tạo cartesian explosion; split queries có trade-off round trips/consistency. Nên dùng filter ở DB, chọn chỉ columns cần, paginate list dài và đo actual execution plan.

## 13.4. SQL JOIN, index và normalization

`INNER JOIN`: chỉ trả kết hợp khớp. `LEFT JOIN`: giữ rows bên trái khi không có matching row. **Primary key** định danh hàng, **foreign key** giữ referential integrity, **unique constraint/index** bảo vệ uniqueness. **Index** giúp read workload phù hợp nhưng tốn dung lượng và chi phí writes.

**Normalization** nhằm giảm redundancy và anomalies khi lưu dữ liệu quan hệ: `Order` và `OrderItem` tách bảng một-nhiều thay vì chứa list món trong một cột tùy ý (nếu không có lý do rõ ràng khác). Denormalization có thể hữu ích cho read performance khi đánh đổi được đo đạc.

## 13.5. Transaction và ACID

**Atomicity:** thao tác trong transaction commit/rollback như một đơn vị. **Consistency:** ràng buộc dữ liệu được duy trì. **Isolation:** transaction đồng thời được nhìn nhận theo isolation guarantees của DB. **Durability:** commit bền vững theo bảo đảm hệ quản trị.

`SaveChanges()` của EF Core thường nằm trong transaction khi relational provider hỗ trợ; khi nhiều bước cần cùng transaction, cân nhắc transaction boundary rõ ràng. Đừng bọc gọi external HTTP/SignalR trong DB transaction rồi kỳ vọng rollback SQL sẽ thu hồi message đã gửi.

## 13.6. Optimistic concurrency

Hai request đọc đơn Pending rồi đồng thời Confirm có thể ghi đè hoặc lặp side-effect. Concurrency token/SQL Server `rowversion` giúp detect conflicting updates; nếu phát hiện xung đột, ứng dụng cần chính sách retry/reload/reject phù hợp. Ngoài ra cần xem idempotency cho command và những unique constraints phục vụ nghiệp vụ.

```csharp
public class Order
{
    public int Id { get; set; }
    [Timestamp]
    public byte[] RowVersion { get; set; } = [];
}
```

Không phải cứ `await SaveChangesAsync()` là tự chống mọi race. Transaction isolation và database constraints vẫn cần được chọn theo nghiệp vụ.

**Mẫu trả lời:**

> Em dùng EF Core để viết query bằng LINQ và quản lý entity, nhưng biết hiệu năng cuối cùng phụ thuộc SQL được dịch, index và lượng dữ liệu. Với màn hình đọc, em ưu tiên projection và tracking phù hợp; với cập nhật, em kiểm tra business rules và transaction. Nếu hai nhân viên cùng đổi trạng thái một đơn, em sẽ tìm hiểu concurrency token hoặc conditional update, không chỉ kiểm tra trạng thái một lần trong bộ nhớ.

---

# 14. Authentication, JWT, SignalR và an toàn

## 14.1. Authentication vs Authorization

Authentication trả lời "người gọi được xác thực là ai?"; authorization trả lời "người đó có được phép làm hành động này trên resource này không?". User có token hợp lệ chưa chắc được phép đọc đơn của nhà hàng khác.

## 14.2. JWT: ký không có nghĩa mã hóa

Compact signed JWT/JWS thường có `base64url(header).base64url(payload).signature`. Payload đọc được bằng cách decode Base64URL, không được chứa secret/password. Server phải validate signature, algorithm policy, issuer, audience, expiration và tùy bối cảnh các claims khác. Dùng HTTPS để tránh token bị nghe lén. Access token càng tồn tại lâu, rủi ro khi bị lộ càng lớn.

**Refresh token:** dùng để xin access token mới, phải lưu và quản lý an toàn; rotation/revocation tùy thiết kế. JWT không tự giải quyết việc logout/revoke ngay nếu server chỉ xác minh chữ ký và `exp`.

## 14.3. Lưu token phía client

LocalStorage dễ thao tác nhưng JavaScript chạy trên trang có thể đọc token nếu dính XSS; cookies có `HttpOnly`, `Secure`, `SameSite` phù hợp giúp giảm rủi ro đọc token bằng JS nhưng cần quản lý CSRF khi sử dụng cookie-based authentication. Không tồn tại một phương án luôn tốt nhất cho mọi kiến trúc SPA. **Quan trọng hơn:** giảm XSS, bảo vệ transport, dùng token ngắn hạn và áp dụng chính sách phù hợp.

## 14.4. SignalR và thông báo đơn mới

SignalR giữ kết nối logical cho server push, thường ưu tiên WebSockets khi khả dụng và có transport fallback. `Hub` là abstraction cho connection, group, client invocation. Có thể dùng `IHubContext<KitchenHub>` để gửi message từ application service. Group membership cần kiểm tra authorization: không tin `restaurantId` do client tự nhập.

**Không nhầm signal với durable event:** Nếu bếp offline, SignalR không thay thế database. Khi reconnect, client cần fetch trạng thái mới. Nếu lưu đơn thành công nhưng gửi SignalR lỗi, DB vẫn là source of truth. Outbox hoặc background job có thể tăng độ tin cậy, cùng với cơ chế xử lý duplicate và reconciliation.

## 14.5. Bảo mật ứng dụng cơ bản

- **SQL Injection:** dùng parameterized query/LINQ đúng cách; không nối raw SQL từ input.
- **XSS:** encode output, không render HTML không tin cậy tùy tiện; CSP là defense-in-depth.
- **CSRF:** lưu ý cookie-auth workflows, anti-forgery/SameSite phù hợp.
- **Broken Access Control:** luôn kiểm tra quyền ở server, kể cả React đã ẩn nút.
- **Secrets:** không commit signing keys, connection strings production hoặc mật khẩu vào GitHub; dùng environment variables/secret manager.
- **Password:** hash bằng password hashing algorithm phù hợp (ví dụ ASP.NET Core Identity), không lưu plain text hoặc hash nhanh thông thường như SHA-256 trực tiếp cho mật khẩu.

---

# 15. Testing, Git, Debugging và trả lời tình huống

## 15.1. Unit test vs Integration test

Unit test kiểm tra một đơn vị logic có boundary tương đối nhỏ, thay dependency ngoài bằng fake/mock khi hợp lý. Integration test kiểm tra nhiều thành phần kết hợp, như controller + database test hoặc API pipeline. Đừng mock mọi thứ: một test chỉ kiểm tra mock được gọi đôi khi không chứng minh nghiệp vụ đúng.

```csharp
// Ví dụ logic thuần, dễ unit test
public static decimal CalculateTotal(decimal price, int quantity)
{
    if (price < 0 || quantity <= 0)
        throw new ArgumentOutOfRangeException();
    return price * quantity;
}
```

Các case test nên có: giá hợp lệ, quantity=0, giá âm, quantity rất lớn theo contract, rounding nếu có quy tắc tiền tệ.

## 15.2. Debugging có cấu trúc

Một cách kể bug tốt: **reproduce → hypothesis → inspect logs/breakpoints/database → xác định root cause → fix → regression test → bài học**. Ví dụ: UI không cập nhật khi bếp mất kết nối; xác định client reconnect nhưng không reload đơn mới; khắc phục bằng đồng bộ lại API sau reconnect và test tình huống mất kết nối.

Nhấn mạnh đó là *ví dụ tình huống* chứ không tự nhận đã gặp nếu bạn chưa có bằng chứng.

## 15.3. Git cơ bản

Biết `clone`, `branch`, `add`, `commit`, `push`, `pull`, pull request, merge conflict, revert vs reset. Với repo public: kiểm tra secrets, connection strings, `.gitignore`, README, hướng dẫn chạy/migration và test. Không force-push vào shared branch tùy tiện.

## 15.4. Khi không biết một câu hỏi

Câu trả lời mẫu:

> Phần này em chưa triển khai trực tiếp, nên em không muốn khẳng định theo kinh nghiệm. Em hiểu mục tiêu của nó là …, và nếu phải áp dụng em sẽ kiểm tra tài liệu chính thức, tạo ví dụ nhỏ để thử nghiệm, viết test và nhờ review khi thay đổi ảnh hưởng bảo mật hoặc dữ liệu.

Interviewer thường đánh giá cao **giới hạn rõ ràng + cách tìm lời giải hợp lý** hơn việc bịa ra trải nghiệm.

---

# 16. Ngân hàng câu hỏi có mẫu trả lời dài

Phần này được viết theo ngôn ngữ nói để bạn luyện trước phỏng vấn. Sau mỗi câu, hãy tự viết lại bằng cách diễn đạt của mình.

### Q1. OOP là gì và vì sao dự án backend dùng OOP?

**Trả lời:** OOP là phương pháp tổ chức code quanh các object có state và behavior, giúp mô hình hóa domain và chia trách nhiệm. Trong hệ thống nhà hàng, Order đại diện cho đơn hàng, có thông tin và hành vi hợp lệ như Confirm hoặc Cancel; OrderService có thể điều phối tương tác giữa domain, database và notification. OOP hỗ trợ encapsulation, abstraction, inheritance, polymorphism. Em không cho rằng OOP luôn tốt nhất: CRUD đơn giản có thể chỉ cần các service và DTO gọn, còn nghiệp vụ phức tạp thì domain model có invariant rõ sẽ mang lại nhiều giá trị.

### Q2. Encapsulation và Abstraction khác nhau như thế nào?

**Trả lời:** Encapsulation kiểm soát truy cập và thay đổi trạng thái, ví dụ Status private setter và Confirm() kiểm tra điều kiện. Abstraction tập trung cung cấp contract vừa đủ cho caller, ví dụ controller chỉ gọi IOrderService.CreateAsync mà không cần biết SQL cụ thể. Một interface biểu diễn abstraction, nhưng bản thân class có private fields chưa chắc tạo abstraction tốt; hai nguyên tắc giải quyết những mối quan tâm khác nhau và thường được kết hợp.

### Q3. Interface hay Abstract Class, chọn cái nào?

**Trả lời:** Em chọn interface khi muốn mô tả một capability được nhiều implementation khác nhau thực hiện và cho module khác chỉ phụ thuộc contract, ví dụ INotificationSender có SignalR hoặc Email implementation. Em chọn abstract class khi có quan hệ is-a thật và các type cần chia sẻ state, constructor hoặc một phần thuật toán. C# cho class implement nhiều interface nhưng chỉ có một base class. Em cũng lưu ý C# mới có default interface methods, nên không nói interface tuyệt đối không có code.

### Q4. Phân biệt Overload, Override, `new`?

**Trả lời:** Overload là cùng tên method nhưng khác parameter signatures; compiler chọn lời gọi phù hợp lúc compile. Override thay đổi virtual/abstract behavior của class cha, runtime dispatch chọn theo object thực tế. `new` là hiding, khác override: khi giữ derived object trong biến kiểu base, lời gọi tới member bị hide có thể chọn member base. Em có thể chứng minh bằng ví dụ `Parent p = new Child()` và so sánh kết quả in ra.

### Q5. Value type có luôn ở stack không?

**Trả lời:** Không. Value type có semantics copy giá trị; reference type có semantics copy reference. Vị trí memory tùy runtime context: một int field của class nằm cùng object trên managed heap, và JIT có thể giữ local value trong register. Câu "value type ở stack, reference type ở heap" dễ nhớ nhưng không đủ chính xác. Khi phỏng vấn em ưu tiên giải thích bằng phép gán và mutation hơn là chỉ dựa vào vị trí bộ nhớ.

### Q6. Vì sao string là reference type nhưng gán biến khác trông như copy?

**Trả lời:** String immutable. Khi `string a="Hi"; string b=a; b="Hello"`, biến b được gán reference đến string khác, chứ không sửa object gốc mà a đang tham chiếu. String còn có value equality theo nội dung; hai chuỗi có cùng nội dung có thể bằng nhau dù không nhất thiết cùng object identity. Với lặp nối nhiều chuỗi lớn, em cân nhắc StringBuilder nhưng chỉ tối ưu khi cần.

### Q7. const, readonly, static khác gì?

**Trả lời:** const là compile-time constant, phải khởi tạo tại declaration và giá trị có thể inline vào assembly sử dụng; vì vậy không phù hợp với cấu hình hay public giá trị thường đổi. readonly áp dụng cho field, có thể gán trong declaration/constructor nhưng không gán lại ở instance method thường; nếu field trỏ đến object mutable thì object vẫn thay đổi được. static nghĩa là member thuộc type, chia sẻ thay vì mỗi instance có bản riêng. Có thể kết hợp static readonly vì hai từ khóa kiểm soát hai đặc tính khác nhau.

### Q8. `ref`, `out`, `in` dùng khi nào?

**Trả lời:** Mặc định C# truyền argument by value: với class là copy reference. `ref` cho phép method thay đổi biến caller và yêu cầu assigned trước; `out` dùng để trả thêm kết quả và method phải gán trước khi return bình thường; `in` là readonly by-reference, đáng cân nhắc với struct lớn. Em không dùng các modifier chỉ để làm code "tối ưu" mà cần cân nhắc API clarity và performance đo được.

### Q9. Class và Struct, dùng cái nào cho Order?

**Trả lời:** Em chọn class cho Order vì Order là entity có identity, quan hệ với line items, trạng thái được cập nhật qua lifecycle. Struct phù hợp hơn cho small value-like data như tọa độ hoặc immutable value objects với thiết kế default state cẩn thận. Struct assign thường copy toàn bộ value nên không phải luôn nhanh hơn class; performance cần đo theo use case.

### Q10. Extension method thực chất là gì?

**Trả lời:** Extension method là static method có cú pháp gọi như instance method qua `this` ở parameter đầu; compiler resolve tĩnh. Nó không thêm instance member thực sự vào type và không override được virtual method. LINQ Where/Select là ví dụ phổ biến; em cũng có thể dùng để nhóm DI registrations trong Program.cs. Em tránh giấu business logic lớn hoặc side effects bất ngờ trong extension methods.

### Q11. IEnumerable và IQueryable khác nhau khi dùng EF Core?

**Trả lời:** IEnumerable cho khả năng enumerate; IQueryable kết hợp expression tree và provider nên EF Core có thể dịch phần truy vấn phù hợp sang SQL. Em đặt filter/projection/pagination trước khi materialize để hạn chế lấy dữ liệu thừa. Nếu gọi ToListAsync quá sớm rồi mới Where trong memory, hiệu năng có thể giảm. Em cũng biết không phải mọi biểu thức C# đều dịch được sang SQL nên cần xem query và đo khi tối ưu.

### Q12. Async/await có làm query nhanh hơn không?

**Trả lời:** Không tự làm SQL chạy nhanh hơn. Async giúp không giữ thread bị block khi chờ database/network I/O, nhờ đó backend thường scale tốt hơn khi có nhiều concurrent requests. Em dùng các async APIs thực như FirstOrDefaultAsync, truyền CancellationToken, tránh Task.Run để bọc sync EF Core query và không thực thi song song nhiều query trên cùng DbContext.

### Q13. Vì sao DTO quan trọng trong Web API?

**Trả lời:** Entity là persistence/domain representation, DTO là contract request/response. Không nên đưa entity có PasswordHash hay internal fields trực tiếp ra client. DTO giúp giới hạn dữ liệu, validation, hỗ trợ API versioning và tránh over-posting. Trade-off là mapping code và nhiều types hơn. Với project nhỏ có thể map thủ công, còn project lớn cân nhắc giải pháp khác tùy độ phức tạp.

### Q14. Authentication và Authorization khác nhau như thế nào?

**Trả lời:** Authentication xác định danh tính, Authorization kiểm tra quyền thao tác trên resource. Người dùng đăng nhập thành công chưa chắc có quyền xóa đơn, nhất là đơn thuộc chi nhánh khác. JWT là một dạng token thường dùng; server phải verify signature và claims phù hợp. JWT ký số không làm payload bí mật. Backend vẫn phải enforce quyền ngay cả khi UI đã ẩn nút Admin.

### Q15. SignalR có thay REST API không?

**Trả lời:** Không phải thay thế hoàn toàn. REST thích hợp với read/write resource thông thường và xây dựng các endpoint có contract rõ; SignalR hữu ích để server push thông báo nhanh đến browser đang kết nối. Với đơn hàng nhà hàng, API lưu đơn vào database, SignalR báo bếp có đơn mới. Nếu mất kết nối, client cần gọi API để đồng bộ lại. Trường hợp yêu cầu giao message đáng tin cậy cao có thể cần outbox, queue và retry/idempotency bổ sung.

### Q16. Hai người cùng xác nhận một đơn, xử lý thế nào?

**Trả lời:** Chỉ `if (Status == Pending)` ở application memory chưa đủ vì hai request có thể đọc cùng trạng thái cũ. Em cân nhắc optimistic concurrency token, conditional update và transaction theo business requirement. Khi conflict, endpoint nên trả phản hồi phù hợp (ví dụ 409) hoặc retry có kiểm soát. Nếu operation có external side effect như thanh toán hay gửi event, còn cần idempotency để không thực hiện trùng.

### Q17. Tại sao cần database index? Có bất lợi gì?

**Trả lời:** Index giúp database tìm/lọc/join/order nhanh hơn cho những query phù hợp, ví dụ query danh sách đơn theo CustomerId và thời điểm. Nhưng index chiếm storage, tốn chi phí maintain khi insert/update/delete, và một index không phải luôn được query optimizer sử dụng. Em sẽ kiểm tra SQL, execution plan và thống kê trước khi quyết định index mới, không đánh index mọi column.

### Q18. Nếu nhà tuyển dụng hỏi bug khó nhất bạn từng gặp?

**Trả lời theo khuôn, thay bằng bug thật của bạn:** Ban đầu em mô tả triệu chứng và cách reproduce, rồi đưa giả thuyết, dùng logging/breakpoints hoặc SQL để so sánh expectation với dữ liệu thực. Khi tìm ra nguyên nhân, em sửa ở vị trí tối thiểu phù hợp và test regression, sau đó rút ra điều cần cải thiện như validation hay logging. Em sẽ ưu tiên kể một bug đã tự giải quyết và có thể chỉ vào commit hoặc source, thay vì một vấn đề nghe hoành tráng nhưng không chứng minh được.

### Q19. Em đã áp dụng Clean Architecture chưa?

**Trả lời trung thực:** Em có tìm hiểu các nguyên tắc dependency direction và separation of concerns. Trong các project cá nhân, mức áp dụng có thể khác nhau: có nơi controller trực tiếp dùng DbContext để giữ đơn giản, có nơi tách service hoặc DTO rõ hơn. Em chưa nên khẳng định dự án đạt Clean Architecture chỉ vì chia folder; em sẽ nêu chính xác dependency graph hiện tại và lý do nếu cần refactor.

### Q20. Nếu không biết kiến thức được hỏi thì sao?

**Trả lời:** Em sẽ nói rõ phần mình chưa từng triển khai, trình bày giả thuyết trên nền tảng đang biết, rồi đề xuất cách kiểm tra bằng tài liệu chính thức, sample nhỏ, unit/integration test và code review. Đối với tính năng ảnh hưởng bảo mật hoặc dữ liệu, em sẽ không đưa quyết định dựa trên suy đoán chưa xác thực.

---

# 17. Kế hoạch ôn tập và checklist

## Lộ trình 14 ngày (thực hiện, không chỉ đọc)

| Ngày | Đọc sâu | Bài thực hành bắt buộc |
|---|---|---|
| 1 | Chương 1–2 | Tự giới thiệu + vẽ hệ thống nhà hàng |
| 2 | Chương 3 | Viết `Order.Confirm()/Cancel()` có validation |
| 3 | Chương 4–5 | Soạn ví dụ interface vs abstract, `new` vs `override` |
| 4 | Chương 6 | Dự đoán output reference/value và chạy kiểm chứng |
| 5 | Chương 7 | Demo const/readonly/static, ref/out/in |
| 6 | Chương 8 | Tạo class/struct/enum/record, so equality và mutation |
| 7 | Chương 9–10 | Tạo extension + LINQ + mô tả SQL được dịch |
| 8 | Chương 11 | Viết async query, CancellationToken, TryParse/exception |
| 9 | Chương 12 | Tự giải thích request pipeline và DI lifetimes |
| 10 | Chương 13 | Viết SQL JOIN, index và mô tả race condition |
| 11 | Chương 14 | Giải thích JWT và SignalR reconnect |
| 12 | Chương 15 | Lấy một bug thật, kể theo STAR hoặc RCA |
| 13 | Chương 16 | Trả lời toàn bộ 20 câu bằng giọng nói, ghi âm |
| 14 | Mock interview | Mở source hai dự án và bảo vệ mọi claim trong CV |

## Tiêu chí "đã hiểu" một chủ đề

- [ ] Tự nói định nghĩa trong 30 giây, không nhìn tài liệu.
- [ ] Giải thích cơ chế và nguyên nhân thay vì đọc cú pháp.
- [ ] Viết ví dụ C# và dự đoán output chính xác.
- [ ] Nêu ít nhất hai ưu điểm và một trade-off hoặc hạn chế.
- [ ] Phân biệt với khái niệm dễ nhầm.
- [ ] Đưa một use case thật trong dự án hoặc ghi rõ đây mới là đề xuất.
- [ ] Trả lời một câu đào sâu về concurrency, performance, test hoặc bảo mật nếu phù hợp.

## Nguồn học để kiểm chứng khi có nghi vấn

- C# Language Reference: https://learn.microsoft.com/dotnet/csharp/language-reference/
- C# Programming Guide: https://learn.microsoft.com/dotnet/csharp/programming-guide/
- .NET GC fundamentals: https://learn.microsoft.com/dotnet/standard/garbage-collection/fundamentals
- ASP.NET Core fundamentals: https://learn.microsoft.com/aspnet/core/fundamentals/
- EF Core documentation: https://learn.microsoft.com/ef/core/
- ASP.NET Core SignalR: https://learn.microsoft.com/aspnet/core/signalr/introduction
- ASP.NET Core security: https://learn.microsoft.com/aspnet/core/security/
- SQL Server documentation: https://learn.microsoft.com/sql/sql-server/

> **Tổng kết:** Để làm tốt phỏng vấn Intern, không nhất thiết dùng thuật ngữ thật khó. Cách thuyết phục nhất là **định nghĩa đúng → giải thích vì sao → ví dụ code → trade-off → liên hệ source thật**. Với nội dung trong ảnh, hãy ưu tiên kỹ 4 tính chất OOP, value/reference, access modifiers, const/readonly/static, class/struct/enum, extension methods; sau đó dựa trên CV để luyện Web API/EF Core/JWT/SignalR.

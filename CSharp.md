# 1.Kiểu dữ liệu
| Đặc điểm              | **Value Type**                                    | **Reference Type**                                          |
| --------------------- | ------------------------------------------------- | ----------------------------------------------------------- |
| Bộ nhớ lưu trữ        | Lưu **trực tiếp** giá trị ở Stack                 | Lưu **tham chiếu (địa chỉ)** đến giá trị trong Heap         |
| Khi gán cho biến khác | **Sao chép giá trị** (tạo bản sao độc lập)        | **Sao chép tham chiếu** (cùng trỏ đến vùng nhớ)             |
| Null được không?      | Không (trừ khi dùng `Nullable<T>` hoặc `int?`)    | Có thể `null`                                               |
| Vùng nhớ quản lý      | Stack (nhỏ, nhanh)                                | Heap (lớn hơn, cần GC dọn)                                  |
| Ví dụ                 | `int`, `double`, `bool`, `char`, `struct`, `enum` | `string`, `class`, `object`, `array`, `List<T>`, `delegate` |

Hỏi: Sự khác biệt giữa Value Type và Reference Type là gì?
Value type lưu trữ trực tiếp giá trị, còn Reference type lưu tham chiếu đến vùng nhớ chứa giá trị.
Khi gán, value type tạo bản sao, còn reference type dùng chung vùng nhớ.

Hỏi: Khác nhau giữa const và readonly là gì?
const: giá trị cố định tại compile-time, bắt buộc khởi tạo ngay, không thay đổi được.
readonly: cho phép gán một lần duy nhất, thường trong constructor, và cho phép gán tại runtime.

var ≠ dynamic → var vẫn là strongly typed!
object là cha của tất cả, nhưng mất thông tin kiểu cụ thể.
dynamic tắt hệ thống type checking — dùng cẩn thận!
DÙNG `dynamic` – xử lý JSON từ API không có schema
var có cả ở java và c#

- Anonymous Types (Kiểu ẩn danh):
var orders = new List<Order>
{
    new Order { Id = "ORD1", CustomerName = "Alice", Total = 250m, Status = "Shipped" },
    new Order { Id = "ORD2", CustomerName = "Bob", Total = 800m, Status = "Pending" }
};

- Tuples & Deconstruction:
nhóm nhiều giá trị khác kiểu vào một biến (C# 7+).
Deconstruction: "giải nén" tuple hoặc object thành các biến riêng lẻ.
Cú pháp: (type1, type2), hoặc (var a, var b) = tuple;

- Dynamic Type
dynamic tắt hệ thống type checking — dùng cẩn thận!
DÙNG `dynamic` – xử lý JSON từ API không có schema

- Attributes 
[Required] , [Range(0.01, 10000)], [StringLength(100)]

- Nullable Types & Null-Coalescing Operator (??)
Nullable types: Cho phép value type (int, bool, DateTime…) nhận giá trị null.
    Cú pháp: int?, DateTime?, hoặc Nullable<T>
Null-coalescing operator (??): Trả về toán hạng bên trái nếu không null, ngược lại trả về toán hạng bên phải.
Null-coalescing assignment (??=) (C# 8+): Gán giá trị chỉ khi biến hiện tại là null.

- Extension Methods
Cho phép thêm phương thức vào kiểu đã tồn tại mà không kế thừa hay sửa code gốc.
Phải là static method trong static class.
Tham số đầu tiên có tiền tố this.

- Partial Class
Cho phép chia định nghĩa một lớp thành nhiều file, Thường dùng với code sinh tự động (Entity Framework, Windows Forms, WPF).
Ví dụ e-commerce: Entity Order được sinh bởi Entity Framework, nhưng bạn muốn thêm logic
public partial class Order
{
    public string OrderId { get; set; }
    public decimal Total { get; set; }
}
public partial class Order
{
    public bool IsHighValue => Total > 1000m;
}

- Access modifier C#
| Bạn muốn...                         | Dùng modifier        |
| ----------------------------------- | -------------------- |
| Để mọi nơi dùng (API public)        | `public`             |
| Chỉ dùng trong class                | `private`            |
| Cho phép class kế thừa dùng         | `protected`          |
| Dùng trong toàn bộ project          | `internal`           |
| Kế thừa hoặc nội bộ                 | `protected internal` |
| Kế thừa nhưng giới hạn trong nội bộ | `private protected`  |

Tuy nhiên thường thì dùng private với public thôi , class con muốn dùng của cha thì dùng hàm get,set hoặc dùng base
- Trong Java thì cũng tương đương
| C# Modifier          | Java tương đương                 |
| -------------------- | -------------------------------- |
| `private`            | `private`                        |
| `public`             | `public`                         |
| `protected`          | `protected`                      |
| `internal`           | *(default)* (package-private)    |
| `protected internal` | ❌ Không có tương đương trực tiếp |
| `private protected`  | ❌ Không có trong Java            |

- namespace
| Ý chính             | Nội dung                                   |
| ------------------- | ------------------------------------------ |
| `namespace` dùng để | Nhóm logic class/struct/interface/enum lại |
| Lợi ích             | Tránh trùng tên, tổ chức code rõ ràng      |
| Dùng bằng           | `using NamespaceName;` hoặc viết đầy đủ    |
| C# 10 trở lên có    | `file-scoped namespace` gọn hơn            |

- sealed là từ khóa dùng để ngăn không cho class bị kế thừa, hoặc ngăn method bị override tiếp ở lớp con kế tiếp.

- ref và out và in
| Loại dữ liệu                            | Kiểu truyền mặc định      | Hành vi khi thay đổi trong hàm                                                  |
| --------------------------------------- | ------------------------- | ------------------------------------------------------------------------------- |
| Value type (int, struct...)             | Truyền bản sao giá trị    | Không ảnh hưởng bản gốc                                                         |
| Reference type (class, object, list...) | Truyền bản sao tham chiếu | Thay đổi thuộc tính → ảnh hưởng bản gốc<br>Gán lại object mới → không ảnh hưởng |
| ref / out                               | Truyền tham chiếu thật sự | Có thể thay đổi cả biến gốc                                                     |

+ ref cho phép truyền một biến theo tham chiếu, nghĩa là phương thức có thể thay đổi giá trị của biến gốc bên ngoài.
Biến phải được khởi tạo trước khi truyền vào. không bắt buộc gán lại bên trong method.
void UpdateValue(ref int x)
{
    x = x + 10;
}

int a = 5;
UpdateValue(ref a);
Console.WriteLine(a); // 👉 15

+ out cũng truyền theo tham chiếu, nhưng dùng để truyền giá trị trả ra, bắt buộc phải gán giá trị trong method trước khi trả ra.
Biến không cần khởi tạo trước khi truyền vào.
void GetValues(out int x, out int y)
{
    x = 10;
    y = 20;
}

int a, b;
GetValues(out a, out b);
Console.WriteLine(a); // 👉 10
Console.WriteLine(b); // 👉 20

+ in
Truyền tham chiếu để tối ưu hiệu năng (tránh copy), nhưng không được phép thay đổi giá trị bên trong phương thức.
Phải gán giá trị trước khi truyền.
Bên trong method không được phép gán lại.

| Tiêu chí                                  | `ref`   | `out`   | `in`               |
| ----------------------------------------- | ------- | ------- | ------------------ |
| Truyền tham chiếu?                        | ✅       | ✅       | ✅                  |
| Bắt buộc gán giá trị trước khi gọi?       | ✅ Có    | ❌ Không | ✅ Có               |
| Bắt buộc gán giá trị bên trong method?    | ❌ Không | ✅ Có    | ❌ Không            |
| Có thể thay đổi giá trị bên trong method? | ✅ Có    | ✅ Có    | ❌ Không            |
| Tính năng từ phiên bản C# nào?            | C# 1.0  | C# 1.0  | C# 7.2             |
| Dùng với `readonly struct`?               | Không   | Không   | ✅ Có, rất hiệu quả |

Có thể overload method theo ref, out, in

- Nếu dùng biến kiểu tham chiếu (reference type) – như object, array, List<T>, Dictionary<K,V> thì không cần ref,out do nó hoàn toàn có thể thay đổi được bên trong hàm do nó là tham chiếu sẵn rồi, chỉ dùng khi muốn thay đổi hoàn toàn tạo mới thôi

# 2.Delegate, Event và Func/Action/Predicate
Delegate là con trỏ đến phương thức trong C#.
Nó đóng gói một hoặc nhiều phương thức có cùng chữ ký (signature): cùng kiểu trả về, cùng tham số.
Là kiểu tham chiếu an toàn kiểu (type-safe function pointer).
Đơn giản là "Một biến có thể lưu trữ và gọi một hàm." 

// 1. Khai báo delegate
public delegate void OrderProcessedHandler(string orderId, bool success);
// 2. Phương thức phù hợp
public void SendEmailNotification(string orderId, bool success)
{
    Console.WriteLine($"[Email] Đơn {orderId} {(success ? "thành công" : "thất bại")}");
}
public void UpdateInventory(string orderId, bool success)
{
    if (success)
        Console.WriteLine($"[Kho] Cập nhật tồn kho cho đơn {orderId}");
}
// 3. Sử dụng
var handler = new OrderProcessedHandler(SendEmailNotification);
handler("ORD-123", true); // Gọi như hàm bình thường

- Delegate đa hướng (Multicast Delegate)
Là delegate có thể trỏ đến nhiều phương thức cùng lúc.
Được tạo bằng cách kết hợp (combine) các delegate đơn lẻ bằng toán tử + hoặc +=.
Khi gọi, tất cả phương thức được gọi theo thứ tự.
Chỉ hoạt động với delegate trả về void (nếu có giá trị trả về, chỉ giá trị của phương thức cuối cùng được giữ lại).

Ví dụ e-commerce: Xử lý sau khi đơn hàng được xử lý
Giả sử khi đơn hàng xử lý xong, bạn cần:
    Gửi email thông báo
    Cập nhật tồn kho
    Ghi log
→ Dùng multicast delegate để kết hợp các hành động.

public delegate void OrderProcessedHandler(string orderId, bool success);
public class OrderService
{
    public void ProcessOrder(string orderId)
    {
        // Giả lập xử lý
        bool success = true;

        // Tạo multicast delegate
        OrderProcessedHandler notificationHandler = SendEmailNotification;
        notificationHandler += UpdateInventory;
        notificationHandler += LogOrderStatus;

        // Gọi tất cả
        notificationHandler?.Invoke(orderId, success);
    }

    private void SendEmailNotification(string orderId, bool success)
        => Console.WriteLine($"[Email] Đơn {orderId} {(success ? "thành công" : "thất bại")}");

    private void UpdateInventory(string orderId, bool success)
    {
        if (success)
            Console.WriteLine($"[Kho] Cập nhật tồn kho cho đơn {orderId}");
    }

    private void LogOrderStatus(string orderId, bool success)
        => Console.WriteLine($"[Log] {DateTime.Now}: {orderId} - {(success ? "OK" : "FAIL")}");
}

- `Action`, `Func`, `Predicate` là multi delegate cung cấp sẵn, tuy nhiên chỉ nên dùng multi delegate với Action
+ Action Trả về: void
Tham số: 0 → 16 tham số kiểu generic
Dùng khi: Thực hiện hành động không cần kết quả trả về
Action                    // () => void
Action<T>                 // (T) => void
Action<T1, T2>            // (T1, T2) => void
...
Action<T1, ..., T16>      // (T1, ..., T16) => void

public class NotificationService
{
    public void SendOrderConfirmation(string orderId, string email)
        => Console.WriteLine($"Gửi email xác nhận cho {email} - Đơn: {orderId}");
}

// Sử dụng
var notify = new Action<string, string>(new NotificationService().SendOrderConfirmation);
notify("ORD-100", "user@example.com");

// Hoặc dùng lambda
Action<string> logOrder = orderId => Console.WriteLine($"[LOG] Đã tạo đơn: {orderId}");
logOrder("ORD-101");

+ Func Trả về: Có giá trị (TResult), chỉ trả về kết quả hàm cuối + vào nếu là mutil delegate
Tham số: 0 → 16 tham số đầu vào + 1 kiểu trả về
Dùng khi: Cần tính toán và trả kết quả
Func<TResult>                // () => TResult
Func<T, TResult>             // (T) => TResult
Func<T1, T2, TResult>        // (T1, T2) => TResult
...
Func<T1, ..., T16, TResult>  // (T1, ..., T16) => TResult

// Tính VAT
Func<decimal, decimal> calculateVat = amount => amount * 0.1m;
// Tính giá cuối
Func<decimal, decimal> addVat = amount => amount + calculateVat(amount);
var finalPrice = addVat(1000m); // → 1100m
// Dùng trong LINQ: lấy danh sách đơn hàng cao cấp
var highValueOrders = orders.Where(o => o.Total > 500)
                            .Select(o => new { o.Id, DiscountedPrice = addVat(o.Total * 0.9m) });

+ Predicate Là Func<T, bool> — nhưng ngữ nghĩa rõ ràng hơn cho điều kiện
Dùng khi: Lọc, kiểm tra điều kiện đúng/sai
Predicate<T>  // (T) => bool

Predicate<Order> isValidOrder = order =>
    order != null &&
    !string.IsNullOrEmpty(order.CustomerId) &&
    order.Total > 0;

// Dùng với List<T>.FindAll
var validOrders = allOrders.FindAll(isValidOrder);

// Hoặc trong validation
if (!isValidOrder(newOrder))
    throw new InvalidOperationException("Đơn hàng không hợp lệ!");


# 3. Events và EventHandler
Event là cơ chế publisher-subscriber an toàn, dựa trên multicast delegate.
event là thông báo một chiều — publisher không quan tâm subscriber làm gì hay trả về gì.
Nếu bạn cần phản hồi, hãy dùng callback, command pattern, hoặc message with response.
Chỉ lớp chứa event mới có thể kích hoạt (invoke) nó — subscriber chỉ có thể đăng ký (+=) hoặc hủy đăng ký (-=).
💡 Think of it as: "Đăng ký nhận tin — không cần biết ai gửi, chỉ cần phản ứng khi có tin." 

- EventHandler .NET cung cấp hai delegate chuẩn cho sự kiện, đều trả về void giống action:
🔹 EventHandler
public delegate void EventHandler(object sender, EventArgs e);
Dùng cho sự kiện không cần dữ liệu bổ sung.

🔹 EventHandler<TEventArgs>
public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e)
    where TEventArgs : EventArgs;
Dùng khi bạn cần truyền dữ liệu kèm theo sự kiện (phải kế thừa EventArgs).

Ví dụ e-commerce: Xử lý đơn hàng và thông báo
Bước 1: Định nghĩa EventArgs tùy chỉnh 
    public class OrderProcessedEventArgs : EventArgs
Bước 2: Lớp phát hành sự kiện (Publisher)
    public class OrderService
Bước 3: Các subscriber (người nghe)
    public class EmailService
    public class InventoryService
    public class LoggingService
Bước 4: Đăng ký và sử dụng
    // Đăng ký sự kiện
    orderService.OrderProcessed += email.HandleOrderProcessed;
    orderService.OrderProcessed += inventory.HandleOrderProcessed;
    orderService.OrderProcessed += logger.HandleOrderProcessed;
    // Xử lý đơn hàng
    orderService.ProcessPayment("ORD-2024-001", 1200m);

- Memory Leak khi dùng Event:
"Khi một đối tượng A (subscriber) đăng ký vào event của đối tượng B (publisher), thì B giữ một tham chiếu mạnh (strong reference) đến A."
→ Nếu B sống lâu hơn A, thì A không được giải phóng bởi GC, dù A đã "hết việc". 
Cách khắc phục : Hủy đăng ký khi không cần nữa (dùng IDisposable)

- IDisposable là interface chuẩn của .NET định nghĩa một phương thức duy nhất:
public interface IDisposable
{
    void Dispose();
}
Phương thức Dispose() dùng để giải phóng tài nguyên một cách chủ động, ngay lập tức, thay vì chờ Garbage Collector (GC).
    Timer, Event, hoặc event subscriptions có thể bị giữ reference
    Database connections (SqlConnection, DbContext)
    File handles (file, stream)
    Network socket

Dùng từ khoá using để tự động gọi Dispose() khi ra khỏi phạm vi.
public class FileLogger : IDisposable
    public void Dispose()
    {
        _fileStream?.Dispose(); // Giải phóng tài nguyên
    }
Gọi
public void Dispose() => _httpClient.Dispose();

// Finalizer — chỉ nếu có unmanaged
~FileLogger()
{
    Dispose(disposing: false);
}
Luôn dùng using Với FileStream , SqlConnection , HttpClient, v.v.

❓IDisposable dùng để làm gì?
Trả lời: Để giải phóng tài nguyên không quản lý bởi GC như file, stream, connection,... giúp tránh memory leak và chiếm tài nguyên không cần thiết.

❓Sự khác biệt giữa Dispose và Finalize là gì?
| Thuộc tính  | `Dispose()`                                            | `Finalize()`             |
| ----------- | ------------------------------------------------------ | ------------------------ |
| Gọi bởi     | Lập trình viên (thông qua `using`, hoặc gọi trực tiếp) | Hệ thống GC              |

- So sánh nhanh: Stream trong C# vs Stream trong Java
| Tiêu chí              | **Stream trong C#**                                           | **Stream trong Java (Java 8+)**                                 |
| --------------------- | ------------------------------------------------------------- | --------------------------------------------------------------- |
| Mục đích chính        | Xử lý **luồng dữ liệu I/O** (File, Network, Memory...)        | Xử lý **luồng dữ liệu dạng tập hợp (Collection)** theo kiểu hàm |
| Thuộc thư viện        | `System.IO.Stream`                                            | `java.util.stream.Stream<T>`                                    |
| Là gì?                | **Abstract class** đại diện cho I/O stream                    | **Interface** để xử lý collection dạng pipeline                 |
| Tính năng nổi bật     | Read/Write byte, position, seek                               | `map`, `filter`, `reduce`, `collect`, lazy evaluation           |
| Gần giống gì bên kia? | C#'s `Stream` gần giống Java's `InputStream` / `OutputStream` | Java's `Stream<T>` gần giống C#'s **LINQ**                      |
LINQ trong C# mới là thứ tương đương với Java Stream

# 4.Collections và LINQ
1. Danh sách (List-like)    Truy cập theo chỉ số, thứ tự quan trọng
2. Tập hợp (Set-like)       Lưu giá trị duy nhất, không thứ tự
3. Từ điển (Map/Dictionary) Cặp key-value
4. Hàng đợi & Ngăn xếp      Truy cập theo nguyên tắc FIFO/LIFO

Collections bất biến (Immutable Collections) 
ImmutableList<T>, ImmutableHashSet<T>, ImmutableDictionary<TKey, TValue>, v.v.
Không thể sửa đổi — mọi thao tác trả về bản sao mới
An toàn cho đa luồng, hashable, dễ test
 -> Dùng immutable collections cho cấu hình, DTO, state trong functional programming
Thread-safe collections: ConcurrentDictionary,ConcurrentQueue...

List là mảng động x2 lên khi đầy, array là mảng thường
Dictionary<TKey, TValue> dùng tốt hơn Hashtable, nhanh hơn

Cứ hash thì tìm là O(1)
| Hành động                             | **List**                           | **Set**                                                  | **Map**                                                  |
| ------------------------------------- | ---------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| **Tìm 1 phần tử (contains / search)** | `O(n)` – phải duyệt toàn bộ list   | `O(1)` trung bình (HashSet)<br>`O(log n)` nếu là TreeSet | `O(1)` trung bình (HashMap)<br>`O(log n)` nếu là TreeMap |
| **Lấy phần tử theo chỉ số / key**     | `O(1)` (bằng index)                | ❌ Không có chỉ số                                        | `O(1)` trung bình với key                                |
| **Thêm phần tử**                      | `O(1)` trung bình (cuối danh sách) | `O(1)` HashSet<br>`O(log n)` TreeSet                     | `O(1)` HashMap<br>`O(log n)` TreeMap                     |
| **Xóa phần tử**                       | `O(n)` – phải tìm vị trí trước     | `O(1)` HashSet<br>`O(log n)` TreeSet                     | `O(1)` HashMap<br>`O(log n)` TreeMap                     |
| **Cho phép trùng lặp**                | ✅ Có                               | ❌ Không                                                  | ❌ Key không trùng (value có thể trùng)                   |
| **Giữ thứ tự**                        | ✅ Có (List giữ insertion order)    | ❌ HashSet không giữ<br>✅ LinkedHashSet giữ               | ❌ HashMap không giữ<br>✅ LinkedHashMap giữ               |


- LINQ = Language Integrated Query
Là tập hợp các tính năng trong C# cho phép viết truy vấn kiểu SQL để lọc, sắp xếp, nhóm, biến đổi dữ liệu từ:
    Collections (List<T>, Array, v.v.)
    Database (Entity Framework Core)
    XML (XDocument)
    JSON (thông qua thư viện)
    Và bất kỳ nguồn nào implement IEnumerable<T> hoặc IQueryable<T>
💡 LINQ không phải là ORM — nó là ngôn ngữ truy vấn tích hợp, còn Entity Framework là ORM dựa trên LINQ. 
- Hai cú pháp LINQ :
+ Query Syntax (giống SQL):
var result = from product in products
             where product.Price > 100
             orderby product.Name
             select product;

+ Method Syntax (dùng extension methods):
var result = products
    .Where(p => p.Price > 100)
    .OrderBy(p => p.Name);

| Phương thức           | Ý nghĩa                                    | Ví dụ                       |
| --------------------- | ------------------------------------------ | --------------------------- |
| `Where()`             | Lọc theo điều kiện                         | `Where(x => x.Price > 100)` |
| `Select()`            | Dựng lại đối tượng mới                     | `Select(p => p.Name)`       |
| `OrderBy()`           | Sắp xếp tăng dần                           | `OrderBy(p => p.Name)`      |
| `GroupBy()`           | Nhóm theo khóa                             | `GroupBy(p => p.Category)`  |
| `Any()` / `All()`     | Kiểm tra có phần tử nào thỏa / tất cả thỏa | `Any(x => x.IsActive)`      | Trả về true, false
| `First()`, `Single()` | Lấy phần tử đầu tiên / duy nhất            | `First(p => p.Age > 18)`    |
FirstOrDefaul, SingleOrDefault 
Nếu single >1 hoặc =0 thì đều là ko đúng vì chỉ lấy 1, do đó thường dùng lấy product theo id
First, Single trả về entity, Where, Select, GroupBy,.. trả về IEnumerable/IQueryable, Any,All trả về boolean true, false
Sum, Average trả về int,decimal , ToList trả về List, ToArray trả về Array
Include là method của Entity Framework (EF) dùng để Eager Loading, tức là load luôn các entity liên quan khi truy vấn, tránh vấn đề Lazy Loading n+1 queries.
✅ Method syntax được ưa chuộng hơn vì: 
    Hỗ trợ tất cả toán tử LINQ (query syntax thiếu một số như Count, Aggregate)
    Dễ kết hợp với lambda
    Dễ debug từng bước

- Lazy và Eager loading
+ Lazy EF không load các navigation property liên quan ngay khi query chính, mà chỉ load khi bạn truy cập property đó lần đầu.
Ví dụ: bạn load một Order nhưng không load OrderItems. Khi bạn gọi order.OrderItems, EF sẽ tự động gửi SQL query thứ hai để lấy dữ liệu này.
var orders = context.Orders.ToList(); // chỉ load Orders

foreach (var order in orders)
{
    // lúc này mới query OrderItems cho từng order
    var items = order.OrderItems;
}
Vấn đề n+1 queries:
    1 query load Orders → n query load OrderItems cho từng order → tổng 1 + n queries
    Nếu 100 Orders, sẽ có 101 queries → rất tốn performance

+ Eager Loading
Dùng .Include() hoặc .ThenInclude() để load luôn các entity liên quan trong 1 query.
Tránh n+1 queries, tối ưu performance.
var orders = context.Orders
                    .Include(o => o.OrderItems)
                    .ToList(); // tất cả OrderItems load cùng Orders
-> Mặc định bản mới là bật lazy load, bản cũ là eager
| EF Version | Mặc định                                                                              |
| ---------- | ------------------------------------------------------------------------------------- |
| EF Core    | **Lazy Loading tắt mặc định**, chỉ load entity chính (Eager Loading nếu dùng Include) |
| EF6        | Lazy Loading **bật mặc định**, navigation properties load khi truy cập                |


- Ví dụ
+ Tình huống: Xử lý giỏ hàng và báo cáo doanh thu
var products = new List<Product>
{
    new Product { Id = "P1", Name = "Laptop", Price = 1200m, Category = "Electronics" },
    new Product { Id = "P2", Name = "Mouse", Price = 25m, Category = "Electronics" },
    new Product { Id = "P3", Name = "Book", Price = 15m, Category = "Books" }
};

// 1. Lọc sản phẩm điện tử trên $50
var expensiveElectronics = products
    .Where(p => p.Category == "Electronics" && p.Price > 50)
    .ToList();

// 2. Tính tổng doanh thu theo danh mục
var revenueByCategory = products
    .GroupBy(p => p.Category)
    .Select(g => new { Category = g.Key, Total = g.Sum(p => p.Price) })
    .ToList();

// 3. Tìm sản phẩm rẻ nhất
var cheapest = products.MinBy(p => p.Price); // C# 10+

// 4. Kiểm tra xem có sản phẩm nào trên $1000 không
bool hasHighValue = products.Any(p => p.Price > 1000);

+ Dùng với Entity Framework Core (truy vấn database)
// Trả về IQueryable — chưa thực thi SQL
var highValueOrders = _context.Orders
    .Where(o => o.Total > 500)
    .OrderByDescending(o => o.CreatedAt)
    .Select(o => new { o.Id, o.CustomerName, o.Total });

// Chỉ khi gọi .ToList(), .First(), v.v. → mới gọi DB
var list = highValueOrders.ToList();
→ LINQ giúp bạn viết query database như thao tác collection!

- Cơ chế quan trọng: Deferred Execution (Thực thi trì hoãn):
Hầu hết toán tử LINQ (Where, Select, OrderBy) không thực thi ngay — chúng trả về IEnumerable<T> "lười".
Dữ liệu chỉ được duyệt khi bạn gọi:
    .ToList(), .ToArray()
    foreach
    .First(), .Single(), .Count(), v.v.

VD:
var numbers = new List<int> { 1, 2, 3 };
var query = numbers.Where(x => x > 1); // ← CHƯA DUYỆT

numbers.Add(4); // Thêm sau khi định nghĩa query

// Bây giờ mới duyệt → kết quả: 2, 3, 4
foreach (var n in query)
    Console.WriteLine(n);

Lưu ý: Khi dùng với IQueryable<T> (EF Core) Không gọi method trong lambda mà chỉ so sánh bình thường bên trong thôi
// ❌ LỖI: EF không biết dịch IsHighValue thành SQL
bool IsHighValue(decimal total) => total > 500;
var orders = context.Orders.Where(o => IsHighValue(o.Total)); // NotSupportedException

- Tracking vs NoTracking trong EF
+ Tracking khi bạn truy vấn dữ liệu với EF, EF sẽ theo dõi (track) các entity được load từ database.Khi gọi SaveChanges(), EF tự động update những entity đã thay đổi
+ AsNoTracking() tắt tracking cho entity khi query.EF sẽ không theo dõi entity tăng performance khi chỉ đọc dữ liệu.
    var products = context.Products
                          .AsNoTracking()
                          .Where(p => p.CategoryId == 1)
                          .ToList();
    products[0].Price = 500; 
    context.SaveChanges(); // ❌ Không có effect, EF không track entity

- Lưu ý:
Include()
Phải OrderBy() trước Skip(), Take() Khi phân trang → nếu không sẽ lỗi SQL / kết quả không ổn định
Nên dùng FirstOrDefault thay cho First vì ko bị lỗi nếu ko có dữ liệu trả về


Câu hỏi 1: “Sự khác biệt giữa IEnumerable và IQueryable trong LINQ?”
“- IEnumerable<T>: Dùng cho collections trong bộ nhớ (List, Array).
→ Lambda biên dịch thành delegate, thực thi trong C#.
IQueryable<T>: Dùng cho nguồn dữ liệu từ xa (database, API).
→ Lambda biên dịch thành expression tree, được provider (EF Core) dịch sang SQL.
Trong e-commerce, tôi dùng IQueryable để tối ưu truy vấn database — chỉ lấy dữ liệu cần thiết, không load toàn bộ bảng.” 
IQueryable → dịch sang SQL (EF Core), IEnumerable → chạy trong bộ nhớ.

Câu hỏi 2: “Khi nào nên dùng LINQ thay vì vòng lặp for?”
“Tôi dùng LINQ khi logic liên quan đến truy vấn dữ liệu: lọc, sắp xếp, nhóm, tổng hợp.
Dùng vòng lặp for khi:
    Cần chỉ số (index) cụ thể
    Thực hiện side-effect phức tạp (không phải transform dữ liệu)
    Hiệu năng cực hạn chế (LINQ có overhead nhỏ)
    Trong e-commerce, 95% trường hợp tôi dùng LINQ — code ngắn gọn, dễ đọc, ít bug.” 

# 5.Generics
Generics cho phép bạn định nghĩa kiểu dữ liệu tổng quát, mà không chỉ định cụ thể kiểu trong quá trình viết code – kiểu sẽ được xác định khi sử dụng (compile time).

where T : ... – Ràng buộc kiểu (Generic Constraints)
| Cú pháp                    | Ý nghĩa                                 |
| -------------------------- | --------------------------------------- |
| `where T : class`          | T phải là **reference type**            |
| `where T : struct`         | T phải là **value type**                |
| `where T : new()`          | T phải có **constructor không tham số** |
| `where T : SomeBaseClass`  | T phải kế thừa từ `SomeBaseClass`       |
| `where T : ISomeInterface` | T phải implement interface              |
| `where T : class, new()`   | Kết hợp nhiều ràng buộc                 |

public interface IAnimal { void Speak(); }
public class Zoo<T> where T : IAnimal, new()
{
    public void ShowAnimal()
    {
        T animal = new T();
        animal.Speak();
    }
}

# 6.Threading, Task, và Async/Await trong C#
- Thread vs Task – Khác biệt và cách dùng
| Tiêu chí               | `Thread`                         | `Task`                                        |
| ---------------------- | -------------------------------- | --------------------------------------------- |
| Cấp độ                 | **Thấp** (Low-level API)         | **Cao hơn**, trừu tượng hơn                   |
| Khởi tạo               | `new Thread(...)`                | `Task.Run(...)`, `Task.Factory.StartNew(...)` |
| Đa luồng?              | ✅ Có                             | ✅ Có (dùng thread pool)                       |
| Điều phối (scheduling) | Do bạn tự quản lý                | .NET tự quản lý (ThreadPool)                  |
| Ưu tiên sử dụng        | Khi cần kiểm soát luồng chi tiết | Khi xử lý bất đồng bộ / I/O-bound             |

💡 Khi nào dùng Thread? Khi cần điều khiển chi tiết (pause/resume/priority).
💡 Khi nào dùng Task? Khi muốn xử lý bất đồng bộ hoặc song song (đa luồng nhẹ hơn Thread).

| Thành phần | Mục tiêu                                                                          |
| ---------- | --------------------------------------------------------------------------------- |
| `Thread`   | Tạo **luồng thực** để thực hiện song song                                         |
| `Task`     | Thực hiện **tác vụ bất đồng bộ hoặc song song**, sử dụng **ThreadPool** để tối ưu |
Task Dựa trên ThreadPool – không tạo mới luồng mỗi lần, Reuse thread pool Hỗ trợ async/await

- async / await – Bất đồng bộ (Asynchronous)
async biến hàm thành bất đồng bộ.
await chờ task hoàn thành mà không block thread hiện tại.

| Kiểu                           | Mô tả                                                                                |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| **Synchronous (Đồng bộ)**      | Thực hiện **tuần tự**, tác vụ sau phải **chờ** tác vụ trước hoàn thành               |
| **Asynchronous (Bất đồng bộ)** | Cho phép **tiếp tục chạy tác vụ khác** trong khi chờ tác vụ chưa xong (non-blocking) |

| Tiêu chí              | Synchronous                                      | Asynchronous                                              |
| --------------------- | ------------------------------------------------ | --------------------------------------------------------- |
| **Cơ chế hoạt động**  | Blocking – chạy từng bước, chờ mỗi bước hoàn tất | Non-blocking – không chờ, có thể tiếp tục xử lý việc khác |
| **Hiệu suất**         | Thấp hơn nếu có I/O hoặc delay                   | Tối ưu tài nguyên – tốt cho xử lý I/O                     |
| **Độ phức tạp code**  | Dễ hiểu hơn                                      | Phức tạp hơn nhưng linh hoạt                              |
| **Ứng dụng tốt nhất** | CPU-bound tasks (tính toán)                      | I/O-bound tasks (API, DB, File, Network)                  |
| **Dùng từ khóa?**     | Không                                            | `async`, `await`, `Task`                                  |
| **Blocking UI?**      | Có thể gây treo UI                               | Tránh treo UI nếu dùng đúng                               |

- Parallel.ForEach, Task.WhenAll, CancellationToken
+ Parallel.ForEach – Lặp song song (multi-threaded)
    Duyệt qua tập hợp và xử lý nhiều phần tử song song.
    Tận dụng CPU đa nhân (multi-core).
+ Task.WhenAll – Chờ nhiều Task hoàn thành
    Chạy nhiều task bất đồng bộ cùng lúc
    Chờ tất cả task hoàn tất rồi mới đi tiếp
+ CancellationToken – Hủy task an toàn
    Cho phép người dùng/người gọi chủ động hủy một task đang chạy.
    Ví dụ: hủy upload file, hủy xử lý đơn hàng đang chờ...

- Deadlock (bế tắc) xảy ra khi:
Deadlock là hiện tượng khi nhiều luồng cùng chờ tài nguyên mà các luồng khác đang giữ, khiến chúng không thể tiếp tục.
Làm sao tránh deadlock?
    Khóa tài nguyên theo thứ tự nhất định
    Sử dụng TryEnter, SemaphoreSlim, hoặc timeout khi cần chờ tài nguyên

- Lock 
    Đảm bảo chỉ 1 thread được phép thực thi code bên trong critical section cùng lúc.
    Ngăn race condition khi nhiều thread thao tác cùng dữ liệu chung.

    lock(_lockObj)
    {
        // critical section
    }

# 7.ASP.NET MVC / ASP.NET Core MVC / Web API
Routing trong ASP.NET MVC hoạt động ra sao?
Routing ánh xạ URL đến controller và action thông qua cấu hình route trong Startup.cs. Ví dụ URL /Product/Details/5 sẽ gọi ProductController.Details(5).

Các loại ActionResult phổ biến? Khi nào dùng?
| ActionResult         | Dùng khi                            |
| -------------------- | ----------------------------------- |
| `View()`             | Trả HTML                            |
| `Json()`             | Trả dữ liệu cho frontend (AJAX/API) |
| `RedirectToAction()` | Chuyển hướng nội bộ                 |
| `File()`             | Tải file về                         |
| `Content()`          | Trả text/raw                        |

| Thành phần   | Vai trò chính                  | Ghi chú                    |
| ------------ | ------------------------------ | -------------------------- |
| Model        | Đại diện dữ liệu & nghiệp vụ   | Entity, ViewModel, Service |
| View         | Giao diện hiển thị             | Razor, HTML                |
| Controller   | Xử lý yêu cầu                  | Chứa các action            |
| Routing      | Ánh xạ URL → Controller/Action | Cấu hình trong Startup.cs  |
| ActionResult | Kết quả trả về từ controller   | View, Json, Redirect...    |

- Model binding
là quá trình tự động ánh xạ dữ liệu từ request (form, query string, route, body) vào tham số của Action hoặc ViewModel.
| Nguồn             | Ví dụ                        |
| ----------------- | ---------------------------- |
| Form fields       | `<input name="FirstName" />` |
| Query string      | `/Product?id=5`              |
| Route values      | `/Product/Details/5`         |
| JSON Body (API)   | `{ "name": "Laptop" }`       |
| Headers / Cookies | (có thể custom bind)         |

- Validation : ModelState.IsValid sẽ kiểm tra các annotation.
[Required], [Range(1000, 100000)],..
if (!ModelState.IsValid)
    return View(model);

- FluentValidation Viết 1 class validate riêng rồi đăng ký trong Startup.cs

- Razor Pages
Một file .cshtml chứa HTML và Razor logic
Một file .cshtml.cs chứa logic xử lý (PageModel class)

- Partial View và Layout
Layout là “khung HTML tổng quát” chứa header, footer, sidebar, scripts…, dùng chung cho nhiều trang
Partial View là Thành phần nhỏ trong giao diện, có thể tái sử dụng chứa một phần giao diện riêng biệt như header, form, item list…

- Middleware
Middleware là các thành phần trung gian trong pipeline xử lý HTTP của ASP.NET Core.
Chúng có thể chặn, sửa,  request/response.
Chặn, sửa đổi, dừng, Validate, hoặc chuyển tiếp request/response.
Ghi log, xác thực (auth), nén, cache, CORS, bắt lỗi, v.v.
Đăng ký Middleware trong Startup.cs

Một số Middleware phổ biến:
| Middleware            | Chức năng                                           |
| --------------------- | --------------------------------------------------- |
| `UseRouting()`        | Thiết lập route                                     |
| `UseAuthentication()` | Xác thực người dùng                                 |
| `UseAuthorization()`  | Kiểm tra quyền                                      |
| `UseStaticFiles()`    | Phục vụ file tĩnh (js, css, img)                    |
| `UseEndpoints()`      | Xử lý endpoint cuối cùng (controller, RazorPage...) |

Thứ tự rất quan trọng! Ví dụ: UseAuthentication() phải đặt trước UseAuthorization()

- Filters 
là các lớp cho phép bạn chèn logic tùy chỉnh vào trước hoặc sau các bước xử lý của Controller/Action.

- HTTP Method trong RESTful API
| HTTP Verb | Hành động        | Ý nghĩa REST   |
| --------- | ---------------- | -------------- |
| `GET`     | Lấy dữ liệu      | Đọc            |
| `POST`    | Tạo mới          | Thêm mới       |
| `PUT`     | Cập nhật toàn bộ | Thay thế       |
| `PATCH`   | Cập nhật 1 phần  | Sửa 1 phần     |
| `DELETE`  | Xoá              | Xóa tài nguyên |

# 8. Entity Framework (EF)
Entity Framework (EF) là một ORM (Object-Relational Mapper) giúp bạn:
    Giao tiếp với CSDL thông qua các class C#
    Không cần viết SQL thủ công cho CRUD
    Tự map giữa table (CSDL) và class (model C#)

| Phiên bản                | Ghi chú                                              |
| ------------------------ | ---------------------------------------------------- |
| EF6 (Entity Framework 6) | Truyền thống, dùng trong .NET Framework              |
| EF Core (EF7, EF8…)      | Phiên bản hiện đại, cross-platform, nhẹ hơn, tốt hơn |

| Cách tiếp cận             | Mô tả                          |
| ------------------------- | ------------------------------ |
| **Code First**            | Tạo model C# → EF tạo DB       |
| **Database First**        | Có sẵn DB → sinh model tự động |
| **Model First** (ít dùng) | Vẽ sơ đồ → sinh code & DB      |

| Khái niệm | Mô tả                       |
| --------- | --------------------------- |
| EF        | ORM giúp map class ↔ table  |
| DbContext | Cửa giao tiếp với DB        |
| DbSet     | Đại diện cho 1 bảng         |
| Migration | Theo dõi thay đổi schema DB |
| LINQ      | Query dữ liệu như SQL       |
| Include   | JOIN dữ liệu                |
| Tracking  | Theo dõi thay đổi entity    |

Entity State
| State     | Ý nghĩa                    |
| --------- | -------------------------- |
| Added     | Entity mới, sẽ được insert |
| Modified  | Entity bị sửa, sẽ update   |
| Deleted   | Entity bị xóa              |
| Unchanged | Không thay đổi             |
| Detached  | Không thuộc context nào    |

Làm sao để optimize hiệu năng EF?
    Dùng AsNoTracking() cho query chỉ đọc
    Dùng Select() chỉ lấy field cần thiết
    Tránh Include() dư thừa
    Dùng FirstOrDefault() thay vì ToList() nếu chỉ lấy 1 item
    Paging bằng Skip() + Take()

- Lưu ý về include()
Include() trong Entity Framework dùng để load các navigation property (liên kết) cùng lúc với entity chính.
Include() chỉ thêm thông tin “muốn load thêm bảng nào” vào biểu thức truy vấn, nhưng không thực thi gì cả cho đến khi toàn bộ query được "materialize" (chuyển thành dữ liệu thật bằng .ToList(), .First(), v.v.).

EF là ORM giúp map C# class với bảng DB, xử lý CRUD không cần SQL thủ công. Khác với ADO.NET là thao tác SQL trực tiếp, EF cung cấp API kiểu hướng đối tượng.

- Quá trình Code First
Tạo class C# (entity): biểu diễn bảng DB
Tạo DbContext: khai báo các bảng (DbSet)
Tạo migration: EF tạo file chứa lệnh tạo bảng
Apply migration: cập nhật schema xuống DB

- Migration – Quản lý schema DB qua code
✅ 1. Cài đặt EF CLI
dotnet tool install --global dotnet-ef

✅ 2. Tạo migration
dotnet ef migrations add InitialCreate

✅ 3. Update database
dotnet ef database update
➡️ Tạo DB nếu chưa có
➡️ Thực thi các lệnh trong migration lên DB thật

✅ 4. Thay đổi model → Tạo migration mới
Ví dụ: thêm trường Stock vào Product
public int Stock { get; set; } // thêm vào Product

dotnet ef migrations add AddStockToProduct
dotnet ef database update

🔁 5. Rollback Migration
Quay về migration trước
    dotnet ef database update LastMigrationName

Xóa migration cuối chưa apply
    dotnet ef migrations remove

Nếu sửa tên field trong Model thì EF xử lý sao?
    EF sẽ xem là xoá field cũ, tạo field mới
    Nếu bạn muốn đổi tên cột thật sự (không mất dữ liệu), cần dùng:
    migrationBuilder.RenameColumn(
        name: "OldName",
        table: "TableName",
        newName: "NewName");

- DbContext, DbSet
| Thành phần  | Vai trò                                                 |
| ----------- | ------------------------------------------------------- |
| `DbContext` | **Cửa giao tiếp giữa ứng dụng và database**             |
| `DbSet<T>`  | Đại diện cho **1 bảng trong DB**, dùng để thao tác CRUD |

DbContext Là lớp trung tâm của Entity Framework, giúp bạn, Kết nối tới database, Quản lý entity (model), Theo dõi thay đổi (Change Tracking), Sinh lệnh SQL từ LINQ, Áp dụng Migration

DbSet<T> là đại diện cho 1 bảng trong database, nơi bạn thực hiện: Add(), Remove(), Find(), ToList(), Where()...

| Entity Framework (C#)   | Spring Boot (Java)               | Vai trò tương tự  |
| ----------------------- | -------------------------------- | ----------------- |
| `DbContext`             | `JpaRepository`, `EntityManager` | Giao tiếp DB      |
| `DbSet<T>`              | `JpaRepository<T, ID>`           | Đại diện bảng     |
| Model class (`Product`) | `@Entity class Product`          | Entity            |
| LINQ                    | JPQL / Criteria API              | Truy vấn          |
| Migration               | Flyway / Liquibase               | Schema versioning |

| C# EF Core          | Java Spring Boot                |
| ------------------- | ------------------------------- |
| `DbContext`         | `@Repository` + `JpaRepository` |
| `DbSet<Product>`    | `JpaRepository<Product, Long>`  |
| `Add(entity)`       | `save(entity)`                  |
| `Remove(entity)`    | `delete(entity)`                |
| `ToList()`          | `findAll()`                     |
| `Find(id)`          | `findById(id)`                  |
| `Where(...)` (LINQ) | `findBy...`, JPQL               |

- Kết nối cơ sở dữ liệu trong Entity Framework Core
| Bước | Mô tả                                                   |
| ---- | ------------------------------------------------------- |
| 1    | Cài gói EF Core phù hợp DB                              |
| 2    | Tạo `DbContext`                                         |
| 3    | Cấu hình chuỗi kết nối (`ConnectionString`)             |
| 4    | Đăng ký DbContext vào `DI container` trong `Program.cs` |
| 5    | Migrate (nếu dùng Code First)                           |

Bước 1: Cài đặt gói NuGet cho DB bạn dùng
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL

Bước 2: Tạo DbContext
public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }

    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }
}

Bước 3: Cấu hình chuỗi kết nối
Trong file appsettings.json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Database=ShopDb;Username=postgres;Password=123;"
  }
}

Bước 4: Cấu hình DbContext trong Program.cs
Bước 5: Dùng DbContext ở Controller/Service
public class ProductService
{
    private readonly AppDbContext _context;

    public ProductService(AppDbContext context)
    {
        _context = context;
    }

    public List<Product> GetAll()
    {
        return _context.Products.ToList();
    }
}
Bước 6: Migration và tạo DB (Code First)
dotnet ef migrations add InitialCreate
dotnet ef database update

- Lazy loading vs Eager loading vs Explicit loading
| Tiêu chí           | Lazy Loading    | Eager Loading | Explicit Loading             |
| ------------------ | --------------- | ------------- | ---------------------------- |
| Load khi nào?      | Khi truy cập    | Ngay lập tức  | Khi gọi `.Load()`            |
| Cách dùng          | Virtual + proxy | `Include()`   | `Entry().Reference().Load()` |
| Số lượng query     | N + 1           | 1 (JOIN)      | Tùy bạn                      |
| Dễ dùng            | Rất dễ          | Dễ            | Trung bình                   |
| Gây lỗi hiệu năng? | ✅ Có            | ❌             | ❌                            |
| Kiểm soát tốt nhất | ❌               | ❌             | ✅                            |

- Tracking vs NoTracking
| So sánh           | **Tracking** (mặc định) | **NoTracking**          |
| ----------------- | ----------------------- | ----------------------- |
| Theo dõi thay đổi | ✅ Có                    | ❌ Không                 |
| Dùng để cập nhật? | ✅ Có                    | ❌ Không                 |
| Dùng khi nào?     | Khi cần update sau đó   | Khi chỉ đọc (read-only) |
| Hiệu năng         | Trung bình              | ✅ Tốt hơn               |
| Memory usage      | Cao hơn                 | ✅ Nhẹ hơn               |

- Transactions trong EF
using var transaction = _context.Database.BeginTransaction();
try
{
    var order = new Order { ... };
    _context.Orders.Add(order);
    _context.SaveChanges();

    var log = new OrderLog { OrderId = order.Id, Status = "Created" };
    _context.OrderLogs.Add(log);
    _context.SaveChanges();

    transaction.Commit(); // ✅ Xác nhận
}
catch
{
    transaction.Rollback(); // ❌ Lỗi → hủy tất cả
}

- Stored Procedure trong EF
Phải gọi EXEC Raw sql như: FromSqlRaw, FromSqlInterpolated

- Truy vấn custom model (không có DbSet)
[Keyless]
public class ProductSummary
{
    public string CategoryName { get; set; }
    public int TotalProduct { get; set; }
}

public DbSet<ProductSummary> ProductSummaries { get; set; }

var result = _context.ProductSummaries
    .FromSqlRaw("SELECT c.Name AS CategoryName, COUNT(*) AS TotalProduct FROM Products p JOIN Categories c ON c.Id = p.CategoryId GROUP BY c.Name")
    .ToList();

- Pagination (Phân trang)
LINQ với Skip() và Take() Lưu ý Luôn cần OrderBy() để EF sinh câu SQL đúng

DbSet<T> trong EF thực chất là IQueryable<T>

- Fluent API
Fluent API = Cấu hình qua code trong dbcontext → chi tiết và linh hoạt hơn so với Data Annotation ([Key], [Required], …)
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Product>(entity =>
    {
        entity.HasKey(p => p.Id);                         // Primary key
        entity.Property(p => p.Name)
              .IsRequired()
              .HasMaxLength(100);
        entity.Property(p => p.Price)
              .HasColumnType("decimal(18,2)");
        entity.HasIndex(p => p.Name);                     // Index
    });
}

# 9. Caching 
| Loại              | Vị trí / Ví dụ                                                        | Đặc điểm                                                         |
| ----------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------- |
| In-Memory Cache   | `MemoryCache` (System.Runtime.Caching), `IMemoryCache` (ASP.NET Core) | Lưu trong RAM, nhanh, **chỉ trên 1 server**, mất khi app restart |
| Distributed Cache | Redis, Memcached                                                      | Dùng cho **multi-server**, dữ liệu tồn tại lâu hơn app restart   |
| Response Cache    | `[ResponseCache]` trong ASP.NET Core                                  | Cache kết quả HTTP response                                      |
| Output Cache      | ASP.NET MVC (cũ)                                                      | Cache toàn bộ output của view                                    |

Redis :
1. Key trong Redis
Key trong Redis luôn là string.
Key phải unique trong database Redis để nhận dữ liệu đúng.
Key thường được quy ước có dạng “namespace:entity:id” để dễ quản lý:

TopProducts         // danh sách top products
Product:123         // thông tin sản phẩm id=123
Cart:User:456       // giỏ hàng của user 456

2. Value trong Redis
| Kiểu                  | Mô tả                         | Ví dụ                                |
| --------------------- | ----------------------------- | ------------------------------------ |
| String                | Lưu chuỗi, đơn giản nhất      | JSON serialized object, HTML, number |
| List                  | Danh sách (FIFO)              | ["product1","product2"]              |
| Hash                  | Lưu dạng dictionary key-value | Product:{Name, Price, Stock}         |
| Set                   | Tập hợp không trùng lặp       | {"tag1","tag2"}                      |
| Sorted Set            | Set có thứ tự                 | leaderboard: userId -> score         |
| Bitmaps, HyperLogLog… | Chuyên dụng                   | tracking online users                |

MySQL nhỏ nhẹ , cấu hình đơn giản, phù hợp web blog đơn giản
PostgreSQL do meta phát triển ,db lớn, phù hợp xử lý transaction phức tạp, hệ thống ecommerce
SQL Server do microsoft phát triển, tích hợp sâu với .NET / C#, phù hợp hệ sinh thái của nó
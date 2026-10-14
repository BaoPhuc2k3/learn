object lifetime management – thường gặp trong Dependency Injection container như Spring, .NET, hoặc các hệ thống áp dụng Design Pattern.
Trong Design Pattern và DI frameworks, các lifetime (vòng đời) xác định:⏳ Object được tạo khi nào, tồn tại bao lâu, và có bị tái sử dụng không?
Bean Lifetime


🔶 1. Singleton
✅ Định nghĩa:
Chỉ có một instance duy nhất của class trong toàn bộ ứng dụng.
Dù bạn gọi bao nhiêu lần, cũng dùng lại cùng một object đã tạo ra từ trước.

📌 Ví dụ thực tế:
Trong Spring:
@Service // mặc định là singleton
public class AppConfigService {
    public String getAppName() {
        return "MyApp";
    }
}
➡ Từ lúc app khởi động đến lúc tắt, AppConfigService chỉ được tạo 1 lần, mọi nơi inject đều dùng chung instance.
Trong Java thuần (Design Pattern):
public class DatabaseConnection {

    private static DatabaseConnection instance;

    private DatabaseConnection() {}

    public static synchronized DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
}

➡ Đây là Singleton pattern – tự tay bạn quản lý vòng đời object.
✅ Khi nào dùng?
Class chứa cấu hình, cache, config system
Không có state thay đổi, có thể dùng lại

🔷 2. Scoped (Request, Session, Custom Scope)
✅ Định nghĩa:
Object được tạo mới theo từng phạm vi (scope): request, session, websocket, job, ...
Dùng phổ biến trong web application hoặc cloud app

Các loại scoped phổ biến trong Spring:
| Scope         | Tồn tại bao lâu                             |
| ------------- | ------------------------------------------- |
| `request`     | Trong 1 HTTP request duy nhất               |
| `session`     | Trong suốt session login của người dùng     |
| `application` | Toàn bộ vòng đời ứng dụng (giống singleton) |

📌 Ví dụ thực tế:
@Component
@Scope("request")
public class RequestTracker {
    private final String uuid = UUID.randomUUID().toString();
    public String getRequestId() {
        return uuid;
    }
}

➡ Mỗi HTTP request vào sẽ được tạo 1 RequestTracker mới.
Trong 1 request: dùng chung 1 instance.
Hết request: object bị loại bỏ.

🔸 3. Transient (Prototype trong Spring)
✅ Định nghĩa:
Mỗi lần yêu cầu sẽ tạo một object mới
Không giữ lại object nào, không reuse

Spring gọi là prototype scope
@Component
@Scope("prototype")
public class EmailBuilder {
    private String to;
    private String subject;
    private String content;
}

➡ Mỗi lần gọi new EmailBuilder() qua DI, Spring tạo một instance hoàn toàn mới.

📊 So sánh 3 loại vòng đời:
| Tên           | Tạo bao nhiêu lần?    | Phạm vi sử dụng lại      |
| ------------- | --------------------- | ------------------------ |
| **Singleton** | 1 lần duy nhất        | Mọi nơi dùng chung       |
| **Scoped**    | 1 lần trong mỗi scope | Trong request/session đó |
| **Transient** | Mỗi lần tạo là mới    | Không reuse              |

💬 Gợi ý trả lời phỏng vấn:

Em hiểu rằng mỗi object có vòng đời khác nhau. Với Singleton, em dùng cho các service không thay đổi trạng thái. Với Request scope, em dùng để log request hoặc lưu thông tin tạm thời. Với Transient (hoặc prototype), em dùng khi object có trạng thái riêng cho từng tác vụ, như EmailBuilder. Em chọn vòng đời phù hợp để tránh memory leak và đảm bảo hiệu năng.


----------------------------------------------------------------------------------------------------------------------------


I. Định nghĩa "Bean Lifetime" là gì?
Là khoảng thời gian một object (bean) tồn tại trong ứng dụng – từ khi được tạo ra cho đến khi bị hủy đi.
Trong Spring Boot, bạn có thể quy định vòng đời của bean thông qua annotation @Scope.

II. CÁC LOẠI BEAN LIFETIME (SCOPE) TRONG SPRING
| Tên Bean Scope  | Mô tả ngắn                                        | Thường dùng cho...                             |
| --------------- | ------------------------------------------------- | ---------------------------------------------- |
| **singleton**   | Mặc định. Tạo 1 instance duy nhất trong container | Các `Service`, `Component` không có trạng thái |
| **prototype**   | Tạo mới mỗi lần gọi `getBean()`                   | Bean có trạng thái riêng biệt từng lần         |
| **request**     | 1 instance duy nhất trong 1 HTTP request          | Lưu thông tin người dùng trong request         |
| **session**     | 1 instance duy nhất trong 1 session               | Lưu giỏ hàng, thông tin đăng nhập              |
| **application** | 1 instance cho toàn bộ ServletContext             | Dữ liệu cache toàn app                         |
| **websocket**   | 1 instance mỗi WebSocket session                  | Giao tiếp thời gian thực                       |

III. Ví dụ từng loại Bean Lifetime
1. Singleton (default) 
ConfigService  
Spring tạo ra ConfigService 1 lần duy nhất, toàn bộ app dùng lại.
Đây là giống Design Pattern Singleton.

2. Prototype (Transient)
@Component
@Scope("prototype")
public class EmailBuilder {
    private String to, subject, body;
}

Mỗi lần gọi context.getBean(EmailBuilder.class) → tạo object mới.
Dùng khi bạn cần object mang trạng thái riêng cho từng lần gửi email.

3. Request Scope
@Component
@Scope("request")
public class RequestTracker {
    private final String requestId = UUID.randomUUID().toString();
}

Trong 1 request: các class dùng chung RequestTracker.
Khác request: tạo mới.
Áp dụng để log, kiểm tra tracing,...

4. Session Scope
@Component
@Scope("session")
public class SessionData {
    private String userId;
}
Giữ thông tin người dùng sau đăng nhập (giỏ hàng, quyền,...)
Hết session → bị xóa.

5. Application Scope
@Component
@Scope("application")
public class GlobalStatistics {
    private AtomicInteger totalRequestCount = new AtomicInteger(0);
}
Dữ liệu tồn tại suốt đời ứng dụng (shared across requests).

IV. Khi nào nên dùng từng loại?
| Tình huống                            | Scope phù hợp |
| ------------------------------------- | ------------- |
| Service không giữ state               | `singleton`   |
| Object cần trạng thái riêng biệt      | `prototype`   |
| Tạm lưu dữ liệu theo request          | `request`     |
| Giỏ hàng, user info, lưu suốt session | `session`     |
| Thống kê hệ thống toàn app            | `application` |

VI. Câu hỏi phỏng vấn thường gặp
✅ Cơ bản:

❓ Bean default scope trong Spring là gì?
➤ Trả lời: singleton

❓ Sự khác nhau giữa singleton và prototype?
➤ Singleton: chỉ 1 object duy nhất
➤ Prototype: mỗi lần tạo là một object mới

❓ Khi nào nên dùng prototype?
➤ Khi object mang state riêng biệt: như builder, temp object,...

✅ Trung bình – Khó:

❓ Inject prototype vào singleton có tạo mới mỗi lần không?
➤ Không. Prototype chỉ tạo mới tại thời điểm inject → cần ObjectProvider

❓ Sự khác nhau giữa request và session scope?
➤ Request: tồn tại trong 1 HTTP request
➤ Session: tồn tại suốt phiên làm việc người dùng

❓ Spring có quản lý vòng đời của prototype bean không?
➤ Không hoàn toàn. Không gọi được @PreDestroy → bạn phải tự dọn tài nguyên nếu cần.

❓ Bean session được lưu ở đâu?
➤ Lưu trong HttpSession của servlet container (Tomcat, Jetty...)

✅ Gợi ý câu trả lời hay:

Em hiểu rằng việc chọn đúng bean scope ảnh hưởng trực tiếp đến hiệu năng, memory và logic xử lý. Trong các service không state em dùng singleton. Còn những bean cần state riêng biệt như builder pattern hoặc cache tạm thời, em dùng prototype. Với request, em dùng scope "request" để lưu dữ liệu theo từng lần request. Em cũng biết các cạm bẫy khi inject prototype vào singleton, và dùng ObjectProvider để khắc phục.

VÍ dụ trong web bán hàng:
ProductFactory có thể là prototype , còn lại Product hay ProductDTO đều là POJO(Plain Old Java Object)



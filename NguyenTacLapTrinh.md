Nguyên tắc SOLID 
| Nguyên tắc                                    | Ý nghĩa chính                                                                  |
| -----------------------------------           | ------------------------------------------------------------------------------ |
| **S - SRP** (Single Responsibility)           | Mỗi class chỉ nên **làm một nhiệm vụ duy nhất**                                |
| **O - OCP** (Open/Closed Principle)           | Mở rộng được mà **không cần sửa code cũ**                                      |
| **L - LSP** (Liskov Substitution)             | Subclass có thể **thay thế** cho superclass mà không thay đổi hành vi          |
| **I - ISP** (Interface Segregation)           | Interface nên **nhỏ, rõ**, không nên "tổng hợp đủ thứ"                         |
| **D - DIP** (Dependency Inversion Principle)  | Class nên phụ thuộc vào **abstraction (interface)**, không phải implementation |

DIP: High-level module (business logic) không nên phụ thuộc vào low-level module (chi tiết).
Cả 2 nên phụ thuộc vào abstraction (interface).
| Không theo DIP                             | Theo DIP                                         |
| ------------------------------------------ | ------------------------------------------------ |
| `Controller` → `EmailServiceImpl` (cụ thể) | `Controller` → `NotificationService` (interface) |
| Phụ thuộc vào implementation cụ thể        | Phụ thuộc vào abstraction                        |
| Khó mock, test, thay thế logic             | Dễ thay thế, dễ mock khi test                    |

High-level module Nó định nghĩa hành vi tổng thể của hệ thống phải độc lập và dễ tái sử dụng.
Low-level module Là mô-đun cấp thấp, xử lý chi tiết kỹ thuật có thể thay đổi thường xuyên, không nên "trói buộc" với logic cấp cao

| Mô-đun         | Vai trò                                | Ví dụ                                                        |
| -------------- | -------------------------------------- | ------------------------------------------------------------ |
| **High-level** | Business logic, điều phối nghiệp vụ    | `OrderService`, `UserService`, `CheckoutController`          |
| **Low-level**  | Chi tiết kỹ thuật, phụ thuộc bên ngoài | `EmailSender`, `SmsClient`, `JdbcRepository`, `RestTemplate` |


Tính chất của lập trình hướng đối tượng (OOP)
| Tính chất         | Ý nghĩa                                                                |
| ----------------- | ---------------------------------------------------------------------- |
| **Encapsulation** | Đóng gói dữ liệu và hành vi → ẩn thông tin nội bộ (`private`)          |
| **Abstraction**   | Ẩn chi tiết thực thi, chỉ cung cấp giao diện (`interface`, `abstract`) |
| **Inheritance**   | Kế thừa thuộc tính và hành vi của class cha                            |
| **Polymorphism**  | Đa hình: 1 hành vi nhưng thực thi khác nhau (override, overload)       |

Tính chất dữ liệu ACID trong Transaction (Data Integrity – rất hay gặp khi làm việc với DB)
| Tính chất       | Ý nghĩa                                 |
| --------------- | --------------------------------------- |
| **Atomicity**   | Tất cả hoặc không gì cả                 |
| **Consistency** | Luôn đưa DB về trạng thái hợp lệ        |
| **Isolation**   | Không bị ảnh hưởng bởi transaction khác |
| **Durability**  | Khi commit thì lưu vĩnh viễn            |

Consistency có nghĩa là sau khi transaction kết thúc, dữ liệu vẫn tuân theo các ràng buộc (constraint) của database.
Nếu DB đang ở trạng thái hợp lệ S, và thực hiện transaction T, thì sau khi T kết thúc (commit) DB vẫn ở trạng thái hợp lệ S’.

Tính chất Isolate
| Level                                      | Dirty Read | Non-Repeatable Read | Phantom Read | Ý nghĩa                      |
| ------------------------------------------ | ---------- | ------------------- | ------------ | ---------------------------- |
| **Read Uncommitted**                       | ✅ Có       | ✅ Có                | ✅ Có         | Đọc được dữ liệu chưa commit |
| **Read Committed** *(mặc định SQL Server)* | ❌ Không    | ✅ Có                | ✅ Có         | Chỉ đọc dữ liệu đã commit    |
| **Repeatable Read**                        | ❌ Không    | ❌ Không             | ✅ Có         | Không bị sửa/đọc lại         |
| **Serializable**                           | ❌ Không    | ❌ Không             | ❌ Không      | Cách ly tối đa (chậm nhất)   |


Nguyên tắc Clean Code & Best Practices
| Nguyên tắc           | Ý nghĩa                                                  |
| -------------------- | -------------------------------------------------------- |
| **KISS**             | Keep It Simple, Stupid – giữ code đơn giản dễ hiểu       |
| **DRY**              | Don’t Repeat Yourself – tránh trùng lặp logic            |
| **YAGNI**            | You Aren’t Gonna Need It – không viết thứ chưa cần thiết |
| **Code Convention**  | Tuân thủ quy ước đặt tên, format code nhất quán          |
| **Comment đúng chỗ** | Chỉ comment nơi khó hiểu, tránh comment dư thừa          |

Ví dụ về nguyên tắc solid:
- S Single: Mỗi class chỉ nên chịu trách nhiệm về một nhiệm vụ duy nhất.
VD: Class UserService vừa lưu user vào db vừa gửi email, như vậy là sai, nên tách gửi email ra vào EmailService 
- O Open/Close: Open code mới, Close code cũ
VD: Viết email impl noti chứ không viết luôn email, sau này thêm service noti khác vd như sms thì impl tiếp không sửa code cũ
- L Liskov: Class con thay class cha mà không thay đổi hành vi
VD: impl freeOrder ở interface Thanh toán, miễn phí thì ko cần trả tiền, mà nên impl Cách thanh toán
- I Interface: Interface nên nhỏ, rõ, không chứa phương thức thừa
VD: noti interface không nên có sendEmail, sendSMS mà chỉ cần send thôi là được, vì có thể tk impl không cần dùng đến
- D Dependency: Class nên phụ thuộc vào abstraction(interface), chứ không nên phụ thuộc vào impl cụ thể
VD: impl noti thôi, không nên impl smsNoti

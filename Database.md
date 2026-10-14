1. View
- View :Là bảng ảo Không lưu dữ liệu – chỉ là câu lệnh SELECT được đặt tên
| Tiêu chí                  | **Table (Bảng thật)**           | **View (Bảng ảo)**                                         |
| ------------------------- | ------------------------------- | ---------------------------------------------------------- |
| **Lưu trữ dữ liệu**       | Có lưu dữ liệu vật lý trong DB  | Không lưu dữ liệu – chỉ là câu lệnh SELECT được đặt tên    |
| **Tạo bằng**              | `CREATE TABLE`                  | `CREATE VIEW`                                              |
| **Hiệu suất**             | Truy vấn nhanh hơn nếu có index | Chậm hơn (vì phải thực thi lại SELECT gốc mỗi lần)         |
| **Có index không?**       | Có thể tạo chỉ mục (index)      | Không thể tạo index trực tiếp trên View                    |
| **Có thể insert/update?** | Có                              | Có điều kiện (chỉ với *simple view*)                       |
| **Bảo mật**               | Không hỗ trợ che giấu dữ liệu   | Có thể ẩn cột nhạy cảm qua View                            |
| **Tái sử dụng truy vấn**  | Không                           | Dùng lại được nhiều lần                                    |
| **Phụ thuộc bảng khác?**  | Không                           | Có (phụ thuộc bảng thật để lấy dữ liệu)                    |
| **Cập nhật được không?**  | Có                              | Có thể (nếu là updatable view, không có GROUP BY, JOIN...) |

Khi nào nên dùng View?
| Trường hợp                          | Mô tả                                                                                    |
| ----------------------------------- | ---------------------------------------------------------------------------------------- |
| ✅ **Tái sử dụng truy vấn phức tạp** | Thay vì lặp lại nhiều `JOIN`, `WHERE`, bạn tạo 1 View cho truy vấn phức tạp và dùng lại. |
| ✅ **Ẩn thông tin nhạy cảm**         | Ví dụ: Chỉ show cột `username`, `email`, nhưng không show `password` từ bảng `users`.    |
| ✅ **Tách quyền truy cập**           | Cấp quyền SELECT lên View thay vì bảng gốc.                                              |
| ✅ **Chuẩn hóa tên cột, dữ liệu**    | View giúp thay đổi tên cột, chuẩn hóa dữ liệu đầu ra.                                    |
| ✅ **Giúp frontend dễ query**        | View giúp API hoặc frontend không cần hiểu cấu trúc DB phức tạp.                         |

Khi nào không nên dùng View?
| Trường hợp                              | Lý do                                                                                                       |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| ❌ **Hiệu năng quan trọng**              | Vì View luôn thực thi lại SELECT → chậm hơn bảng thật (đặc biệt nếu truy vấn phức tạp, không index được).   |
| ❌ **Cần thao tác ghi (write)** nhiều    | Không phải View nào cũng `INSERT/UPDATE/DELETE` được.                                                       |
| ❌ **Logic quá phức tạp bên trong View** | Nếu View dùng JOIN, GROUP BY, ORDER BY... sẽ khó maintain hoặc không thể update.                            |
| ❌ **Thay thế bảng thật**                | View không nên dùng như 1 bảng thay thế – chỉ là bảng tạm thời để truy xuất.                                |
| ❌ **Dữ liệu thay đổi quá nhanh**        | Vì View không lưu dữ liệu, mỗi lần truy vấn là mỗi lần thực thi lại SQL → không tối ưu cho real-time nhanh. |

View là bảng ảo được tạo từ câu truy vấn SELECT. Em dùng View để đơn giản hóa truy vấn, che giấu dữ liệu nhạy cảm và hỗ trợ tái sử dụng logic truy vấn nhiều lần. Tuy nhiên, em tránh dùng View khi cần hiệu suất cao hoặc cần ghi dữ liệu thường xuyên.

| Nên dùng View khi...           | Không nên dùng View khi...             |
| ------------------------------ | -------------------------------------- |
| Cần tái sử dụng truy vấn       | Cần hiệu suất cao                      |
| Cần ẩn thông tin nhạy cảm      | Cần ghi dữ liệu thường xuyên           |
| Phân quyền truy cập an toàn    | View quá phức tạp gây khó bảo trì      |
| Muốn đơn giản hóa API/frontend | Dữ liệu thay đổi nhanh và cần realtime |

CREATE VIEW customer_orders AS
SELECT 
    c.id AS customer_id,
    c.name AS customer_name,
    o.id AS order_id,
    o.order_date,
    o.amount
FROM 
    customers c
JOIN 
    orders o ON c.id = o.customer_id;



2. EntityManager Quản lý entity, CRUD, lifecycle

Các phương thức quan trọng của EntityManager
| Phương thức           | Mô tả                                          |
| --------------------- | ---------------------------------------------- |
| `persist(entity)`     | Thêm mới entity vào DB                         |
| `find(Class, id)`     | Tìm entity theo ID                             |
| `merge(entity)`       | Cập nhật entity                                |
| `remove(entity)`      | Xóa entity                                     |
| `createQuery()`       | Tạo JPQL query                                 |
| `createNativeQuery()` | Tạo query SQL thuần                            |
| `flush()`             | Đẩy dữ liệu trong persistence context xuống DB |
| `clear()`             | Xoá tất cả entity khỏi context                 |
| `detach(entity)`      | Gỡ entity ra khỏi context                      |
| `contains(entity)`    | Kiểm tra entity có đang được quản lý không     |

Vòng đời của một Entity (Entity Lifecycle)
| Trạng thái   | Mô tả                                  | Gọi qua            |
| ------------ | -------------------------------------- | ------------------ |
| **New**      | Vừa khởi tạo bằng `new`                | `new User()`       |
| **Managed**  | Được quản lý trong Persistence Context | `em.persist(user)` |
| **Detached** | Từng được quản lý nhưng bị tách ra     | `em.detach(user)`  |
| **Removed**  | Đánh dấu xoá                           | `em.remove(user)`  |

So sánh persist() vs merge()
| So sánh                | `persist()` | `merge()`            |
| ---------------------- | ----------- | -------------------- |
| Mục đích               | Thêm mới    | Cập nhật             |
| Yêu cầu entity phải... | New         | Có thể là detached   |
| Trả về                 | `void`      | Entity đã được merge |
| Nên dùng khi           | Insert      | Update               |


- Transaction

READ UNCOMMITTED : Cho phép đọc dữ liệu chưa được commit. Có thể xảy ra "Dirty Read".
READ COMMITTED : Chỉ cho phép đọc dữ liệu đã được commit. Có thể xảy ra "Non-Repeatable Read".
REPEATABLE READ : Đảm bảo rằng dữ liệu không thay đổi trong suốt transaction (mặc định).
SERIALIZABLE : Ngăn chặn hoàn toàn các transaction đồng thời, cho nó đi tuần tự hết.


| Hiện tượng              | Mô tả                                                                  |
| ----------------------- | ---------------------------------------------------------------------- |
| **Dirty Read**          | Đọc dữ liệu chưa commit từ transaction khác                            |
| **Non-repeatable Read** | Cùng 1 SELECT nhưng giá trị thay đổi trong cùng transaction            |
| **Phantom Read**        | Kết quả SELECT thay đổi vì có bản ghi mới (INSERT) từ transaction khác |

| Hiện tượng              | Read Uncommitted | Read Committed | Repeatable Read | Serializable |
| ----------------------- | ---------------- | -------------- | --------------- | ------------ |
| **Dirty Read**          | ✅ Có             | ❌ Không        | ❌ Không         | ❌ Không      |
| **Non-repeatable Read** | ✅ Có             | ✅ Có           | ❌ Không         | ❌ Không      |
| **Phantom Read**        | ✅ Có             | ✅ Có           | ✅ Có            | ❌ Không      |
| **Hiệu suất**           | 🔥 Cao           | Cao            | Trung bình      | ❄️ Thấp      |


Isolation càng cao thì càng an toàn, nhưng hiệu suất giảm.
Read Committed thường được dùng mặc định trong đa số ứng dụng.
Chỉ dùng Serializable nếu thật sự cần tính toàn vẹn cao nhất.


- Nháp: dirty read, non-reapeat able, phantom
Read uncommit : Đọc chưa commit
dirty read Ví dụ có 2 trans a và b , ban đầu giá trị là 1000 , a update thành 500 chưa commit, b nhảy vào lấy ra 500, a rollback thì nó lại thành 1000, lấy ra sai so với kết quả.


read commit: đọc đã commit
reapeatable giá trị ban đầu 1000, có 2 trans a và b , a lấy ra là 1000 b nhảy vào đổi thành 500 commit, a lại lấy ra thành 500 , 2 cái lần lấy ra trong 1 trans là khác nhau .


read reapeatable: giải quyết thêm vấn đề reapeatable bằng khoá cả trans
phantom read có 2 trans a và b, a lấy ra tuổi > 18 dc 5, b thêm vào 1 thằng > 18 tuổi commit ở giữa, a lấy ra lại > 18 tuổi thì thành dc 6, dữ liệu lại khác nhau trong 1 trans

serializealbe: giải quyết vấn đề phantom read bằng lock cả range


- So sánh Ienum và Iquery
| Đặc điểm      | `IEnumerable` | `IQueryable`               |
| ------------- | ------------- | -------------------------- |
| Nguồn dữ liệu | In-memory     | Out-of-memory (DB)         |
| Xử lý ở đâu   | RAM           | Database                   |
| Thực thi      | Ngay khi gọi  | Khi `.ToList()` hoặc duyệt |
| Dịch sang SQL |  Không        | Có                         |
| Dùng khi      | Dữ liệu nhỏ   | Dữ liệu lớn, query DB      |
                       
Có thể cố tình chuyển đổi qua lại lẫn nhau                       
IQueryable kế thừa IEnumerable
Khi bạn muốn chuyển từ xử lý ở DB sang xử lý ở bộ nhớ dùng AsEnumerable()
var query = db.Users
    .Where(u => u.IsActive)
    .AsEnumerable() // từ đây trở đi xử lý trong RAM
    .Where(u => CustomCheck(u)); // CustomCheck không thể dịch sang SQL


DTO – Data Transfer Object: là đối tượng truyền dữ liệu LoginRequestDTO, LoginResponseDTO 
MODEL – Mô hình nghiệp vụ (Business layer): Có thể bao gồm dữ liệu + phương thức xử lý logic, tầng service/controller nội bộ.
ENTITY – Thực thể dữ liệu (Database layer): Entity đại diện cho bảng trong database.
Mapper / Converter: Chuyển đổi giữa DTO ↔ Entity ↔ Model


| So sánh                    | Stored Procedure     | Function                 |
| -------------------------- | -------------------- | ------------------------ |
| Return                     | Có thể nhiều kết quả | Phải return 1 giá trị    |
| Trong SELECT               | ❌ Không              | ✅ Có                     |
| DML (INSERT/UPDATE/DELETE) | ✅ Có thể             | ❌ Không khuyến khích     |
| Transaction                | ✅ Có thể             | ❌ Không                  |
| Dùng trong JOIN/WHERE      | ❌ Không              | ✅ Có                     |
| Thích hợp cho              | Logic nghiệp vụ      | Tính toán / truy vấn nhỏ |

# 🔤 String vs StringBuilder vs StringBuffer trong Java

I. String – Immutable Chuỗi
✅ Tính chất:
Là một class immutable: mỗi khi thay đổi chuỗi, Java tạo object mới.
Lưu trữ trong String pool nếu tạo bằng "...".
VD:
String s = "hello";
s = s + " world"; // tạo object mới, không thay đổi "hello"

II. StringBuilder – Mutable, Không đồng bộ
✅ Tính chất:
Không đồng bộ (non-synchronized) → không thread-safe
Có thể thay đổi nội dung mà không tạo object mới
Nhanh hơn String khi thao tác nhiều với chuỗi
VD:
StringBuilder sb = new StringBuilder("hello");
sb.append(" world"); // không tạo object mới

✅ Khi nào dùng StringBuilder?
Thao tác chuỗi lặp lại, nhiều lần (append, insert…)
Trong single-thread (không dùng chung giữa các thread)

III. StringBuffer – Mutable, Đồng bộ
✅ Tính chất:
Giống StringBuilder nhưng được đồng bộ hóa (synchronized)
Thread-safe, nhưng chậm hơn vì tốn tài nguyên lock
VD:
StringBuffer sb = new StringBuffer("hello");
sb.append(" world"); // thread-safe

Khi nào dùng StringBuffer?
Trong môi trường đa luồng (multi-threaded)
Khi cần thread-safe trong xử lý chuỗi

IV. So sánh tổng quan
| Tiêu chí     | String                         | StringBuilder            | StringBuffer        |
| ------------ | ------------------------------ | ------------------------ | ------------------- |
| Mutable      | ❌ Immutable                    | ✔️ Có thể thay đổi       | ✔️ Có thể thay đổi  |
| Synchronized | ❌ Không                        | ❌ Không                  | ✔️ Có               |
| Thread-safe  | ❌ Không                        | ❌ Không                  | ✔️ Có               |
| Hiệu năng    | ❌ Chậm khi thay đổi            | ✅ Nhanh nhất             | ⚠️ Trung bình       |
| Khi dùng     | Văn bản tĩnh                   | Nối chuỗi nhanh, 1 luồng | Nối chuỗi, đa luồng |
| Lưu trữ      | String Pool (nếu dùng `"..."`) | Heap                     | Heap                |

VI. Câu hỏi phỏng vấn thường gặp
❓1. Sự khác nhau giữa String, StringBuilder, StringBuffer là gì?
String là immutable
StringBuilder và StringBuffer là mutable
StringBuffer synchronized, thread-safe → chậm hơn

❓2. Khi nào nên dùng StringBuilder thay vì String?
Khi bạn thao tác nhiều lần trên chuỗi (append, insert, delete,...)
Ví dụ: tạo JSON động, ghép file log, xử lý chuỗi trong vòng lặp

❓3. StringBuilder có thread-safe không?
❌ Không
Nếu cần thread-safe → dùng StringBuffer

❓4. So sánh hiệu năng giữa String và StringBuilder?
String tạo object mới mỗi lần nối → chậm
StringBuilder dùng buffer, chỉ thay đổi trong bộ nhớ → rất nhanh

❓5. String Pool là gì? Nó liên quan gì đến String?
String pool là nơi lưu trữ các literal "abc" để tái sử dụng
Giúp tiết kiệm bộ nhớ
Chỉ áp dụng với String tạo bằng dấu "...", không áp dụng với new String(...)

❓6. Làm sao để nối chuỗi hiệu quả nhất?
Nếu thao tác nhiều → StringBuilder
Nếu đa luồng → StringBuffer
Nếu chuỗi cố định → String

❓7. String Pool là gì?
Vùng nhớ đặc biệt lưu literal "abc" để tiết kiệm bộ nhớ.
Chỉ áp dụng với "...", không với new String(...).

| Dùng gì?        | Khi nào?                       |
| --------------- | ------------------------------ |
| `String`        | Chuỗi tĩnh, không thay đổi     |
| `StringBuilder` | Nối chuỗi nhiều, single-thread |
| `StringBuffer`  | Nối chuỗi nhiều, multi-thread  |


Gợi ý khi đi phỏng vấn:
Nếu bị hỏi "Em hãy viết 1 đoạn code nối chuỗi 10,000 lần", đừng dùng +, hãy dùng StringBuilder
Khi được hỏi về "thread-safe trong xử lý chuỗi", hãy đề cập StringBuffer
Nếu hỏi về "vì sao String immutable", hãy nói: Để đảm bảo an toàn khi dùng làm key trong Map, để dùng trong String pool, và để tránh bug do shared reference
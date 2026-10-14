

Tôi cần tìm hiểu các kiến thức gì về luồng của java để thành thạo

- [1. OOP(Object-Oriented Programming) , hướng đối tượng](#1-oopobject-oriented-programming--hướng-đối-tượng)
  - [1.1 Encapsulation : Đóng gói \[private , public\]](#11-encapsulation--đóng-gói-private--public)
  - [1.2 Abstraction : Trừu tượng(Giấu logic) \[interface , abstract class\]](#12-abstraction--trừu-tượnggiấu-logic-interface--abstract-class)
  - [1.3 Inheritance : Kế thừa \[ extends, supper, base \]](#13-inheritance--kế-thừa--extends-supper-base-)
  - [1.4 Polymorphism : Đa hình(1 phương thức, trả về kq khác nhau) \[overloading , overriding\]](#14-polymorphism--đa-hình1-phương-thức-trả-về-kq-khác-nhau-overloading--overriding)
  - [1.5 Composition : Tái sử dụng](#15-composition--tái-sử-dụng)
- [2. Design Patterns](#2-design-patterns)
  - [2.1 Creational : Quy định cách tạo đối tượng object](#21-creational--quy-định-cách-tạo-đối-tượng-object)
  - [2.2 Structural : Cấu trúc , lắp ghép các obj khác nhau](#22-structural--cấu-trúc--lắp-ghép-các-obj-khác-nhau)
  - [2.3 Behavioral : Hành vi , cách thức 1 obj phản hồi 1 obj khác](#23-behavioral--hành-vi--cách-thức-1-obj-phản-hồi-1-obj-khác)
- [3. Spring](#3-spring)
  - [3.1 Vòng đời bean (Scope) :](#31-vòng-đời-bean-scope-)
  - [3.2 Inversion of Control(IOC), Dependency Injection(DI)](#32-inversion-of-controlioc-dependency-injectiondi)
- [4. Database](#4-database)
  - [4.1 Các lệnh , từ khoá cơ bản :](#41-các-lệnh--từ-khoá-cơ-bản-)
  - [4.2.1 UNION kết hợp nhiều câu lệnh select](#421-union-kết-hợp-nhiều-câu-lệnh-select)
  - [4.2 JOINS kết hợp nhiều bảng](#42-joins-kết-hợp-nhiều-bảng)
  - [4.3 Quan hệ (Relationship)](#43-quan-hệ-relationship)
  - [4.4 Chuẩn hoá (Normalization And Denormalization)](#44-chuẩn-hoá-normalization-and-denormalization)
  - [4.5 Transaction](#45-transaction)
  - [4.6 Stored Procedures, Function, Trigger](#46-stored-procedures-function-trigger)
  - [4.7 Tối ưu truy vấn với Partitioning, Indexing, Materialized Views](#47-tối-ưu-truy-vấn-với-partitioning-indexing-materialized-views)
  - [4.8 Note](#48-note)
  - [4.9 Redis](#49-redis)
- [5. Cloud](#5-cloud)
  - [5.1 Infrastructure as a Service (IaaS) : Lưu trữ, mạng, hệ điều hành](#51-infrastructure-as-a-service-iaas--lưu-trữ-mạng-hệ-điều-hành)
  - [5.2 Platform as a Service (PaaS) : runtime](#52-platform-as-a-service-paas--runtime)
  - [5.3 Software as a Service (SaaS) : gmail, team, google driver](#53-software-as-a-service-saas--gmail-team-google-driver)
  - [5.4 So sánh IaaS, PaaS, SaaS](#54-so-sánh-iaas-paas-saas)
  - [5.5 So sánh Các Nhà Cung Cấp Dịch Vụ Cloud Nổi Tiếng](#55-so-sánh-các-nhà-cung-cấp-dịch-vụ-cloud-nổi-tiếng)
- [6. Java core](#6-java-core)
  - [6.1 Thread, Mutil Thread, lập trình đa nhiệm (multitasking), xử lý đồng thời (concurrency)](#61-thread-mutil-thread-lập-trình-đa-nhiệm-multitasking-xử-lý-đồng-thời-concurrency)
  - [6.2 Các loại cấu trúc dữ liệu trong Java](#62-các-loại-cấu-trúc-dữ-liệu-trong-java)
  - [6.3 So sánh để hiểu rõ:](#63-so-sánh-để-hiểu-rõ)
- [7. Algorithm](#7-algorithm)
- [8. JS TS](#8-js-ts)
- [9. Mạng máy tính (Networking)](#9-mạng-máy-tính-networking)
  - [9.1 Mô hình mạng](#91-mô-hình-mạng)
  - [9.2 Hệ thống file](#92-hệ-thống-file)
  - [9.3 Websocket](#93-websocket)
- [10. Microservice](#10-microservice)
- [11. JWT (JSON Web Token)](#11-jwt-json-web-token)
- [12. Câu hỏi phỏng vấn](#12-câu-hỏi-phỏng-vấn)


# 1. OOP(Object-Oriented Programming) , hướng đối tượng 
## 1.1 Encapsulation : Đóng gói [private , public]
+ Gói gọn thuộc tính , hành vi vào trong 1 lớp , như hộp đen chỉ có thể truy cập được 1 số thuộc tính và phương thức cho phép mà thôi
+ Đảm bảo tính bảo mật, bảo trì, mở rộng, thuộc tính là private , hàm là public
public class User {
    private String username;
    private String password;
    // Được đổi username
    // Không cho get Password mà chỉ có hàm changePassword chuyên dụng
}


## 1.2 Abstraction : Trừu tượng(Giấu logic) [interface , abstract class]
+ Ẩn đi chi tiết triển khai bên trong, hiển thị những gì cần thiết ra bên ngoài .
+ Ẩn đi logic cụ thể, chỉ cung cấp interface mô tả hành vi.
+ Thể hiện qua Abstract Class (extends), Interface (implement), đều cần @Override
VD:
public interface NotificationService {
    void send(String to, String content);
}
public class EmailService implements NotificationService {
    public void send(String to, String content) {
        // Gửi email
    }
}

Abstract Class: Là 1 class nhưng không thể khởi tạo trực tiếp
    Đại diện cho một lớp cha chung với các thuộc tính và hành vi cơ bản, có mối quan hệ "is-a".
    Là một lớp không thể được khởi tạo trực tiếp (không thể tạo đối tượng từ nó giống interface).
    Chỉ kế thừa được 1
Interface:
    Định nghĩa hành vi mà các lớp triển khai phải tuân theo, có mối quan hệ "can-do"
    Có thể implement được nhiều Interface khác nhau
    Tất cả thuộc tính , phương thức đều là public
Phương thức trừu tượng :
    Là một phương thức được khai báo nhưng không có phần triển khai
    Chỉ có thể tồn tại trong một abstract class hoặc một interface .
    Bắt buộc lớp con phải ghi đè
    Trong abstract class , phương thức trừu tượng được khai báo bằng từ khóa abstract.
    Trong interface , tất cả các phương thức mặc định đều là trừu tượng (trừ khi chúng là default/static methods).

Tất cả các method trong interface (trừ khi đã default hoặc static) đều là abstract, nên bắt buộc phải override khi implement.

Class con chỉ phải override những method được đánh dấu là abstract.
Các method đã có body thì có thể dùng lại luôn, không cần override.

## 1.3 Inheritance : Kế thừa [ extends, supper, base ]
+ Mang theo thuộc tính phương thức của lớp cha, mối quan hệ is-a (Là một)
+ Từ khoá extends ,supper, base
BaseEntity có sẵn Id, createdAt, updatedAt

## 1.4 Polymorphism : Đa hình(1 phương thức, trả về kq khác nhau) [overloading , overriding]
+ Thể hiện hành vi khác nhau khi gọi chung 1 phương thức
+ Thể hiện qua overloading (Compile-time)(Có thể khác nhau kiểu trả về , tham số đầu vào)  và overriding (Ghi đè) (Runtime)
overloading (Nạp chồng) :
    Xảy ra tại compile-time (thời điểm biên dịch).
    Tên phương thức phải giống nhau , Kiểu trả về phải giống nhau , Tham số Phải khác nhau , khác logic

Overriding (Ghi đè) class con viết lại method cha :
    Xảy ra tại runtime (thời điểm chạy chương trình).
    Tên phương thức phải giống nhau , Kiểu trả về có thể khác , Tham số Phải khác nhau
    
VD: Gửi thông báo bằng nhiều phương thức khác nhau
public interface NotificationService {
    void send(String to, String message);
}

@Service
public class EmailNotificationService implements NotificationService {
    public void send(String to, String message) {
        // Gửi email
    }
}

@Service
public class SmsNotificationService implements NotificationService {
    public void send(String to, String message) {
        // Gửi SMS
    }
}


| Tính chất     | Mục tiêu                          | Cách dùng trong Java                         |
| ------------- | --------------------------------- | -------------------------------------------- |
| Encapsulation | Giấu dữ liệu, bảo vệ class        | `private`, `getter/setter`, method kiểm soát |
| Inheritance   | Tái sử dụng code, tổ chức cha-con | `extends`, `super`                           |
| Polymorphism  | Hành vi đa dạng                   | Overriding, Overloading                      |
| Abstraction   | Giảm phụ thuộc, làm code gọn gàng | `interface`, `abstract class`, DI            |

## 1.5 Composition : Tái sử dụng
Composition là việc tạo một đối tượng bằng cách kết hợp nhiều đối tượng nhỏ hơn – gọi là các “thành phần” – thay vì kế thừa từ một class cha. Thay vì "is-a" (là một) như kế thừa, composition là "has-a" (có một).
+ Một lớp chứa tham chiếu đến một đối tượng của lớp khác.
+ Quan hệ "has-a" (có một)
VD: Composition trong Service dùng Repository
→ UserService có một UserRepository → Đây chính là Composition.hoặc một Controller có thể gọi nhiều service khác nhau.
@Service
public class UserService {

    private final UserRepository userRepository;

    // Inject thông qua constructor: Composition
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User findByUsername(String username) {
        return userRepository.findByUsername(username);
    }
}


# 2. Design Patterns  
Là các giải pháp đã được kiểm chứng và tái sử dụng để giải quyết các vấn đề phổ biến trong thiết kế phần mềm.  
có 3 loại : Creational, Structural, Behavioral
## 2.1 Creational : Quy định cách tạo đối tượng object
+ singleton : Đảm bảo 1 lớp chỉ có 1 instance (  logging system, kết nối cơ sở dữ liệu , Chỉ có 1 file cấu hình,...)
```java
    public class Singleton {
        private static Singleton instance;
        private Singleton() {} // Private constructor

        public static Singleton getInstance() {
            if (instance == null) {
                instance = new Singleton();
            }
            return instance;
        }
    }

+ factory : định nghĩa một giao diện để tạo đối tượng, nhưng để các lớp con quyết định kiểu đối tượng cần tạo.
+ prototype : cho phép sao chép một đối tượng hiện có thay vì tạo mới từ đầu. (viết hàm clone return new đối tượng)
+ DI : dependency injection
+ object pool là một mẫu thiết kế giúp tái sử dụng các đối tượng thay vì tạo mới mỗi khi cần.
+ builder : xây dựng đối tượng từng bước, tạo đối tượng khác nhau theo cùng 1 quá trình, không phải tạo nhiều hàm khởi tạo

public class Computer {

    private String CPU;b
    private String RAM;

    // Constructor riêng tư để ngăn việc khởi tạo trực tiếp
    private Computer(Builder builder) {
        this.CPU = builder.CPU;
        this.RAM = builder.RAM;
    }

    public void showInfo() {
        System.out.println("CPU: " + CPU);
        System.out.println("RAM: " + RAM);
    }

    // Lớp Builder lồng bên trong
    public static class Builder {
        private String CPU;
        private String RAM;

        // Constructor cho các thuộc tính bắt buộc
        public Builder(String CPU) {
            this.CPU = CPU;
        }

        // Các phương thức setter để thiết lập các thuộc tính tùy chọn
        public Builder setRam(String ram) {
            // logic nghiệp vụ
            this.graphicsCard = graphicsCard;
            return this;
        }

        // Phương thức build để trả về đối tượng Computer
        public Computer build() {
            return new Computer(this);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng Computer bằng Builder
        Computer computer = new Computer.Builder("Intel i7" )
                .setRam("16GB")
                .build();

        // Hiển thị thông tin máy tính
        computer.showInfo();
    }
}
```

## 2.2 Structural : Cấu trúc , lắp ghép các obj khác nhau
+ decorator : bọc obj trong 1 class mới để bổ sung, thay đổi tính năng mà không thay đổi code cũ
abstract class implement interface

+ facade : Cung cấp một giao diện đơn giản để che giấu sự phức tạp của hệ thống bên dưới.
+ proxy : một đối tượng đại diện (proxy ) được sử dụng để kiểm soát quyền truy cập vào một đối tượng thực tế (real subject ).
    Virtual Proxy : Trì hoãn việc tạo đối tượng thực tế cho đến khi nó thực sự cần thiết.
    Remote Proxy : Đại diện cho một đối tượng nằm trên một máy chủ khác (remote object).
    Protection Proxy : Kiểm soát quyền truy cập vào đối tượng thực tế dựa trên vai trò hoặc quyền hạn của người dùng.

+ adapter : chuyển đổi giao diện để tăng khả năng tương thích
changerUSBC

## 2.3 Behavioral : Hành vi , cách thức 1 obj phản hồi 1 obj khác
Behavioral Patterns được chia thành hai loại chính: Class Patterns (Template Method) , Object Patterns (Observer, Strategy.)
+ observer : Cho phép đối tượng theo dõi, phản hồi với những thay đổi từ đối tượng khác
vd : gắn obj class A vào 1 danh sách, khi 1 obj class B thay đổi, xử lý(có thể là thay đổi thuộc tính gì đó) 
với từng đối tượng của mảng class A . VD: Hệ thống publish-subscribe.
+ Iterator : Cung cấp một cách để truy cập tuần tự các phần tử của một collection mà không làm lộ cấu trúc bên trong.
+ strategy : Cho phép chọn hành vi khác nhau tại runtime mà không thay đổi mã nguồn đối tượng gọi (Override, tính đa hình)
vd : tạo 1 interface payMent có hàm pay() , có các class con implement lại như papalPayment, creditPayment override lại pay() 
thì trong class Shopping dùng interface payMent chỉ cần gọi hàm pay là được , có 1 hàm dùng để set interface payMent là class con nào (papalPayment, hoặc creditPayment)
từ đó class Shopping không cần phải thay đổi mã nguồn, logic pay sẽ được xử lý ở từng thằng con implement lại từ interface payMent

# 3. Spring
## 3.1 Vòng đời bean (Scope) :
| Scope         | Áp dụng            | Đặc điểm                                |
| ------------- | ------------------ | --------------------------------------- |
| `singleton`   | Default (ứng dụng) | Một instance duy nhất trong container   |
| `prototype`   | Ứng dụng           | Mỗi lần `getBean()` là một instance mới |
| `request`     | Web app            | Mỗi HTTP request tạo một bean mới       |
| `session`     | Web app            | Một bean cho mỗi HTTP session           |
| `application` | Web app            | Một bean cho mỗi ServletContext         |
| `websocket`   | Web app            | Một bean cho mỗi WebSocket session      |


## 3.2 Inversion of Control(IOC), Dependency Injection(DI)
- IoC là nguyên lý thiết kế trong đó quyền điều khiển việc tạo và quản lý đối tượng được chuyển từ lập trình viên sang framework (Spring). Spring container tạo, cấu hình, và quản lý vòng đời các đối tượng
- Dependency Injection là kỹ thuật để Spring tiêm (inject) các đối tượng phụ thuộc (dependencies) vào một class, thay vì để class đó tự tạo. DI là cách cụ thể để thực hiện IoC.
- Các kiểu tiêm :
| Kiểu                      | Mô tả                   | Cách dùng                                            |
| ------------------------- | ----------------------- | ---------------------------------------------------- |
| **Constructor Injection** | Tiêm qua constructor    | ✅ Khuyến khích                                       |
| **Setter Injection**      | Tiêm qua setter method  | Dùng khi dependency không bắt buộc                   |
| **Field Injection**       | Tiêm trực tiếp vào biến | Ngắn gọn nhưng khó test (nên tránh trong production) |

- Spring Context (ApplicationContext)
- AOP
- Spring Data
- Spring Security
- Spring Transaction Management

# 4. Database 
Cơ sở dữ liệu quan hệ (Sequel) : MySql, Postgresql, sql server 
Schema(Lược đồ) bản thiết kế của toàn bộ csdl (Không lưu dữ liệu mà là cấu trúc)
Em phân biệt được các kiểu dữ liệu chính như số (int, float, decimal), chuỗi (varchar, text), thời gian (datetime, timestamp), boolean. Khi thiết kế bảng, em thường dùng VARCHAR cho chuỗi, BIGINT cho ID, DATETIME cho thời gian và BOOLEAN cho trạng thái. Ngoài ra, nếu dữ liệu cần độ chính xác cao như tiền tệ, em sẽ dùng DECIMAL thay vì FLOAT.


## 4.1 Các lệnh , từ khoá cơ bản : 
``` sql
+ Từ khoá liên quan đến bảng : 
CREATE, ALTER, DROP, TRUNCATE, DESCRIBE, SHOW , ENGINE, MEMORY
PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL, DEFAULT, CHECK, AUTO_INCREMENT, INDEX

+ Từ khoá liên quan đến truy vấn dữ liệu :
SELECT - FROM, WHERE, ORDER BY, GROUP BY, HAVING, LIMIT, OFFSET, DISTINCT, LIKE, IN, BETWEEN, UNION, VIEW, MIN, MAX, AVG, SUM, COUNT, AS
INSERT INTO - VALUES, UPDATE - SET - WHERE, DELETE FROM - WHERE

SELECT 
    column1, column2, aggregate_function(column3) AS alias_name
FROM 
    table_name
WHERE 
    condition1 AND condition2 OR condition3
GROUP BY 
    column1, column2
HAVING 
    aggregate_function(column3) > value
ORDER BY 
    column1 ASC, column2 DESC
LIMIT 
    row_count 
OFFSET 
    offset_value;

WHERE chỉ dùng lọc dữ liệu trước khi nhóm (GROUP BY) 
HAVING chỉ dùng sau khi nhóm (GROUP BY) 
HAVING, ORDER BY, LIMIT, OFFSET, JOIN Chỉ có thể sử dụng với SELECT(ko dùng dc với UPDATE, DELETE)

+ Từ khoá liên quan đến chỉ mục 
CREATE INDEX - ON , DROP INDEX - ON

+ Từ khóa liên quan đến giao dịch (Transactions) 
START TRANSACTION, COMMIT, ROLLBACK, SAVEPOINT 

+ Từ khóa liên quan đến Stored Procedures :
DELIMITER , CREATE PROCEDURE, IN | OUT | INOUT , BEGIN , END$$ , DELIMITER ,  CALL , SHOW PROCEDURE , DROP PROCEDURE
DECLARE , SET , IF , THEN , ELSE , END IF , WHILE , DO , END WHILE

+ Từ khóa liên quan đến Trigger :
CREATE TRIGGER , {BEFORE | AFTER} {INSERT | UPDATE | DELETE} , ON , FOR EACH ROW , NEW , OLD BEGIN, END

+ Từ khóa liên quan đến Function :
CREATE FUNCTION , DETERMINISTIC ( trả về cùng một kết quả với cùng một đầu vào), BEGIN , RETURN , END

+ Từ khóa liên quan đến PARTITION (Phân vùng) :
PARTITION BY RANGE , LIST , VALUES LESS THAN , VALUES IN , PARTITION BY KEY() , PARTITIONS 4
```

## 4.2.1 UNION kết hợp nhiều câu lệnh select
Lưu ý quan trọng:
    Các câu SELECT phải có số cột giống nhau.
    Thứ tự và kiểu dữ liệu của các cột cũng phải tương thích.
    UNION loại bỏ các dòng trùng lặp -> (giống DISTINCT).
    Dùng UNION ALL để giữ lại các dòng trùng lặp.

SELECT column1, column2 FROM tableA
UNION 
SELECT column1, column2 FROM tableB;


## 4.2 JOINS kết hợp nhiều bảng
+ inner join : Phần chung giữa 2 bảng, phép giao
SELECT * FROM <table> INNER JOIN <other_table> ON [conditions]

+ left join : Phần chung giữa 2 bảng và giá trị của bảng bên trái ( Bảng đứng trước chữ left join), nếu ko có thông tin chung thì trả về null
SELECT * FROM <table> LEFT JOIN <other_table> ON [conditions] LEFT JOIN <other_table> ON [conditions] WHERE [conditions]
Chủ yếu dùng left join (Lồng nhiều left join)
vd : Tìm kiếm người dùng (user) có phát sinh đơn hàng (order) , có thể thấy được 1000 người dùng nhưng chỉ có 10 người dùng phát sinh ra order

+ right join : Phần chung giữa 2 bảng và giá trị của bảng bên phải
SELECT * FROM <table> RIGHT JOIN <other_table> ON [conditions]
left join và right join có tư tưởng giống nhau 

+ full join : Trả về thông tin 2 bảng kể cả không có bảng nào được kết hợp
SELECT * FROM <table> FULL JOIN <other_table> ON [conditions]

SELECT c.customer_id, c.name, SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
HAVING SUM(o.total_amount) > 1000000
ORDER BY total_spent DESC;

## 4.3 Quan hệ (Relationship)
One-to-One : 1-1
One-to-Many : 1-n 
Many-to-Many : n-n Thường có thêm bảng trung gian kết nối 

enum trong code ánh xạ thành int trong csdl (Dùng cho các loại type , ví dụ coupon Type)

## 4.4 Chuẩn hoá (Normalization And Denormalization) 
Có các loại 1NF, 2NF, 3NF, BCNF loại bỏ sự trùng lặp, đảm bảo tính nhất quán và giảm thiểu các biến đổi dữ liệu.
+ 1NF : Mỗi ô trong bảng chỉ chứa 1 giá trị duy nhất .
VD : 1 ô chỉ có là "Hà nội" thôi, còn "Hà Nội","Đà Nẵng" , "Hà Nội,25,Nam"  hoặc "Đỏ,30,Lớn"  trong 1 ô là sai
chuẩn hoá bằng cách tách ra thành nhiều cột tương ứng

+ 2NF : Đã là 1NF và tất cả thuộc tính phải PHỤ THUỘC HOÀN TOÀN VÀO KHOÁ CHÍNH, chứ không phải phụ thuộc 1 phần vào khoá chính (Khoá chính là 2 cột , phụ thuộc 1 phần là phụ thuộc 1 cột vào khoá chính)
VD : Bảng có : order_id | product_id | product_name | quantity | product_price
Trong bảng này khoá chính là kết hợp của (order_id, product_id) , Mà product_name , product_price lại chỉ phụ thuộc vào product_id (1 phần của khoá chính không phải toàn bộ khoá chính) 
Do đó đã vi phạm chuẩn 2NF, ta có thể chuẩn hoá lại bảng thành : order_id | product_id | quantity 
Còn product_name | product_price thì ta đưa về lại bảng product 

+ 3NF : Đã là 2NF và Các thuộc tính không khoá phải phụ thuộc trực tiếp vào khoá chính
VD : Bảng có : employee_id | employee_name | department_id | department_name | department_location   
Khoá chính là employee_id
Đây là chuẩn 2NF do tất cả thuộc tính không khoá (employee_name, department_id, department_name, location) đều phụ thuộc vào khoá chính employee_id
Không đạt 3NF vì tồn tại thuộc tính bắc cầu giữa các giá trị không khoá : department_name,department_location  phụ thuộc vào department_id
Chuẩn hoá tách thành 2 bảng : employee_id | employee_name | department_id và bảng department_id | department_name | department_location   

+ BCNF : Đã là 3NF và Không có thuộc tính khoá mà phụ thuộc hàm vào thuộc tính không khoá. Trong mô hình microservice database bị chia nhỏ thì không cần làm tới mức này 
VD : Bảng StudentCourse : student_id | course_id | professor   có khoá là cặp (student_id, course_id)
Bảng là 3NF vì không khoá không phụ thuộc vào không khoá, nhưng vi phạm BCNF vì professor phụ thuộc vào course_id mà course_id lại không phải là siêu khoá
Chuẩn hoá tách thành 2 bảng : bảng CourseInstructor  course_id | professor    và bảng StudentCourse   student_id | course_id 

## 4.5 Transaction
- Bảng InnoDB 
Là bảng mặc định, hỗ trợ transactions, khóa hàng (row-level locking)

- Bảng MyISAM
Không hỗ trợ giao dịch hoặc khóa hàng (row-level locking), mà sử dụng khóa bảng (table-level locking) , nhanh hơn InnoDB

- Bảng MEMORY(HEAP)
Tất cả dữ liệu được lưu trữ trong bộ nhớ RAM, khi máy chủ MySQL khởi động lại hoặc gặp sự cố, toàn bộ dữ liệu trong bảng sẽ bị mất.
Bảng MEMORY có giới hạn về kích thước (được cấu hình bởi tham số max_heap_table_size).
Từ khoá ENGINE=MEMORY; khi tạo bảng
Phù hợp cho dữ liệu tạm thời như bộ đệm (cache) hoặc dữ liệu phiên làm việc.

- Transaction : Một transaction là một chuỗi các thao tác cơ sở dữ liệu được thực hiện như một đơn vị công việc duy nhất.
INSERT, UPDATE, DELETE, hoặc thậm chí SELECT (khi cần khóa dữ liệu).
Dùng trong chuyển tiền giữa tài khoản ngân hàng, đặt hàng trong thương mại điện tử, xử lý dữ liệu phức tạp
Từ khoá START TRANSACTION, COMMIT, SAVEPOINT, ROLLBACK

+ Nguyên tắc ACID :
Atomicity (Nguyên tử) : Tất cả các thao tác trong transaction phải hoàn thành thành công hoặc không có thao tác nào được thực hiện.
Consistency (Nhất quán) : Cơ sở dữ liệu phải chuyển từ trạng thái hợp lệ này sang trạng thái hợp lệ khác sau khi transaction kết thúc.
Isolation (Cách ly): Các transaction đồng thời không ảnh hưởng lẫn nhau.
Durability (Bền vững) : Khi transaction đã được commit, các thay đổi sẽ được lưu trữ vĩnh viễn, ngay cả khi hệ thống gặp sự cố.

+ Triển khai :
START TRANSACTION;

-- Trừ tiền từ tài khoản A
UPDATE accounts SET balance = balance - 100 WHERE account_id = 'A';
SAVEPOINT sp1;

-- Cộng tiền vào tài khoản B
UPDATE accounts SET balance = balance + 100 WHERE account_id = 'B';

IF (SELECT balance FROM accounts WHERE account_id = 'A') == 0 THEN
    ROLLBACK TO sp1;
    
-- Kiểm tra điều kiện (ví dụ: số dư không âm)
IF (SELECT balance FROM accounts WHERE account_id = 'A') >= 0 THEN
    COMMIT; -- Hoàn thành giao dịch
ELSE
    ROLLBACK; -- Hủy bỏ giao dịch nếu không đủ số dư
END IF;

+ Nhược điểm : Transaction yêu cầu khóa dữ liệu (locking) để đảm bảo tính cách ly, điều này có thể làm giảm hiệu suất trong môi trường nhiều người dùng.
+ Các cấp độ cách ly (Isolation Levels) :MySQL InnoDB mặc định là REPEATABLE READ. PostgreSQL,SQL Server, Oracle: Mức độ cách ly mặc định là READ COMMITTED, 
READ UNCOMMITTED : Cho phép đọc dữ liệu chưa được commit. Có thể xảy ra "Dirty Read".
READ COMMITTED : Chỉ cho phép đọc dữ liệu đã được commit. Có thể xảy ra "Non-Repeatable Read".
REPEATABLE READ : Đảm bảo rằng dữ liệu không thay đổi trong suốt transaction (mặc định).
SERIALIZABLE : Ngăn chặn hoàn toàn các transaction đồng thời, cho nó đi tuần tự hết.

"Non-Repeatable Read" : Khi một transaction đọc một hàng dữ liệu, sau đó một transaction khác cập nhật hoặc xóa hàng đó và commit, transaction ban đầu đọc lại hàng này sẽ thấy giá trị mới.
Chỉ áp dụng cho transaction tiếp theo và chỉ transaction đó : SET TRANSACTION ISOLATION LEVEL READ COMMITTED; 
Áp dụng cho toàn bộ phiên làm việc (SESSION) : SET SESSION TRANSACTION ISOLATION LEVEL <level>;
Áp dụng cho toàn bộ máy chủ (GLOBAL) : SET GLOBAL TRANSACTION ISOLATION LEVEL <level>;

- Khóa (Locking) ,tranh chấp (Contention), (Race Condition) và Deadlock (bế tắc) :
Khoá (Locking) là cơ chế hệ quản trị dùng để kiểm soát quyền truy cập vào các tài nguyên (như hàng, bảng, hoặc chỉ mục) để tránh xung đột giữa các transaction.
Khi một transaction khóa một tài nguyên, các transaction khác không thể thực hiện thao tác trên tài nguyên đó cho đến khi khóa được giải phóng.
+ Các loại phạm vi khoá :
    Khóa hàng (Row-Level Locking) : InnoDB, Tiêu tốn nhiều tài nguyên hơn so với khóa bảng.
    Khóa bảng (Table-Level Locking) : MyISAM , Hạn chế khả năng truy cập đồng thời
    Khóa chỉ mục (Index-Level Locking) : InnoDB, Khóa áp dụng trên các chỉ mục thay vì trực tiếp trên dữ liệu.
+ Các loại khoá :
    Khóa chia sẻ (Shared Lock - S Lock) : Cho phép nhiều transaction đọc dữ liệu nhưng không cho phép ghi. Phù hợp SELECT
    Khóa độc quyền (Exclusive Lock - X Lock) : Chỉ cho phép một transaction duy nhất truy cập vào tài nguyên (đọc và ghi). Phù hợp INSERT, UPDATE, hoặc DELETE.

START TRANSACTION;
SELECT stock FROM products WHERE product_id = 1 ; -- Đọc và khóa hàng với khóa chia sẻ (Shared Lock - S Lock)
SELECT stock FROM products WHERE product_id = 1 FOR UPDATE; -- Đọc và khóa hàng với khoá độc quyền (Exclusive Lock - X Lock)

READ UNCOMMITTED : Không khoá hàng
READ COMMITTED : Chỉ Áp dụng khóa độc quyền (X Lock) cho các thao tác ghi (INSERT, UPDATE, DELETE)
REPEATABLE READ : Áp dụng khóa chia sẻ (S Lock) và áp dụng khóa độc quyền (X Lock) cho các thao tác ghi.
SERIALIZABLE :Chỉ Áp dụng khóa độc quyền (X Lock) trên toàn bộ phạm vi dữ liệu bị ảnh hưởng.

Tranh chấp (Contention) xảy ra khi nhiều transaction cố gắng truy cập vào cùng một tài nguyên (hàng, bảng, hoặc chỉ mục) và phải đợi nhau để giải phóng khóa.
Deadlock (bế tắc) là tình huống khi hai hoặc nhiều transaction đang chờ nhau giải phóng khóa, dẫn đến không có transaction nào có thể thực thi, gây treo vô thời hạn. 
    T1 đang giữ khóa trên hàng A và chờ T2 giải phóng khóa trên hàng B.
    T2 đang giữ khóa trên hàng B và chờ T1 giải phóng khóa trên hàng A.
    Cả hai transaction đều bị treo vô thời hạn, dẫn đến deadlock.
Cách xử lý : 
    MySQL tự động phát hiện deadlock và cho một transaction làm "nạn nhân" và rollback nó để giải phóng khóa.
    Lập trình để nó truy cập tài nguyên theo thứ tự nhất quán, VD trên : Luôn chạy vào A trước khi chạy vào B
    Giảm thời gian giữ khóa, Chia nhỏ transaction, LOCK TABLES, Retry logic

## 4.6 Stored Procedures, Function, Trigger
- Stored Procedures (thủ tục lưu trữ) là một khối mã SQL được lưu trữ trong cơ sở dữ liệu và có thể được gọi để thực thi khi cần.
Có thể nhận tham số đầu vào, trả về kết quả , thực hiện các thao tác phức tạp như sử dụng biến, sử dụng điều kiện (IF/ELSE), sử dụng vòng lặp để chèn, cập nhật, xóa, hoặc truy vấn dữ liệu.
Ưu điểm : 
    Bảo mật Người dùng chỉ cần quyền thực thi thủ tục mà không cần quyền truy cập trực tiếp vào bảng.
    Giảm tải mạng Thay vì gửi nhiều câu lệnh SQL từ ứng dụng, chỉ cần gửi một lệnh gọi thủ tục.
    Tái sử dụng mã, Tăng hiệu suất
VD :  Tạo một thủ tục để tính giá sau khi áp dụng giảm giá:
DELIMITER $$
CREATE PROCEDURE CalculateDiscount(IN original_price DECIMAL(10, 2), OUT discounted_price DECIMAL(10, 2))
BEGIN
    DECLARE discount DECIMAL(10, 2) DEFAULT 0.1; -- Giảm giá 10%
    SET discounted_price = original_price * (1 - discount);
END$$
DELIMITER ;

CALL CalculateDiscount(1000.00, @discounted);  -- Gọi thủ tục
SELECT @discounted AS DiscountedPrice;

- Hàm Function tương tự Stored Procedure ,có điểm riêng biệt như luôn trả về một giá trị duy nhất và có thể được sử dụng trực tiếp trong các truy vấn SELECT.
thường được sử dụng để tính toán hoặc xử lý dữ liệu ngay trong truy vấn.
VD : Tạo một hàm để tính giá sau khi áp dụng giảm giá:
DELIMITER $$
CREATE FUNCTION CalculateDiscountedPrice(original_price DECIMAL(10, 2), discount DECIMAL(5, 2))
RETURNS DECIMAL(10, 2)
DETERMINISTIC
BEGIN
    DECLARE discounted_price DECIMAL(10, 2);
    SET discounted_price = original_price * (1 - discount);
    RETURN discounted_price;
END$$
DELIMITER ;

Cách gọi hàm : Có thể gọi trong SELECT, INSERT, UPDATE
    SELECT CalculateDiscountedPrice(1000.00, 0.1) AS DiscountedPrice;
    INSERT INTO products (name, price, discounted_price) VALUES ('Laptop', 1200.00, CalculateDiscountedPrice(1200.00, 0.1));
    UPDATE products SET discounted_price = CalculateDiscountedPrice(price, 0.1) WHERE id = 1;

-   :
+ Mục đích : 
    Function thực hiện tính toán, xử lý dữ liệu, và trả về kết quả để sử dụng trong truy vấn. VD : Tính tổng tiền sau khi áp dụng giảm giá, Tạo chuỗi đầy đủ từ tên và họ.
    Thực hiện các thao tác phức tạp như chèn, cập nhật, xóa, hoặc gọi nhiều câu lệnh SQL. VD : Thêm một sản phẩm mới vào bảng products, Cập nhật số lượng hàng tồn kho và trả về số lượng mới.
+ Trả về giá trị :
    Function trả về một giá trị duy nhất và có thể được sử dụng trực tiếp trong truy vấn SELECT
    Procedure có thể trả về kết quả qua tham số OUT hoặc INOUT

- Triggers (kích hoạt) là các khối mã SQL được thực thi tự động có thể chạy trước (BEFORE) hoặc sau (AFTER) khi một sự kiện cụ thể (INSERT, UPDATE, DELETE) xảy ra trên bảng trong cơ sở dữ liệu.
Dùng để kiểm tra hoặc sửa đổi dữ liệu trước khi chúng được lưu trữ, ghi nhật ký
VD : Thêm ngày tự động khi cập nhập , 
DELIMITER $$
CREATE TRIGGER AfterDeleteEmployee
AFTER DELETE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO deleted_employees (id, name, deleted_at)
    VALUES (OLD.id, OLD.name, NOW()); -- Ghi lại thông tin nhân viên bị xóa
END$$
DELIMITER ;

## 4.7 Tối ưu truy vấn với Partitioning, Indexing, Materialized Views
- Partitioning (phân vùng)
là một kỹ thuật trong cơ sở dữ liệu để chia một bảng lớn thành các phần nhỏ hơn, giúp thực hiện các thao tác trên dữ liệu nhanh hơn
Phân vùng thì dính vào bảng cụ thể, có thể phân lúc mới tạo bảng hoặc add thêm phân vùng vào bảng
VD : Phân vùng theo ngày, Phân vùng theo quốc gia,
PARTITION BY RANGE (YEAR(sale_date)) (
    PARTITION p2020 VALUES LESS THAN (2021),
    PARTITION p2021 VALUES LESS THAN (2022),
    PARTITION p2022 VALUES LESS THAN (2023),
    PARTITION p2023 VALUES LESS THAN MAXVALUE
);
PARTITION BY LIST (country) (
    PARTITION p_usa VALUES IN ('USA'),
    PARTITION p_canada VALUES IN ('Canada'),
    PARTITION p_uk VALUES IN ('UK')
);

- Indexing 
Ưu điểm :
Index là cấu trúc dữ liệu SẮP XẾP giúp tăng hiệu suất khi truy vấn, nó tạo 1 bảng mapping giữa các cột được chỉ định( cột index ) với các cột tương ứng trong bảng 
Cải thiện hiệu năng đọc dữ liệu,có thể đánh index các cột hay được sử dụng 1 cột, nhiều cột hay unique
Tốt với mệnh đề WHERE, JOIN, ORDER BY, hoặc GROUP BY, triệu bản ghi trở lên, phù hợp bài toán đọc quan trọng hơn ghi
index sử dụng B-Tree (balanced tree),Tìm kiếm binarySearch  O(log n), cây tự cân bằng , O(logn)

Nhược điểm : 
insert,delete và update không được nhanh do cần viết lại cây cùng với bảng dữ liệu
và việc cập nhật hoặc xóa dữ liệu có thể gây ra khóa (lock) trên các hàng hoặc chỉ mục. 
Điều này có thể dẫn đến tranh chấp (contention), làm giảm hiệu suất tổng thể của hệ thống.

Cú pháp: CREATE INDEX <index_name> ON <table_name> (column_1, column_2, ...).
VD: CREATE INDEX idx_customers_last_name ON customers (last_name);
Sử dụng: SELECT * FROM customers WHERE last_name = Giang';

- Materialized Views là một bản sao vật lý của kết quả truy vấn, được cập nhật định kỳ.
Có thể chạy lại theo Manual, Scheduled (cron job), Auto refresh (Incremental).Dùng để truy vấn phức tạp VD Dashboard
CREATE MATERIALIZED VIEW mv_employee_stats AS
SELECT department_id, COUNT(*) AS total_employees, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;

## 4.8 Note
- Hệ thống database phân tán lưu trữ trên nhiều máy tính (nodes) khác nhau, nằm ở các vị trí địa lý khác nhau, nhưng vẫn hoạt động như một cơ sở dữ liệu duy nhất.
CAP Theorem : trong một hệ thống phân tán, bạn chỉ có thể đạt được tối đa hai trong ba thuộc tính sau :
    Consistency (Nhất quán): Tất cả các node nhìn thấy cùng một dữ liệu tại cùng một thời điểm.
    Availability (Sẵn sàng): Mọi yêu cầu đều nhận được phản hồi, dù dữ liệu có nhất quán hay không.
    Partition Tolerance (Chịu lỗi phân vùng): Hệ thống tiếp tục hoạt động ngay cả khi có sự cố mạng giữa các node.

- Cải tiến hiệu suất :
Denormalization : Chủ ý vi phạm chuẩn hoá, cố ý đưa vào trùng lặp để giúp tăng tốc truy vấn ( Lưu ý vấn đề dữ liệu mất nhất quán)
Materialized views : Tạo bảng chứa kết quả các truy vấn phức tạp
Indexing : Tạo các index trên cột thường dùng để tìm kiếm , sắp xếp
Partitioning : Phân chia bảng lớn thành 1 bảng nhỏ cải thiện hiệu suất truy vấn 
Caching : Lưu kết quả truy vấn tạm thời 


- Cơ sở dữ liệu không quan hệ NoSQL là viết tắt của "Not Only SQL" : Redis (Key-value), MongoDB(JSON), Graph(Lưu dạng Node, Neo4j), Cassandra(Column family)

## 4.9 Redis
Redis là một hệ quản trị cơ sở dữ liệu dạng key-value nằm trong RAM, cực kỳ nhanh, hỗ trợ nhiều kiểu dữ liệu có thể ghi ra ổ đĩa (persistence) tùy cấu hình.

| Use case             | Mô tả thực tế                            |
| -------------------- | ---------------------------------------- |
| **Cache**            | Lưu tạm kết quả DB để truy vấn nhanh hơn |
| **Session Store**    | Lưu session login của user               |
| **Rate Limiting**    | Đếm số request/IP theo thời gian         |
| **Message Queue**    | Dùng Redis List/Stream để làm hàng đợi   |
| **Leaderboard/Game** | Dùng Sorted Set cho bảng xếp hạng        |
| **Pub/Sub**          | Gửi thông báo, cập nhật real-time        |
| **Locking**          | Làm distributed lock giữa nhiều server   |



# 5. Cloud
Cloud (điện toán đám mây) là một mô hình cung cấp tài nguyên và dịch vụ máy tính thông qua mạng Internet.
Ba loại dịch vụ chính : Infrastructure as a Service (IaaS), Platform as a Service (PaaS), Software as a Service (SaaS)
VD : IaaS = AWS EC2, PaaS = Heroku, SaaS = Gmail
Các mô hình triển khai : public cloud , private cloud , hybrid cloud , và multi-cloud .
VD : Amazon Web Services (AWS), Google Cloud Platform (GCP), Microsoft Azure, IBM Cloud, Oracle Cloud

## 5.1 Infrastructure as a Service (IaaS) : Lưu trữ, mạng, hệ điều hành
Là mô hình cung cấp tài nguyên hạ tầng(máy chủ ảo, lưu trữ, mạng và hệ điều hành) công nghệ thông tin (IT) dưới dạng dịch vụ qua Internet.
- Máy chủ ảo (Virtual Machines - VMs) : Là tài nguyên chính của IaaS, cho phép người dùng chạy các ứng dụng và hệ điều hành trên môi trường ảo hóa.
Ví dụ: Amazon Elastic Compute Cloud (EC2), Google Compute Engine (GCE), Microsoft Azure Virtual Machines
- Lưu trữ (Storage) Cung cấp không gian lưu trữ dữ liệu trên đám mây, bao gồm: 
  + Block Storage: Lưu trữ giống như ổ cứng (ví dụ: AWS Elastic Block Store (EBS)).
  + Object Storage: Lưu trữ dữ liệu dưới dạng đối tượng duy nhất metadata ,VD lưu ảnh,video theo id (ví dụ: AWS S3).
  + File Storage: Lưu trữ dữ liệu dưới dạng file phân cấp (ví dụ: AWS EFS).
- Mạng (Networking) Cung cấp các dịch vụ mạng như :
  + IP Addressing: Gán địa chỉ IP cho máy chủ.
  + Load Balancing: Phân phối tải giữa các máy chủ.
  + Firewall: Bảo vệ tài nguyên khỏi các cuộc tấn công mạng.
- Hệ điều hành (Operating System) như Linux, Windows để triển khai trên máy chủ ảo.
- Công cụ quản lý (Management Tools) để giám sát, điều chỉnh và tự động hóa tài nguyên.

## 5.2 Platform as a Service (PaaS) : runtime
Là mô hình cung cấp một nền tảng phát triển và triển khai ứng dụng qua Internet.
Các thành phần: 
- Development Tools tích hợp (IDE), trình biên dịch, thư viện, và framework để xây dựng ứng dụng.
Ví dụ: Google App Engine hỗ trợ các ngôn ngữ lập trình như Python, Java, Node.js.
- Middleware Là phần mềm hoạt động giữa hệ điều hành và ứng dụng, cung cấp các dịch vụ như API, message queue, và caching.
Ví dụ: IBM Cloud cung cấp middleware để quản lý giao tiếp giữa các ứng dụng.
- Database Management Cung cấp các dịch vụ cơ sở dữ liệu như MySQL, PostgreSQL, MongoDB, hoặc các cơ sở dữ liệu NoSQL.
Ví dụ: AWS RDS (Relational Database Service) hoặc Google Cloud SQL.
- Runtime Environment Cung cấp môi trường thực thi cho ứng dụng, bao gồm web server, container, và virtual machine.
Ví dụ: Heroku hỗ trợ runtime environment cho các ứng dụng Ruby, Python, và Java.
- DevOps Tools Hỗ trợ các công cụ CI/CD (Continuous Integration/Continuous Deployment) để tự động hóa quá trình phát triển và triển khai.
Ví dụ: Azure DevOps, GitHub Actions.

## 5.3 Software as a Service (SaaS) : gmail, team, google driver
Là mô hình cung cấp phần mềm hoàn chỉnh qua Internet dưới dạng dịch vụ.
VD:  
Google Workspace : Gmail, Google Drive, Google Docs, Google Sheets.
Microsoft 365 : Word, Excel, PowerPoint, Outlook, Teams.
Salesforce, Slack, Dropbox

## 5.4 So sánh IaaS, PaaS, SaaS
- IaaS
Bạn thuê mặt bằng, mua bàn ghế, máy pha cà phê, và tự quản lý mọi thứ.
Bạn thuê tài nguyên hạ tầng (máy chủ ảo, lưu trữ, mạng) từ nhà cung cấp như AWS EC2, Google Compute Engine.
- PaaS
Bạn thuê quán cà phê đã được trang bị sẵn bàn ghế, máy móc, và nhân viên phục vụ.
Bạn sử dụng nền tảng phát triển ứng dụng (Google App Engine, Heroku) mà không cần quản lý hạ tầng.
- SaaS
Bạn đến quán cà phê và gọi đồ uống đã được pha sẵn.
Bạn sử dụng phần mềm hoàn chỉnh qua Internet (Gmail, Salesforce).

## 5.5 So sánh Các Nhà Cung Cấp Dịch Vụ Cloud Nổi Tiếng
- Amazon Web Services (AWS) là nhà cung cấp dịch vụ cloud lớn nhất thế giới, Ra mắt năm 2006, thuộc sở hữu của Amazon.
Đa dạng dịch vụ, 32% thị phần cloud toàn cầu.
- Microsoft Azure là nền tảng cloud của Microsoft, ra mắt năm 2010, Phù hợp cho các doanh nghiệp sử dụng hệ sinh thái Microsoft (Windows Server, Active Directory, Office 365),  22% thị phần cloud toàn cầu.
- Google Cloud Platform (GCP) là nền tảng cloud của Google, ra mắt năm 2011, 10% thị phần cloud toàn cầu.
- Alibaba Cloud 9% thị phần cloud toàn cầu, IBM Cloud 3% thị phần cloud toàn cầu , Oracle Cloud Infrastructure (OCI) 2% thị phần cloud toàn cầu .

# 6. Java core 
Java LTS 8,17,21
## 6.1 Thread, Mutil Thread, lập trình đa nhiệm (multitasking), xử lý đồng thời (concurrency)
Process là một chương trình đang chạy trên hệ điều hành.
Thread là một đơn vị thực thi nhỏ nhất trong một process, cùng process có thể chia sẻ tài nguyên
Đơn luồng (single-threading) một chương trình  chỉ sử dụng một thread duy nhất để thực thi mã nguồn, tất cả các tác vụ được thực hiện tuần tự từ đầu đến cuối.
Đa luồng (multi-threading) một chương trình sử dụng nhiều thread để thực thi mã nguồn, thread có thể chạy song song trên các nhân CPU khác nhau hoặc xen kẽ (interleaved) trên cùng một nhân.

- Cách tạo 1 thread :
+ Truyền vào 1 anonymous function :
Thread thread1 = new Thread(() -> {
      for (int i = 0; i < 1000; i++) {
          counter.increment();
      }
  });
thread1.start();

+ Kế thừa lớp Thread : Phương thức run() chứa mã nguồn mà thread sẽ thực thi.
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}
MyThread thread = new MyThread();
thread.start(); 

+ Triển khai giao diện Runnable : Phương thức run() chứa mã nguồn mà thread sẽ thực thi.
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable is running");
    }
}
Thread thread = new Thread(new MyRunnable());
thread.start();

+ Có thể tạo pool chứa nhiều thread để quản lý.

- Thread chạy nền (Daemon Thread) hỗ trợ các thread khác (non-daemon thread) trong quá trình thực thi.
tự động bị dừng khi tất cả các non-daemon thread (thread chính và các thread không phải daemon) kết thúc.
VD : Garbage Collector, Logging, hoặc các tác vụ giám sát hệ thống.
isDaemon() để kiểm tra và setDaemon(boolean on) : Đặt thread là daemon thread (chạy nền).
Lưu ý : không setDaemon(true) khi đã start(), nếu không sẽ gây lỗi

- Vòng đời của thread :
+ New : Thread đã được tạo new Thread() nhưng chưa khởi động.
+ Runnable : Thread đã được khởi động bằng phương thức start()
+ Blocked/Waiting : bị chặn hoặc đang chờ tài nguyên/tín hiệu từ thread khác synchronized, wait(), join()
+ wait( | long mili) : Phải được gọi từ khối synchronized, muốn chạy tiếp đợi hết time hoặc Một thread khác gọi notify() hoặc notifyAll() trên cùng đối tượng.
+ Terminated : Thread đã hoàn thành thực thi hoặc bị dừng(interrupted). 

- Các hàm làm việc với Thread :
+ run() : Không gọi phương thức này vì nó sẽ chạy trên Main Thread
+ start() : Chạy run() nhưng là trên thread mới
+ isAlive() : true nếu thread đang chạy, false nếu thread đã kết thúc.
+ setName(String name) và getName() : Lấy tên và đặt tên cho thread
+ getId() : Trả về ID duy nhất của thread.
+ getState() : Các trạng thái có thể trả về: NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED.
+ stop() : 
+ interrupt() : Gửi tín hiệu ngắt (interrupt) đến một thread, nó không tự động dừng thread mà chỉ gửi tín hiệu ngắt.
Sau khi biết nó interrupt cần viết code xử lý, ví dụ như giải phóng tài nguyên trước khi dừng
Thread cần kiểm tra trạng thái interrupted hoặc xử lý ngoại lệ InterruptedException để phản hồi tín hiệu ngắt.
Th1 : Kiểm tra trạng thái interrupted khi thread đang ở trạng thái chạy :
 while (!Thread.currentThread().isInterrupted()){}
Th2 : Bắt ngoại lệ InterruptedException thread đang ở trạng thái chờ (sleep, wait, join)
 try {
      while (!Thread.currentThread().isInterrupted()) {
          System.out.println("Thread is running...");
          Thread.sleep(500); // Giả lập tác vụ nặng
      }
  } catch (InterruptedException e) {
      System.out.println("Thread interrupted. Stopping...");
      Thread.currentThread().interrupt()
  }
Nếu không xử lý nó sẽ tiếp tục chạy
Khi InterruptedException được bắt, trạng thái interrupted của thread bị reset về false.Nên cần Thread.currentThread().interrupt()
để đặt lại trạng thái interrupted thành true

+ join() : Chờ thread hoàn thành trước khi tiếp tục thực thi thread hiện tại. Block chính thread gọi nó
VD : thread1.join() gọi trên main thread thì chỉ main thread bị block đến khi thread1 hoàn thành, còn lại các thread khác chạy bình thường ví dụ : Th1
        task1.start();
        task2.start();
        task1.join(); 
        task2.join(); 
Khác với Th2
        task1.start();
        task1.join(); 
        task2.start();
        task2.join(); 
Ở th1 : task1 và task2 có thể chạy song song hoặc xen kẽ nhau, do main thread start cùng lúc 2 task, sau đó nó nhận lệnh đợi cho task1,task2 hoàn thành mới được chạy tiếp do đó thời gian có thể rút ngắn
Ở th2 : task1 được main thread chạy rồi nhận lệnh join đợi cho task1 hoàn thành xong mới chạy tiếp task2 rồi lại đợi task2 hoàn thành, do đó nó là chạy tuần tự, như không dùng đa luồng

+ getPriority() và setPriority(int priority) : ưu tiên của thread.
  Thread.MIN_PRIORITY (1): Ưu tiên thấp nhất.
  Thread.NORM_PRIORITY (5): Ưu tiên mặc định.
  Thread.MAX_PRIORITY (10): Ưu tiên cao nhất.

- Các hàm static :
+ Thread.currentThread() : Trả về tham chiếu đến thread hiện tại.
+ Thread.yield() : Nhường CPU cho các thread khác cùng mức ưu tiên.
+ Thread.activeCount() : Trả về số lượng thread đang hoạt động trong nhóm thread hiện tại.
+ Thread.sleep(long millis) : tạm dừng thread hiện tại , không giải phóng lock khi thực thi sleep().

- Cách chia sẻ bộ nhớ dùng chung
+ Giao diện Lock của java.util.concurrent.locks.Lock
    lock.lock() : Chặn thread hiện tại cho đến khi lấy được lock.
    lock.unlock() : Giải phóng lock, cho phép các thread khác truy cập tài nguyên. Dùng trong finally, bắt buộc khi dùng lock
    lock.tryLock() : Thử lấy lock mà không chặn. Trả về true nếu thành công, false nếu không.
    lock.tryLock(long time, TimeUnit unit) : Thử lấy lock trong một khoảng thời gian cố định.
    lock.lockInterruptibly() : Lấy lock nhưng có thể bị ngắt bởi tín hiệu interrupt()

+ Từ khoá ReentrantLock : Là một triển khai phổ biến của giao diện Lock.
    lock.lock() , lock.unlock()
    ReadWriteLock : lock.readLock().lock() , lock.writeLock().lock()
    Nhiều thread có thể đọc dữ liệu đồng thời bằng readLock().
    Chỉ một thread có thể ghi dữ liệu tại một thời điểm bằng writeLock().

+ Từ khóa synchronized Chỉ có một thread duy nhất có thể truy cập vào tài nguyên hoặc phương thức tại một thời điểm.
public synchronized void increment() {
      count++;
  }
synchronized (lock) { // Chỉ đồng bộ hóa phần mã này
      return count;
  }

-  Thread-Safe Collections, Concurrent Collections cấu trúc dữ liệu hỗ trợ thread-safe :
+ Thread-Safe Collections : Vector, Hashtable, Stack,
Các collections này được đồng bộ hóa bằng cách sử dụng từ khóa synchronized, chỉ có một thread thực hiện thao tác tại một thời điểm.
+ Concurrent Collections : thiết kế đặc biệt cho môi trường đa luồng, sử dụng các kỹ thuật như lock splitting , non-blocking algorithms , và read-write locks để tối ưu hóa hiệu suất.

- ExecutorService : để quản lý thread pool thay vì tạo thread thủ công.
- ScheduledExecutorService : lập lịch thực thi các tác vụ định kỳ.
- CompletableFuture : để xử lý các tác vụ bất đồng bộ mà không cần quản lý thread thủ công. (Giống promise)
- Deadlock
- Thread-safe và Concurrent Collections

////
Đưa ra các khái niệm tôi có thể cần biết, mở rộng cần thiết liên quan đến chủ đề này
Thread trong spring boot, nó được ứng dụng như nào
Thread trong spring boot, cách tạo các luồng
Nếu như triển khai 1 ứng dụng spring boot làm backend thì mỗi request gửi lên thì nó xử lý là 1 luồng hay 1 process, cách nó dùng cpu giải quyết vấn đề như sử dụng tài nguyên, giải thích chi tiết các vấn đề liên quan
////

- collections framework
## 6.2 Các loại cấu trúc dữ liệu trong Java
- Java Collections Framework (JCF) nằm trong gói java.util, có 2 nhóm chính chia theo interface:
| Interface | Đặc điểm                                   | Triển khai phổ biến                         |
| --------- | ------------------------------------------ | ------------------------------------------- |
| `List`    | Duy trì thứ tự, cho phép trùng             | `ArrayList`, `LinkedList`                   |
| `Set`     | Không trùng lặp, không theo thứ tự         | `HashSet`, `TreeSet`, `LinkedHashSet`       |
| `Queue`   | FIFO, có thể là hàng đợi hoặc hàng ưu tiên | `LinkedList`, `PriorityQueue`, `ArrayDeque` |

Map<K, V> không kế thừa Collection, nhưng nó là một phần của Java Collections Framework.
| Interface  | Đặc điểm                       | Triển khai phổ biến                                        |
| ---------- | ------------------------------ | ---------------------------------------------------------- |
| `Map<K,V>` | Lưu key-value, không trùng key | `HashMap`, `TreeMap`, `LinkedHashMap`, `ConcurrentHashMap` |

- Kiểu chuỗi 
| Loại            | Lớp             | Tính chất                 | Khi nào dùng?                         |
| --------------- | --------------- | ------------------------- | ------------------------------------- |
| `String`        | `String`        | ✅ Immutable               | Gần như luôn dùng                     |
| `StringBuilder` | `StringBuilder` | ✅ Mutable (thay đổi được) | Dùng trong xử lý chuỗi lớn, đơn luồng |
| `StringBuffer`  | `StringBuffer`  | ✅ Mutable + ✅ Thread-safe | Dùng trong đa luồng (cũ)              |


## 6.3 So sánh để hiểu rõ:
- So sánh ArrayList và Array: 
+ ArrayList lấy từ java.util.ArrayList còn Array là nguyên thuỷ không cần import
+ ArrayList là mảng động(Khi elementData đầy → tạo mảng mới 1.5x – 2x kích thước → copy phần tử cũ sang),size khác compacity  dùng được các phương thức add, get,remove vân vân do kế thừa List, ArrayList<Integer> list = new ArrayList<> 
+ Sắp xếp Array thì là Arrays.sort(array) , ArrayList thì là Collections.sort(list);
+ Tìm kiếm tuyến tính : Array dùng vòng for lặp, ArrayList dùng contains(), indexOf() vẫn như nhau chỉ là nó gọi hàm tiện hơn thôi
+ Tìm kiếm nhị phân goị từ lớp trên : int index = Arrays.binarySearch(arr, 3); Collections.binarySearch(list, 3);

- LinkedList có thể dùng để tạo List, Stack, Deque, Queue
+ 1 số phương thức: addFirst,addLast,removeFirst,removeLast,getFirst,getLast,contains,indexOf

- Set : Không trùng lặp, tìm nhanh O(1) phổ biến HashSet,LinkedHashSet,TreeSet : Set<String> set = new HashSet<>();
| Loại `Set`            | Đặc điểm chính                         | Duy trì thứ tự? | Sắp xếp? |
| --------------------- | -------------------------------------- | --------------- | -------- |
| `HashSet`             | ✅ Nhanh nhất, dùng `HashMap` nội bộ    | ❌ Không         | ❌ Không  |
| `LinkedHashSet`       | ✅ Nhớ thứ tự chèn                      | ✅ Có            | ❌ Không  |
| `TreeSet`             | ✅ Sắp xếp tự nhiên / custom comparator | ✅ Có (tự sắp)   | ✅ Có     |
| `EnumSet`             | ✅ Cho Enum, rất hiệu quả               | ✅ Có            | ❌ Không  |
| `CopyOnWriteArraySet` | ✅ Dùng cho đa luồng (thread-safe)      | ✅ Có            | ❌ Không  |

- Map : Giống Set, chỉ có tree mới tự động sắp xếp theo key, truyền vào Comparator còn lại không sắp xếp

| Cấu trúc | Dạng dữ liệu lưu    | Cho phép trùng | Truy cập          |
| -------- | ------------------- | -------------- | ----------------- |
| `List`   | Dạng danh sách      | ✅              | Theo index        |
| `Set`    | Tập hợp không trùng | ❌              | Duyệt tuần tự     |
| `Map`    | Key – Value         | ❌ key trùng    | Truy cập theo key |

- Duyệt phần tử:
| Kiểu   | Duyệt theo for | for-each | Iterator | Stream | forEach() | Có index |
| ------ | -------------- | -------- | -------- | ------ | --------- | -------- |
| `List` | ✅              | ✅        | ✅        | ✅      | ✅         | ✅        |
| `Set`  | ❌              | ✅        | ✅        | ✅      | ✅         | ❌        |
| `Map`  | ❌              | ❌        | ✅        | ✅      | ✅         | ❌        |

- So sánh hiệu suất (Big O)
| Hoạt động                      | `HashSet` | `HashMap` |
| ------------------------------ | --------- | --------- |
| `add()`                        | O(1)      | O(1)      |
| `remove()`                     | O(1)      | O(1)      |
| `contains()` / `containsKey()` | O(1)      | O(1)      |
| `get()`                        | —         | O(1)      |
| `iteration`                    | O(n)      | O(n)      |

| Hoạt động                      | `TreeSet` | `TreeMap` |
| ------------------------------ | --------- | --------- |
| `add()`                        | O(log n)  | O(log n)  |
| `remove()`                     | O(log n)  | O(log n)  |
| `contains()` / `containsKey()` | O(log n)  | O(log n)  |
| `get()`                        | —         | O(log n)  |
| `iteration` (theo thứ tự)      | O(n)      | O(n)      |

| Tiêu chí               | `Set`                                          | `Map`                                                              |
| ---------------------- | ---------------------------------------------- | ------------------------------------------------------------------ |
| **Gói (package)**      | `java.util.Set`                                | `java.util.Map`                                                    |
| **Mục đích**           | Lưu **tập hợp phần tử** không trùng            | Lưu **các cặp key-value**                                          |
| **Cặp key-value**      | ❌ Không có                                     | ✅ Có (key → value)                                                 |
| **Key là duy nhất**    | Các phần tử là key, nên luôn duy nhất          | ✅ Key phải duy nhất                                                |
| **Value có thể trùng** | Không có value riêng                           | ✅ Cho phép value trùng                                             |
| **Thứ tự phần tử**     | Không đảm bảo (trừ `LinkedHashSet`, `TreeSet`) | Không đảm bảo (trừ `LinkedHashMap`, `TreeMap`)                     |
| **Triển khai chính**   | `HashSet`, `LinkedHashSet`, `TreeSet`          | `HashMap`, `LinkedHashMap`, `TreeMap`                              |
| **Duyệt qua phần tử**  | Duyệt phần tử duy nhất                         | Duyệt key, value hoặc entry                                        |
| **Cho phép null**      | ✅ 1 phần tử null (`HashSet`)                   | ✅ 1 key null (`HashMap`), nhiều value null                         |
| **Ứng dụng thực tế**   | Dùng để loại trùng, tập hợp, tag, danh mục...  | Dùng để tra cứu nhanh, ánh xạ dữ liệu (id → user, slug → bài viết) |



- Sort: Dùng Arrays.sort(), Collections.sort() hoặc list.sort() , Cái nào ko có sort hoặc ko tự động sort thì đổi qua list rồi sort




- Ví dụ trong web java springboot:
Lưu Log, Log có thể trùng (vì user đăng nhập nhiều lần)
private List<String> loginLogs;

Một User có nhiều Role không trùng vai trò
private Set<Role> roles;

Lưu tùy chọn cấu hình riêng cho mỗi người dùng(ví dụ: theme=dark, language=en, pageSize=20)
private Map<String, String> preferences;

- So sánh String và StringBuilder  
+ String là + chuỗi còn StringBuilder là append nối vào cuối,ngoài ra còn có insert, delete, reverse
+ Dùng StringBuilder khi cần thay đổi nhiều, nó sửa luôn trên StringBuilder mà không cần tạo obj mới mỗi lần thao tác

- Stream là 1 luồng xử lý các phần tử của collection.Không thay đổi list gốc
+ Intermediate Operations (trung gian – lazy, chưa thực thi): filter,map(Biến đổi từng phần tử), sorted,distinct,limit,skip
+ Terminal Operations (cuối – kích hoạt stream): forEach, collect(Gom về dạng khácList,set,map), count,anyMatch,reduce(Gộp)
List<String> names = List.of("Alice", "Bob", "Alex");
names.stream() // Tạo stream
     .filter(s -> s.startsWith("A")) // Lọc
     .map(String::toUpperCase) // Chuyển đổi
     .forEach(System.out::println); // Hành động cuối cùng


- String Pool : String Pool (hay còn gọi là String Constant Pool) là một vùng bộ nhớ đặc biệt trong heap, nơi Java lưu trữ các chuỗi string literal để tái sử dụng và tiết kiệm bộ nhớ.
VD: String a = "hello";
    String b = "hello";
Thì "hello" là string literal, Chỉ tạo 1 object duy nhất trong pool, và cả a & b đều trỏ về cùng 1 object => a == b là true do `==` là sao sánh địa chỉ. Nhưng String c = new String("hello"); thì c lại khác a và b , khác địa chỉ

# 7. Algorithm
- Các loại thuật toán sắp xếp 
| Thuật toán         | So sánh trung bình | Tốt nhất   | Tệ nhất    | Ghi chú                                      |
| ------------------ | ------------------ | ---------- | ---------- | -------------------------------------------- |
| **Merge Sort**     | O(n log n)         | O(n log n) | O(n log n) | Dùng đệ quy, cần thêm bộ nhớ                 |
| **Quick Sort**     | O(n log n)         | O(n log n) | O(n²)      | Nhanh, thường dùng thực tế                   |
| **Heap Sort**      | O(n log n)         | O(n log n) | O(n log n) | Không ổn định, tốt khi cần không dùng đệ quy |
| **Counting Sort**  | O(n + k)           | O(n + k)   | O(n + k)   | Dùng được với số nguyên nhỏ, ổn định         |
| **Radix Sort**     | O(nk)              | O(nk)      | O(nk)      | Số nguyên nhiều chữ số, không so sánh        |
| **Bucket Sort**    | O(n + k)           |            |            | Giống Counting nhưng chia theo khoảng        |

Merge Sort: Ổn định, dữ liệu lớn
Quick Sort: Tốc độ nhanh, ko ổn định
Heap Sort: Giới hạn tài nguyên

Ổn định là các giá trị bằng nhau sau khi sắp xếp vẫn giữ thứ tự

- So sánh == vs .equals()
| So sánh     | So sánh gì?              | Dùng khi...                    |
| ----------- | ------------------------ | ------------------------------ |
| `==`        | So sánh địa chỉ (object) | Kiểm tra trỏ cùng object không |
| `.equals()` | So sánh nội dung         | So sánh nội dung chuỗi thực sự |


# 8. JS TS
Mỗi tab trong Chrome thường là một process riêng biệt (theo mô hình "multi-process architecture")
Trong mỗi process, có nhiều thread để xử lý các tác vụ khác nhau :
  Main thread: Thực thi mã JavaScript và thao tác DOM.
  Render thread: Xử lý việc render giao diện.
  Network thread: Xử lý các yêu cầu mạng.
  Timer thread: Quản lý các timer (ví dụ: setTimeout).
Đơn luồng trong ngữ cảnh của JavaScript không có nghĩa là trình duyệt chỉ có một thread duy nhất. 
Thay vào đó, nó có nghĩa là mã JavaScript chỉ chạy trên một luồng duy nhất , gọi là main thread .
Render thread hoạt động độc lập với main thread, nhưng nếu main thread bị chặn (blocked), render thread không thể cập nhật giao diện.
Yêu cầu mạng được chuyển sang network thread, nhưng callback (.then) vẫn được trả về main thread để thực thi.
Timer thread quản lý thời gian, nhưng khi timer hết giờ, callback được chuyển về main thread để thực thi.
Các thread phụ trợ (render, network, timer) chỉ thực hiện các tác vụ nền và không trực tiếp thực thi mã JavaScript.

Cơ chế Event Loop đảm bảo rằng các tác vụ bất đồng bộ (asynchronous tasks) (như setTimeout, Promise, Fetch) được thực thi đúng thời điểm trên main thread mà không cần đa luồng.

Cấu trúc của Event Loop
  Call Stack:Là nơi lưu trữ các hàm đang được thực thi. Khi một hàm được gọi, nó sẽ được đẩy vào call stack. 
    Khi hàm hoàn thành, nó sẽ được loại bỏ khỏi call stack.
  Web APIs:Là các API do trình duyệt cung cấp (ví dụ: setTimeout, DOM events).
  Callback Queue (Task Queue):Là hàng đợi lưu trữ các callback của các tác vụ bất đồng bộ từ Web APIs.
    Các callback trong Callback Queue sẽ được đẩy vào call stack khi call stack trống.
  Microtask Queue:Là hàng đợi ưu tiên cao hơn dành cho các microtasks (ví dụ: Promise, MutationObserver).
    Các microtasks trong Microtask Queue sẽ được thực thi trước khi các callback trong Callback Queue được xử lý.

Cách hoạt động của Event Loop :
 Bc 1 : Thực thi mã tuần tự: Các câu lệnh được đẩy vào call stack và thực thi tuần tự.
 Bc 2 : Xử lý bất đồng bộ: Khi gặp các tác vụ bất đồng bộ (ví dụ: setTimeout), chúng được chuyển sang Web APIs.
 Bc 3 : Chuyển callback vào queue, Khi tác vụ bất đồng bộ hoàn thành:
    Nếu là Promise, Async/Await, hoặc tự đưa 1 hàm vào với queueMicrotask(), callback được chuyển vào Microtask Queue .
    Nếu là setTimeout, interval, sự kiện DOM như click, scroll, keypress, đọc/ghi file, callback được chuyển vào Callback Queue .
 Bc 4 : Event Loop liên tục kiểm tra call stack. Nếu call stack trống:
    Xử lý tất cả các microtasks trong Microtask Queue .
    Sau đó, lấy callback từ Callback Queue và đẩy vào call stack để thực thi.

Thứ tự xử lý : call stack => Microtask Queue(Promise) => Callback Queue(setTimeout)

Đơn luồng nhằm tránh 
  Race condition: Khi hai hoặc nhiều luồng cố gắng truy cập vào cùng một tài nguyên (ví dụ: DOM) đồng thời.
  Deadlock: Khi hai luồng chờ nhau mãi mãi.

Ví dụ máy tính có CPU i7-8750H, có 6 nhân vật lý(Core), nhưng lại có 12 luồng logic(Logical processors) nhờ hyper-threading.
Hyper-Threading là công nghệ cho phép một nhân vật lý xử lý hai luồng logic (logical threads) .
1 Nhân chỉ có thể xử lý 1 luồng tại một thời điểm, 1 Nhân với Hyper-Threading có thể xử lý 2 luồng đồng thời
1 Nhân xử lý 1 process tại một thời điểm nếu process đó 1 luồng , nếu có nhiều luồng cần nhiều nhân xử lý



# 9. Mạng máy tính (Networking)
## 9.1 Mô hình mạng
- Mô hình OSI(Open Systems Interconnection) 7 tầng :
+ Physical Layer(Tầng Vật lý): Truyền dữ liệu qua cáp. 
VD: Cáp Ethernet,wifi
+ Data Link Layer(Tầng Liên kết Dữ liệu): Xử lý kết nối giữa các thiết bị trong cùng một mạng. 
VD: Router chuyển dữ liệu đến đúng thiết bị dựa trên địa chỉ MAC.
+ Network Layer(Tầng Mạng): Định tuyến dữ liệu giữa các mạng.
NAT (Network Address Translation) để chuyển đổi private IP thành public IP khi ra khỏi mạng LAN.
VD: Router sử dụng địa chỉ IP để gửi yêu cầu từ máy tính của bạn đến máy chủ của Google
+ Transport Layer(Tầng Vận chuyển): Đảm bảo dữ liệu được truyền an toàn.
TCP chia dữ liệu thành các gói nhỏ và đánh số thứ tự để truyền đi qua http. Bị mất gửi lại
+ Session Layer(Tầng Phiên): Quản lý phiên giao tiếp.
VD : Khi truy cập google.com, trình duyệt tạo một phiên giao tiếp với máy chủ của Google.
Phiên giao tiếp được duy trì cho đến khi bạn đóng trang web hoặc hoàn thành tác vụ.
+ Presentation Layer(Tầng Trình bày): Chuyển đổi dữ liệu sang định dạng phù hợp.
VD: Máy chủ của Google gửi dữ liệu trang web dưới dạng HTML, CSS, và JavaScript, hoặc dạng mã hoá bằng SSL/TLS
+ Application Layer(Tầng Ứng dụng): Tương tác với người dùng.
VD: Trình duyệt (ứng dụng) sử dụng giao thức HTTP/HTTPS để giao tiếp với máy chủ của Google
Máy chủ trả về nội dung trang web (HTML, CSS, JavaScript), và trình duyệt hiển thị nó.

VD: Trong ví dụ truy cập một website (google.com), mô hình OSI hoạt động như sau: Physical Layer truyền tín hiệu qua cáp/Wi-Fi, Data Link Layer sử dụng địa chỉ MAC, Network Layer định tuyến qua IP, Transport Layer đảm bảo truyền tin cậy qua TCP, Session Layer quản lý phiên giao tiếp, Presentation Layer mã hóa dữ liệu, và Application Layer tương tác với người dùng qua HTTP/HTTPS.

- Mô hình TCP/IP(Transmission Control Protocol/Internet Protocol) 4 tầng :
Network Interface Layer: Tương đương Physical và Data Link Layer.
Internet Layer: Tương đương Network Layer.
Transport Layer: Tương đương Transport Layer.
Application Layer: Tương đương Session, Presentation, và Application Layer.

- Các giao thức mạng phổ biến : 
+ IP (Internet Protocol)
IPv4: Địa chỉ IP 32-bit (ví dụ: 192.168.1.1).
IPv6: Địa chỉ IP 128-bit (ví dụ: 2001:0db8::1).
+ TCP và UDP 
TCP (Transmission Control Protocol): Đảm bảo dữ liệu được truyền đúng thứ tự và không lỗi.
UDP (User Datagram Protocol): Truyền dữ liệu nhanh nhưng không đảm bảo độ tin cậy.
+ HTTP và HTTPS
HTTP: Giao thức truyền tải dữ liệu web không mã hóa.
HTTPS: Giao thức truyền tải dữ liệu web có mã hóa (SSL/TLS).
+ DNS (Domain Name System) : Dịch tên miền thành địa chỉ IP.
Ví dụ: google.com → 142.250.191.100.

- Cổng 22 (SSH),cổng 80 (HTTP) , 443 (HTTPS), cổng 3306 (MySQL), 20/21 FTP (File Transfer Protocol),5432
(PostgreSQL),6379(Redis)

## 9.2 Hệ thống file
- Hệ thống file là một phương pháp tổ chức và quản lý dữ liệu trên ổ đĩa, quyết định cách dữ liệu được lưu trữ, truy xuất, cập nhật và xóa.
+ NTFS (New Technology File System) : Là hệ thống file mặc định của Windows
+ ext4 (Fourth Extended File System) : Là hệ thống file phổ biến nhất trên Linux.
+ FAT32 (File Allocation Table 32) : Là hệ thống file cũ, được sử dụng rộng rãi trên các thiết bị lưu trữ di động (USB, thẻ nhớ), file tối đa là 4GB .
+ APFS (Apple File System) : Là hệ thống file mới của Apple
Một số hệ thống file (ví dụ: FAT32, exFAT) được thiết kế để tương thích với nhiều hệ điều hành.
Các hệ thống file chuyên dụng (ví dụ: NTFS, ext4, APFS) thường chỉ hoạt động tốt trên hệ điều hành gốc.

## 9.3 Websocket
WebSocket là một giao thức mạng hai chiều (bi-directional), duy trì kết nối liên tục giữa client và server.
Luồng hoạt động WebSocket: Client gửi WebSocket handshake -> Server xác nhận ->Từ đó, 2 bên có thể gửi nhận dữ liệu liên tục.
Spring hỗ trợ WebSocket qua STOMP protocol + SockJS fallback (hữu ích cho frontend)
Kết nối từ nextjs với STOMP.JS + SOCKJS
Producer (gửi) → [Message Broker] → Consumer (nhận)

- Cách hoạt động của WebSocket:
+ Bước 1: Handshake 
Client gửi HTTP request đặc biệt để nâng cấp lên WebSocket
Server phản hồi , kết nối TCP chuyển sang giao thức WebSocket, và giữ mở liên tục.
| Loại                | Giao thức | Port |
| ------------------- | --------- | ---- |
| Không mã hoá        | `ws://`   | 80   |
| Có mã hoá (SSL/TLS) | `wss://`  | 443  |

+ Bước 2: Dùng STOMP:
WebSocket raw:
    Gửi nhận chuỗi/JSON thô
    Không có khái niệm "topic", "subscribe", "queue"
    Tự định nghĩa format tin nhắn, thiếu chuẩn hóa
STOMP (Simple Text Oriented Messaging Protocol) là một giao thức nhắn tin (messaging protocol) hoạt động qua WebSocket. Nó định nghĩa cách gửi nhận message, giống như HTTP của WebSocket.

Client kết nối WebSocket + STOMP
     |
     |-- CONNECT
     |-- SUBSCRIBE /topic/chatroom
     |-- SEND /app/send-message
     |
Spring Boot xử lý và gửi lại:
     |
     |-- SEND message về /topic/chatroom


# 10. Microservice
Chia mỗi module là 1 service riêng, có DB riêng, logic riêng.
| Khái niệm                      | Giải thích đơn giản                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------- |
| **Service Discovery** (Eureka) | Giống "danh bạ", giúp các service tìm nhau                                            |
| **Config Server**              | Chứa cấu hình tập trung (application.yml) cho toàn hệ thống                           |
| **API Gateway**                | Cổng vào duy nhất cho tất cả request từ frontend, nó sẽ **route** về các service đúng |
| **Load Balancer**              | Cân bằng tải giữa nhiều instance cùng 1 service                                       |
| **Circuit Breaker**            | Khi 1 service bị lỗi, tạm thời "ngắt" kết nối đến nó để tránh lỗi dây chuyền          |
| **Message Queue**              | Hàng đợi trung gian, giúp service giao tiếp gián tiếp với nhau                        |
| **Event-driven**               | Kiểu truyền dữ liệu bằng việc "bắn" sự kiện, ai cần thì bắt sự kiện xử lý             |
| **Database per service**       | Mỗi service có DB riêng, **không JOIN giữa 2 service như trong monolith**             |
| **GraphQL**                    | API nâng cao, giúp client lấy nhiều nguồn dữ liệu chỉ với 1 request                   |


- Câu hỏi phỏng vấn:
+ Ta lấy 1 bảng này trong 1 service này joint với bảng khác trong service khác ta làm kiểu gì, có những cách nào :
Gọi API để lấy dữ liệu từ service kia rồi tự JOIN ở tầng code, Dùng batch API hoặc search service (aggregate service)
Dùng async communication (Message Queue, Kafka) để đồng bộ dữ liệu :
    UserService khi có thay đổi user (create/update), publish message (Kafka, RabbitMQ).
    OrderService subscribe các event này và cập nhật bản sao (user_snapshot) trong DB của mình.
Dùng GraphQL (API Aggregator Gateway) Cài thư viện của META, GraphQL từ client chỉ định cần những gì -> đi qua backend API Aggregator (hoặc API Gateway) xử lý đúng truy vấn.

# 11. JWT (JSON Web Token)
- JWT (JSON Web Token) là một chuẩn mở để truyền thông tin giữa các bên dưới dạng một object JSON nhỏ gọn, an toàn, có thể xác thực được. Dạng Stateless.
JWT gồm 3 phần: Header, Payload, Signature.
  Header: Thông tin về thuật toán ký (ví dụ: HS256)
  Payload: Dữ liệu (ví dụ: email, userId, role, thời gian hết hạn)
  Signature: Chữ ký số, xác thực token không bị sửa đổi
JWT thường được dùng làm Access Token hoặc Refresh Token. Khi Refresh Token thì phải đăng nhập lại.

- Phân biệt StateFull và StateLess:
+ Session truyền thống lưu trạng thái đăng nhập trong RAM/Redis/DB, Token chứa Session ID (random), Xác thực Dựa trên session ID tra ngược về user, Khả năng mở rộng (scale) khó, Tốc độ chậm do cần truy vấn, Bảo mật Cần CSRF protection.
+ JWT (JSON Web Token) Stateless – Server không lưu gì cả,Token chứa Payload chứa luôn user info + claims, Xác thực Dựa trên giải mã JWT + verify chữ ký, Scale dễ dàng, Tốc độ nhanh do chỉ cần verify chữ ký token

- Nơi lưu Access Token & Refresh Token:
+ Access Token: FrontEnd lưu trong Cookie, localStorage hoặc memory, BackEnd không lưu 
+ Refresh Token: FrontEnd lưu trong HttpOnly Cookie, BackEnd lưu trong DB hoặc Redis. Ràng buộc với user, device, IP nếu cần.
| Loại Token        | Dùng để                             | Thời gian sống     | Lưu ở đâu?                        |
| ----------------- | ----------------------------------- | ------------------ | --------------------------------- |
| **Access Token**  | Gửi kèm mỗi request để truy cập API | Ngắn (5-15 phút)   | Client (localStorage)             |
| **Refresh Token** | Dùng để lấy access token mới        | Dài hơn (1-7 ngày) | HttpOnly cookie                   |

- Logout khi dùng JWT:
Đặt version_token +1 

+ Làm sao để BackEnd cho logout hết user dưới Client ? Tất nhiên vẫn cần xoá Refresh Token
Ta tạo thêm trường tokenVersion hoặc lastLogout(Kiểu timestamp) lưu vào user và access token, khi muốn logout ta tăng tokenVersion lên 1 là được, khi đăng nhập đều cần kiểm tra version token trong token với trong db.

| Loại token        | Tần suất sử dụng                      | Lưu ở đâu?                      | Gửi như nào?                                               |
| ----------------- | ------------------------------------- | ------------------------------- | ---------------------------------------------------------- |
| **Access Token**  | Gửi trong **mỗi request API**         | RAM (hoặc localStorage nếu cần) | Gửi thủ công bằng `Authorization: Bearer xxx`              |
| **Refresh Token** | Chỉ dùng khi **access token hết hạn** | HttpOnly cookie                 | Gửi tự động khi gọi `/auth/refresh` (nếu cookie đúng path) |

Cách dùng chuẩn hiện nay:
| Hoạt động     | Token liên quan | Cách gửi                                             |
| ------------- | --------------- | ---------------------------------------------------- |
| Gọi API       | Access Token    | Gửi thủ công bằng header                             |
| Làm mới token | Refresh Token   | Trình duyệt **tự gửi cookie** nếu path hợp lệ        |
| Logout        | Refresh Token   | Gọi API để xoá cookie hoặc refresh token trên server |


# 12. Câu hỏi phỏng vấn
- Mã trả về
| Mã                         | Ý nghĩa                                   | Khi nào dùng                            |
| -------------------------- | ----------------------------------------- | --------------------------------------- |
| `400 Bad Request`          | Dữ liệu gửi lên sai format                | Form không đúng, thiếu trường, JSON lỗi |
| `401 Unauthorized`         | Chưa xác thực (token không có / sai)      | Dùng cho login, token JWT               |
| `403 Forbidden`            | Đã xác thực nhưng **không có quyền**      | Ví dụ: user thường gọi admin API        |
| `404 Not Found`            | Không tìm thấy tài nguyên                 | API sai đường dẫn                       |

- Tổng hợp các nơi client-side có thể lưu dữ liệu
1. Cookie
Lưu key-value dạng text (đơn giản)
Tự động được gửi lên server theo domain/path mỗi lần gọi request

Có thể được đánh dấu:
HttpOnly → không bị truy cập bởi JavaScript
Secure → chỉ truyền qua HTTPS
SameSite=Strict/Lax/None → chống CSRF

🗃️ 2. localStorage
Lưu trữ key-value dạng string
Không bị xoá sau khi đóng tab, reload hoặc tắt máy
Không được gửi lên server
Có thể đọc/ghi dễ dàng bằng JavaScript


🧾 3. sessionStorage
Giống localStorage, nhưng chỉ tồn tại trong 1 tab
Bị mất khi bạn đóng tab hoặc reload bằng window.open()

🧠 4. Memory (RAM JS)
Lưu biến trong bộ nhớ của JavaScript trong runtime
let accessToken = null;

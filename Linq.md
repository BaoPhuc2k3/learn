# LINQ C# - Tổng hợp và Ví dụ

## 1. Filtering (`Where`)
```csharp
var
```

## 2. Projection (`Select`)
```csharp
var productNames = context.Products
                          .Select(p => new { p.Id, p.Name })
                          .ToList();
```

## 3. Sorting (`OrderBy`, `OrderByDescending`, `ThenBy`)
```csharp
var sortedProducts = context.Products
                            .OrderBy(p => p.CategoryId)
                            .ThenByDescending(p => p.Price)
                            .ToList();
```

## 4. Grouping (`GroupBy`)
```csharp
var groupedProducts = context.Products
                             .GroupBy(p => p.CategoryId)
                             .Select(g => new 
                             { 
                                 CategoryId = g.Key, 
                                 Count = g.Count(), 
                                 AvgPrice = g.Average(p => p.Price) 
                             })
                             .ToList();
```

## 5. Joins trong LINQ

### Inner Join
```csharp
var productsWithCategory = context.Products
                                  .Join(context.Categories,
                                        p => p.CategoryId,
                                        c => c.Id,
                                        (p, c) => new { p.Name, CategoryName = c.Name })
                                  .ToList();
```

### Left Outer Join (GroupJoin)
```csharp
var categoriesWithProducts = context.Categories
                                    .GroupJoin(context.Products,
                                               c => c.Id,
                                               p => p.CategoryId,
                                               (c, products) => new { c.Name, Products = products })
                                    .ToList();

// Flatten ra danh sách
var flattened = context.Categories
                       .GroupJoin(context.Products,
                                  c => c.Id,
                                  p => p.CategoryId,
                                  (c, products) => new { c.Name, Products = products })
                       .SelectMany(cp => cp.Products.DefaultIfEmpty(),
                                   (cp, p) => new { CategoryName = cp.Name, ProductName = p != null ? p.Name : null })
                       .ToList();
```

### Cross Join
```csharp
var crossJoin = from c in context.Categories
                from p in context.Products
                select new { c.Name, p.Name };
```

### Query syntax vs Method syntax
```csharp
// Query syntax
var query = from p in context.Products
            join c in context.Categories on p.CategoryId equals c.Id
            select new { p.Name, c.Name };

// Method syntax
var query2 = context.Products
                    .Join(context.Categories,
                          p => p.CategoryId,
                          c => c.Id,
                          (p, c) => new { p.Name, c.Name });
```

## 6. Quantifiers (`Any`, `All`)
```csharp
bool hasInStock = context.Products.Any(p => p.Stock > 0);
bool allValidPrice = context.Products.All(p => p.Price >= 0);
```

## 7. Element Operators (`First`, `FirstOrDefault`, `Single`, `SingleOrDefault`)
```csharp
var firstExpensive = context.Products.First(p => p.Price > 100);
var product = context.Products.SingleOrDefault(p => p.Id == 10);
```

## 8. Paging (`Skip`, `Take`)
```csharp
int pageNumber = 3;
int pageSize = 10;
var pagedProducts = context.Products
                           .OrderBy(p => p.Id)
                           .Skip((pageNumber - 1) * pageSize)
                           .Take(pageSize)
                           .ToList();
```

## 9. Aggregate (`Count`, `Sum`, `Average`, `Min`, `Max`)
```csharp
int stockCount = context.Products.Count(p => p.Stock > 0);
decimal totalPrice = context.Products.Sum(p => p.Price);
decimal avgPrice = context.Products.Average(p => p.Price);
decimal minPrice = context.Products.Min(p => p.Price);
decimal maxPrice = context.Products.Max(p => p.Price);
```

## 10. Set Operators (`Distinct`, `Contains`)
```csharp
var distinctCategories = context.Products // distinct : lấy giá trị duy nhất
                                .Select(p => p.CategoryId)
                                .Distinct()
                                .ToList();

var categoryIds = new List<int> { 1, 2, 3 };
var productsInCategories = context.Products
                                  .Where(p => categoryIds.Contains(p.CategoryId))
                                  .ToList();
```

## 11. EF-specific (`AsNoTracking`, `Include`)
```csharp
var orders = context.Orders
                    .AsNoTracking() // tắt trạng thái theo dõi của EF , chỉ đọc 
                    .Include(o => o.OrderItems) // lấy thêm dữ liệu liên quan
                    .ToList();
```

## 12. Combination Example
```csharp
var topProducts = context.Products
                         .Where(p => p.CategoryId == 2)
                         .OrderByDescending(p => p.Price)
                         .Take(5)
                         .Select(p => new { p.Id, p.Name })
                         .AsNoTracking()
                         .ToList();
```

---

## Lưu ý chung:
1. **Deferred Execution:** query chưa thực thi ngay, chỉ khi enumerate.  -->   tolist() để chạy
2. **IQueryable vs IEnumerable:** `IQueryable` → translate SQL, `IEnumerable` → thao tác in-memory.
3. **Projection + AsNoTracking:** tối ưu performance khi read-only.
4. **Paging:** luôn OrderBy trước Skip.
5. **Element Operators:** chọn đúng `First`, `Single` để tránh exception.
6. **Aggregate Operators:** EF translate trực tiếp sang SQL, không load toàn bộ entity.
7. **Joins trong LINQ:** có Inner Join (`Join`), Left Join (`GroupJoin + SelectMany + DefaultIfEmpty`) và Cross Join (`from ... from ... select`).

var query = context.Products
                // Lọc các sản phẩm có giá > 100
                .Where(p => p.Price > 100)
                
                // Lấy các trường cần thiết
                .Select(p => new {
                    p.ProductId,
                    p.ProductName,
                    p.Category,
                    p.Price,
                    p.Quantity
                })
                
                // Sắp xếp theo giá tăng dần
                .OrderBy(p => p.Price)
                
                // Gom nhóm theo Category
                .GroupBy(p => p.Category)
                
                // Lấy các nhóm và tính tổng Quantity trong từng nhóm
                .Select(g => new {
                    Category = g.Key,
                    TotalQuantity = g.Sum(p => p.Quantity),
                    ProductCount = g.Count()
                })
                
                .ToList();



# Từ khoá
I. Filtering (Lọc dữ liệu)
| Từ khóa       | Mô tả                      | Ví dụ                      |
| ------------- | -------------------------- | -------------------------- |
| `Where()`     | Lọc phần tử theo điều kiện | `nums.Where(x => x > 10)`  |
| `OfType<T>()` | Lọc theo kiểu dữ liệu      | `objects.OfType<string>()` |
Where tương đương SELECT * FROM ... WHERE ... trong SQL.

II. Projection (Biến đổi dữ liệu)
| Từ khóa        | Mô tả                                            | Ví dụ                             |
| -------------- | ------------------------------------------------ | --------------------------------- |
| `Select()`     | Chọn trường cần lấy, chuyển dạng dữ liệu         | `products.Select(p => p.Name)`    |
| `SelectMany()` | Dùng khi phần tử chứa tập hợp con (flatten list) | `orders.SelectMany(o => o.Items)` |
SelectMany dùng cho 1-n, ví dụ: User có nhiều Order.

III. Sorting (Sắp xếp)
| Từ khóa               | Mô tả                     | Ví dụ                                                       |
| --------------------- | ------------------------- | ----------------------------------------------------------- |
| `OrderBy()`           | Sắp xếp tăng dần          | `users.OrderBy(u => u.Name)`                                |
| `OrderByDescending()` | Sắp xếp giảm dần          | `users.OrderByDescending(u => u.Age)`                       |
| `ThenBy()`            | Sắp xếp phụ (thứ 2)       | `users.OrderBy(u => u.Age).ThenBy(u => u.Name)`             |
| `ThenByDescending()`  | Sắp xếp phụ giảm dần      | `users.OrderBy(u => u.Age).ThenByDescending(u => u.Salary)` |
| `Reverse()`           | Đảo ngược thứ tự hiện tại | `nums.Reverse()`                                            |
ThenBy chỉ dùng được sau khi có OrderBy.

IV. Grouping (Nhóm dữ liệu)
| Từ khóa     | Mô tả                | Ví dụ                            |
| ----------- | -------------------- | -------------------------------- |
| `GroupBy()` | Gom nhóm theo trường | `students.GroupBy(s => s.Class)` |
Trả về IGrouping<TKey, TElement>. Muốn duyệt phải dùng vòng lặp lồng:
foreach (var group in groups)
{
    Console.WriteLine(group.Key);
    foreach (var item in group)
        Console.WriteLine(item.Name);
}

V. Joining (Kết hợp dữ liệu)
| Từ khóa       | Mô tả                     | Ví dụ                                                                                               |
| ------------- | ------------------------- | --------------------------------------------------------------------------------------------------- |
| `Join()`      | Inner join giữa 2 tập hợp | `customers.Join(orders, c => c.Id, o => o.CustomerId, (c, o) => new { c.Name, o.Total })`           |
| `GroupJoin()` | Join 1-n (nhóm bên phải)  | `customers.GroupJoin(orders, c => c.Id, o => o.CustomerId, (c, os) => new { c.Name, Orders = os })` |
| `Zip()`       | Ghép 2 tập hợp song song  | `nums.Zip(words, (n, w) => w + n)`                                                                  |
| `Concat()`    | Nối 2 tập hợp             | `list1.Concat(list2)`                                                                               |
| `Union()`     | Gộp và loại trùng         | `list1.Union(list2)`                                                                                |
| `Intersect()` | Giao (chung)              | `list1.Intersect(list2)`                                                                            |
| `Except()`    | Trừ (A trừ B)             | `list1.Except(list2)`                                                                               |

Join ~ INNER JOIN
GroupJoin ~ LEFT JOIN (mô phỏng)
Union ~ UNION DISTINCT trong SQL

VI. Aggregation (Tổng hợp)
| Từ khóa       | Mô tả             | Ví dụ                             |
| ------------- | ----------------- | --------------------------------- |
| `Count()`     | Đếm số phần tử    | `nums.Count()`                    |
| `Sum()`       | Tổng              | `nums.Sum()`                      |
| `Average()`   | Trung bình        | `nums.Average()`                  |
| `Min()`       | Giá trị nhỏ nhất  | `nums.Min()`                      |
| `Max()`       | Giá trị lớn nhất  | `nums.Max()`                      |
| `Aggregate()` | Tổng hợp tùy biến | `nums.Aggregate((a, b) => a + b)` |
Aggregate là tổng quát nhất — có thể dùng để nhân, cộng, nối chuỗi...

VII. Quantifiers (Kiểm tra tồn tại / toàn bộ)
| Từ khóa      | Mô tả                                  | Ví dụ                   |
| ------------ | -------------------------------------- | ----------------------- |
| `Any()`      | Kiểm tra có phần tử nào thoả điều kiện | `nums.Any(n => n > 10)` |
| `All()`      | Tất cả phần tử đều thoả                | `nums.All(n => n > 0)`  |
| `Contains()` | Kiểm tra có tồn tại giá trị            | `nums.Contains(5)`      |

VIII. Element Operators (Lấy phần tử)
| Từ khóa                     | Mô tả                                | Ví dụ                                  |
| --------------------------- | ------------------------------------ | -------------------------------------- |
| `First()`                   | Lấy phần tử đầu tiên                 | `list.First()`                         |
| `FirstOrDefault()`          | Như trên, nhưng null-safe            | `list.FirstOrDefault()`                |
| `Last()`                    | Lấy phần tử cuối                     | `list.Last()`                          |
| `LastOrDefault()`           | Null-safe                            | `list.LastOrDefault()`                 |
| `Single()`                  | Phải có đúng 1 phần tử               | `list.Single(x => x.Id == 1)`          |
| `SingleOrDefault()`         | Cho phép rỗng                        | `list.SingleOrDefault(x => x.Id == 1)` |
| `ElementAt(index)`          | Lấy phần tử theo vị trí              | `list.ElementAt(2)`                    |
| `ElementAtOrDefault(index)` | Null-safe                            | `list.ElementAtOrDefault(10)`          |
| `DefaultIfEmpty()`          | Nếu rỗng thì trả về giá trị mặc định | `list.DefaultIfEmpty(0)`               |

IX. Set Operators (Tập hợp)
| Từ khóa       | Mô tả            | Ví dụ             |
| ------------- | ---------------- | ----------------- |
| `Distinct()`  | Loại trùng lặp   | `nums.Distinct()` |
| `Union()`     | Hợp (loại trùng) | `a.Union(b)`      |
| `Intersect()` | Giao             | `a.Intersect(b)`  |
| `Except()`    | Hiệu             | `a.Except(b)`     |

X. Partitioning (Phân trang, lấy 1 phần)
| Từ khóa           | Mô tả                         | Ví dụ                         |
| ----------------- | ----------------------------- | ----------------------------- |
| `Take(n)`         | Lấy n phần tử đầu             | `nums.Take(5)`                |
| `Skip(n)`         | Bỏ n phần tử đầu              | `nums.Skip(5)`                |
| `TakeWhile(cond)` | Lấy cho đến khi sai điều kiện | `nums.TakeWhile(x => x < 10)` |
| `SkipWhile(cond)` | Bỏ cho đến khi sai điều kiện  | `nums.SkipWhile(x => x < 10)` |

XI. Conversion (Chuyển đổi kiểu dữ liệu)
| Từ khóa          | Mô tả                | Ví dụ                                       |
| ---------------- | -------------------- | ------------------------------------------- |
| `ToList()`       | Chuyển thành List    | `query.ToList()`                            |
| `ToArray()`      | Thành mảng           | `query.ToArray()`                           |
| `ToDictionary()` | Thành dictionary     | `list.ToDictionary(x => x.Id, x => x.Name)` |
| `Cast<T>()`      | Ép kiểu từng phần tử | `list.Cast<string>()`                       |
| `AsEnumerable()` | Ép về IEnumerable    | `query.AsEnumerable()`                      |
| `AsQueryable()`  | Ép về IQueryable     | `list.AsQueryable()`                        |

- So sánh Select và SelectMany
+ Select: var result = classes.Select(c => c.Students);
[
  [An, Bình],
  [Cường, Dũng]
]
+ SelectMany: var result = classes.SelectMany(c => c.Students);
[An, Bình, Cường, Dũng]

- SelectMany có project ra dữ liệu mới, giống join
var result = classes.SelectMany(
    c => c.Students,
    (c, s) => new { ClassName = c.ClassName, StudentName = s.Name }
);

- OrderBy và ThenBy đều có Descending - Sắp xếp nhiều cấp
var result = people
    .OrderByDescending(p => p.LastName)
    .ThenByDescending(p => p.FirstName);

Trước hết sắp theo LastName (Adams → Smith),
Trong cùng một họ (Smith), lại sắp theo FirstName.

- union, Intersect(Chung 2 tập), Except(Chỉ có ở A không có ở B) đều có vấn đề so sánh bằng == là so sánh qua địa chỉ bộ nhớ nên cần cấu hình lại nếu dùng biến tham chiếu obj,class,...
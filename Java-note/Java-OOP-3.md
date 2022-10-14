# Lập trình hướng đối tượng Java (3)

# Class trừu tượng (Abstract Class) và Phương thức trừu tượng (Abstract Method)
## Class trừu tượng
Là một class không thể khởi tạo, có nghĩa là ta không thể tạo đối tượng từ class trừu tượng. Sử dụng từ khóa `abstract` để định nghĩa

```
// Cú pháp Class trừu tượng
abstract class DongVat {
    // Thuộc tính
    // Phương thức
}
```
Do vậy nếu cố gắng khởi tạo đối tượng từ class trừu tượng này sẽ xảy ra lỗi `... is abstract; cannot be instantiated`

Tuy nhiên có thể tạo class con từ nó bằng cách tạo ra các đối tượng class con và sử dụng nó để truy cập vào các thành viên của class trừu tượng

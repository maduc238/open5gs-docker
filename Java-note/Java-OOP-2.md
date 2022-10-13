# Lập trình hướng đối tượng Java (2)

# Sử dụng biểu thức Lambda trong Java
Tính năng mới được giới thiệu trong Java 8, đó là hỗ trợ cho biểu thức **lambda** sử dụng **functional interface**
## Functional Interface là gì?
Nếu một **Java Interface** có một và chỉ một phương thức trừu tượng thì nó được gọi là **Functional Interface**

Ví dụ ``Runnable`` interface từ package `java.lang` là một **functional interface** vì chỉ có một phương thức là `run()`

Ví dụ định nghĩa một Functional Interface trong Java:
```
import java.lang.FunctionalInterface;
    @FunctionalInterface
    public interface MyInterface{
        double getValue();
}
```

## Cách định nghĩa Lambda trong Java

Biểu thức lambda là gì? Về cơ bản, biểu thức lambda là một phương thức vô danh / không có tên, không tự thực thi. Thay vào đó, nó được dùng để triển khai một phương thức xác định bởi một Functional Interface

Biểu thức lambda giới thiệu một cú pháp và toán tử mới trong ngôn ngữ Java: **lambda operator** và **arrow operator** `(->)`

Thông thường chúng ta viết phương thức đơn giản trả về một hằng số như sau:

```
double getPiValue() ( return 3.1415; }
```

Cách viết tương đương khi sử dụng lambda như sau:
```
()->3.1415
```
- Bên trái biểu thức chỉ định bất kỳ tham số khi nào cần thiết
- Bên phải là phần thân, chỉ định hành động của biểu thức lambda

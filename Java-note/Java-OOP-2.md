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

Một vài ví dụ về lambda:
```
() -> System.out.println("Phần Lambda trong bài Tự học Lập trình Java");
```
```
() -> {
    double pi = 3.1415;
    return pi;
}
```

Tạo một file có tên là `IMyInterface.java`
```
// Đây là một Functional Interface
@FunctionalInterface
public interface IMyInterface{
 
    double getPiValue();
}
```
Chữ **I** ở đầu tên **I**MyInteface là quy tắc đặt tên phổ biến cho Interface

Bây giờ gán biểu thức lamda đến thể hiện của Functional Interface

```
public class LambdaMain {
 
    public static void main( String[] args ) {
 
        IMyInterface myInterface;
        myInterface = () -> 3.1415;
 
        System.out.println("Giá trị của Pi = " + myInterface.getPiValue());
    }
}
```

Khi chạy chương trình kết quả nhận được là:
```
Giá trị của Pi = 3.1415
```
Ví dụ khác
```
// Ví dụ Biểu thức Lambda có tham số
@FunctionalInterface
interface IMyInterface {
 
    String reverse(String n);
}
 
public class ParamLambdaMain {
 
    public static void main( String[] args ) {
 
        IMyInterface myInterface = (str) -> {
 
            String result = "";
            for (int i = str.length() - 1; i >= 0 ; i--)
                result += str.charAt(i);
                return result;
        };
 
    System.out.println("Đảo ngược Lambda = " + myInterface.reverse("Lambda"));
    }
 
}
```
Kết quả nhận được:
```
Đảo ngược Lambda = adbmaL
```

## Generic Functional Interface
Có thể tạo Functional Interface chung, để bất kỳ loại dữ liệu nào cũng được chấp nhận
```
// IGenericInterface.java
@FunctionalInterface
interface IGenericInterface<T> {
 
    T func(T t);
}
```

## Biểu thức Lambda và Stream API
Package `java.util.stream` cho phép thực hiện các hoạt động như search, filter, map, reduce hoặc thao tác với các tập hợp như List

Ví dụ có một luồng dữ liệu (giả sử một List các String) là sự kết hợp của tên quốc gia và thành phố

```
// Ví dụ Sử dụng Stream API và Biểu thức Lambda
import java.util.ArrayList;
import java.util.List;
 
public class StreamMain {
 
    static List<String> city = new ArrayList<>();
 
    // Chuẩn bị dữ liệu
    public static List getCity(){
 
        city.add("Vietnam, Hanoi");
        city.add("Vietnam, HCM");
        city.add("Japan, Kyoto");
        city.add("Japan, Tokyo");
        city.add("USA, New York");
 
        return city;
    }
 
    public static void main( String[] args ) {
 
        List<String> myCity = getCity();
        System.out.println("Thành phố của Việt Nam:");
 
        // Lọc thành phố từ Vietnam
        myCity.stream()
            .filter((c) -> c.startsWith("Vietnam"))
            .map((c) -> c.toUpperCase())
            .sorted()
            .forEach((c) -> System.out.println(c));
    }
}
```
Khi chạy chương trình, kết quả nhận được:
```
Thành phố của Việt Nam:
Vietnam, Hanoi
Vietnam, HCM
```

# Java Instanceof
https://niithanoi.edu.vn/lap-trinh-java.html#chuong-iv-phan-8-java-instanceof

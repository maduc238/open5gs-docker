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

# Kế thừa trong Java
## Từ khóa extends
Ví dụ về kế thừa trong Java. Sử dụng `extends` để kế thừa class mẹ

```
class DongVat {
 
    public void an() {
        System.out.println("Đang ăn...");
    }
 
    public void ngu() {
        System.out.println("Đang ngủ...");
    }
}
 
class Cho extends DongVat {
    public void sua() {
        System.out.println("Gâu gâu gâu");
    }
}
 
class Main {
    public static void main(String[] args) {
 
        Cho cauVang = new Cho();
 
        cauVang.an();
        cauVang.ngu();
 
        cauVang.sua();
    }
}
```
Khi chạy chương trình, kết quả nhận được:
```
Đang ăn...
Đang ngủ...
Gâu gâu gâu
```
Ngoài ra còn các từ khóa protected sử dụng trong kế thừa như: `public`, `private`, `protected` dùng cho các phương thức

## Phương thức Overriding

Sử dụng phương thức này để định nghĩa cho class mẹ từ class con

Ví dụ về phương thức trong class con sẽ ghi đè phương thức trong class mẹ

```
// Ví dụ Overloading trong Java
class DongVat {
    protected String giong = "Động vật";
 
    public void an() {
        System.out.println("Đang ăn...");
}
 
    public void ngu() {
        System.out.println("Đang ngủ...");
    }
}
 
class Cho extends DongVat {
 
    @Override
    public void an() {
        System.out.println("Đang ăn cơm...");
    }
 
    public void sua() {
        System.out.println("Gâu gâu gâu");
    }
}
 
class Main {
    public static void main(String[] args) {
 
        Cho cauVang = new Cho();
        cauVang.an();
        cauVang.ngu();
        cauVang.sua();
    }
}
```
Tuy nhiên trong code trên sử dụng `@Override` để báo cho trình biên dịch rằng chúng ta ghi đè lên một phương thức. Nó không bắt buộc nhưng khuyến khích sử dụng để tăng khả năng đọc của chương trình

# Java Instanceof
Từ khóa `instanceof` là một toán tử nhị phân. Nó được dùng để kiểm tra xem một một đối tượng có phải là một thể hiện của một class cụ thể hay không

Cú pháp:
```
result = objectName instanceof className;
```
Trong đó:
- `objectName` là tên đối tượng
- `className` là tên class
- `result` là kết quả trả về, `true` nếu đối tượng là thể hiện của class, `false` nếu ngược lại

```
// Ví dụ đơn giản toán tử instanceof
class Main {
    public static void main (String[] args) {
        String ten = "NIITHANOI.EDU.VN";
        Integer tuoi = 17;
        ​
        System.out.println("ten là thể hiện của String: "+ (ten instanceof String));
        System.out.println("tuoi là thể hiện của Integer: "+ (tuoi instanceof Integer));
    }
}
```
Khi chạy chương trình, kết quả nhận được:
```
ten là thể hiện của String: true
tuoi là thể hiện của Integer: true
```

## Sử dụng toán tử instanceof trong kế thừa
Trong trường hợp kết thừa, `instanceof` được sử dụng để kiểm tra xem một đối tượng của lớp con có phải là thể hiện của lớp mẹ hay không

```
// Ví dụ sử dụng instanceof trong kế thừa
class DongVat {
}
 
class Cho extends DongVat {
}
 
class Main {
    public static void main(String[] args){
        Cho cho = new Cho();
 
        System.out.println("cho là thể hiện của Cho: "+ (cho instanceof Cho));
        System.out.println("cho là thể hiện của DongVat: "+ (cho instanceof DongVat));
    }
}
```
Khi chạy chương trình:
```
cho là thể hiện của Cho: true
cho là thể hiện của DongVat: true
```

## Class Object
Tất cả các class được kế thừa từ class `Object`. Trong quá trình thực hiện, chúng ta không cần từ khóa `extends` như kế thừa trước đó vì đây là một ngoại lệ trong Java.

Điều này do class `Object` là class root được định nghĩa trong package `java.lang`. Tất cả các class con của class `Object` tại thành một hệ thống phân cấp trong Java

## Object Upcasting và Downcasting trong Java
Một đối tượng của class con có thể được coi là một đối tượng của class mẹ. Điều này gọi là **upcasting**

```
// Ví dụ upcasting trong Java
class DongVat {
    public void hienThiThongTin() {
        System.out.println("Tôi là động vật.");
    }
}

class Cho extends DongVat {
}

class Main {
    public static void main(String[] args) {
        Cho cho = new Cho();
        DongVat dv = cho;
        dv.hienThiThongTin();
    }
}
```
Khi chạy chương trình:
```
Tôi là động vật.
```
**Downcasting** thì ngược lại, cú pháp phải thêm `instanceof`
```
// Ví dụ sửa lỗi Downcasting bằng instanceof
class DongVat {
}
​
class Meo extends DongVat {
    public void hienThiThongTin() {
        System.out.println("Tôi là một con mèo.");
    }
}
​
class Main {
    public static void main(String[] args) {
        Meo meo1 = new Meo();
        DongVat dv = meo1;    // Upcasting
        ​
        if (dv instanceof Meo){
            Meo meo2 = (Meo)dv;    // Downcasting
            meo2.hienThiThongTin();
        }
    }
}
```
Khi chạy chương trình:
```
Tôi là một con mèo.
```

# Lập trình hướng đối tượng Java
Object Oriented Programming

Class là một bản kế hoạch chi tiết cho đối tượng

## Cách định nghĩa class trong Java

```
class TenClass{
    // Biến
    // Phương thức
}
```

Còn đây là một ví dụ về class mô tả về đèn

```
class Den{
    private String denSang;

    public void batDen(){
        denSang = "Đèn đang sáng";
    }

    public void tatDen(){
        denSang = "Đèn đang tắt";
    }
}
```

Ở đây chúng ta định nghĩa:
- Một class tên là `Den`
- Một biến thể hiện là `denSang`, có kiểu dữ liệu `String`
- Hai phương thức biểu diễn bằng hàm là `batDen()` và `tatDen()`

Lưu ý: Có từ khóa `private` và `public`. Đây chỉ tới mức độ truy cập
- `private` làm cho biến thể hiện và phương thức chỉ có thể truy cập được từ bên trong cùng class
- `public` làm cho biến thể hiện và phương thức có thể truy cập từ bên ngoài class

## Cách tạo Object trong Java

Khi class được định nghĩa, chỉ có đặc tả của đối tượng được xác định. Bộ nhớ chưa được phân bổ. -> Để truy cập bộ nhớ các thành viên bên trong class, cần tạo các đối tượng

```
Den den1 = new Den();
Den den2 = new Den();
```

## Cách truy cập thành viên trong Java

Ví dụ để truy cập phương thức `batDen()` trong class `Den`:

```
den1.batDen();
```

## Ví dụ về Class và Object trong Java

```
class Den {
    
    // Biến thể hiện (instance variable)
    private String denSang;

    // Phương thức bật đèn
    public void batDen(){
        denSang = "Đèn đang sáng";
    }

    // Phương thức tắt đèn
    public void tatDen() {
        denSang = "Đèn đang tắt";
    }

    public void thongBao() {
        System.out.println("Thông báo: " + denSang);
    }
}
class TaoDoiTuongDen {
    public static void main(String[] args) {

        // Tạo đối tượng den1 từ class Den
        Den den = new Den();

        // Bật đèn
        den.batDen();
        // Thông báo trạng thái của đèn
        den.thongBao();

        // Tắt đèn
        den.tatDen();
        // Thông báo trạng thái của đèn
        den.thongBao();

    }
}
```

# Phương thức trong Java
## Phương thức là gì?

Ví dụ trong toán học, một hàm trả về bình phương của x: f(x) = x^2
- Nếu x = 2 thì f(2) = 4
- Nếu x = 3 thì f(3) = 9
- ...

Tương tự trong việc lập trình, một hàm là một khối code thực hiện một nhiệm vụ cụ thể. Trong OOP, một hàm được gọi với tên gọi khác là **Phương thức** để gần gũi hơn với ý nghĩa hướng đối tượng hơn

**Phương thức** trong tiếng anh là **method**

Các method này được liên kết với một class, và nó định nghĩa hành vi của class đó

## Các kiểu phương thức
Chia làm 2 loại phương thức:
- Standard Library Methods
- User-defined Methods

## Phương thức trong thư viện chuẩn
Các phương thức kiểu Standard Library Methods là các phương thức được dựng sẵn trong Java (Build-in Functions) và có thể sử dụng chúng ngay

Các thư viện chuẩn này đi kèm với thư viện Java Class (JCL) trong tệp lưu trữ Java `(*.jar)` với JVM và JRE

Ví dụ:
- print() là phương thức trong java.io.PrintSteam
- sqrt() là phương thức trong class Math

```
public class ViDuSqrtMethod {
    public static void main(String[] args) {
        System.out.print("Căn bậc 2 của 4 là: " + Math.sqrt(4));
    }
}
```

## Phương thức tự định nghĩa trong Java
Có thể tự định nghĩa phương thức bên trong một class theo mong muốn của mình. Chúng được gọi là User-defined methods

Ví dụ một phương thức tự định nghĩa:
```
public static void myMethod() {
    System.out.println("Phương thức myMethod được gọi");
}
```

Có thể thấy:
- Từ khóa `public` cho phép truy cập phương thức **từ bên ngoài**
- Từ khóa `static` cho phếp truy cập phương thức mà **không cần tạo đối tượng**
- Từ khóa `void` biểu thị phương thức này không trả về bất kỳ giá trị nào

Cú pháp đầy đủ để định nghĩa một phương thức trong Java là:
```

modifier static returnType nameOfMethod (Parameter List) {
    // method body
}
```

Trong đó:
- **modifier** xác định mức độ truy cập như `public`, `private` và `protected`
- **static** nếu sử dụng nó thì phương thức có thể được truy cập mà không cần tạo đối tượng
- **returnType** giá trị trả về của phương thức
- **nameOfMethod** tên của phương thức
- **Parameter** các tham số là các giá trị được truyền cho một phương thức
- **Method body** xác định phương thức sẽ làm gì, cách các tham số được thao tác với các câu lệnh lập trình và giá trị nào được trả về

Khi phương thức được đặt `static` thì có thể gọi trực tiếp:
```
myMethod();
```
Còn khi không gọi `static`, chúng ta phải gọi thông qua đối tượng. Giả sử dưới đây đã tạo đối tượng `den` của Class `Den`:
```
den.myMethod();
```
- Đầu tiên, trình điều khiển chương trình bắt đầu trong hàm main (không quan tâm main được đặt tại vị trí nào trong file code)
- Khi gặp phương thức nào hợp lệ, nhảy để thực thi code bên trong phương thức đã được định nghĩa trong class
- Sau đó trình điều khiển lại tiếp tục nhảy đến dòng tiếp theo (trong main), sau phương thức vừa thực thi

## Ví dụ phương thức trong Java

```
// Ví dụ phương thức trong Java
class Main {

    public static void main(String[] args) {
        System.out.println("Sắp gọi đến một phương thức");

        // Gọi phương thức
        myMethod();

        System.out.println("Phương thức thực thi thành công");
    }

    // Định nghĩa phương thức
    private static void myMethod(){
        System.out.println("Dòng này in từ trong myMethod");
    }
}
```

## Phương thức chấp nhận đối số và có giá trị trả về trong Java
Chỉ cần thêm `return`

# Constructor trong Java
## Constructor là gì?

Một constructor là hàm tạo, tương tự như một phương thức nhưng không thực sự là phương thức, được gọi tự động khi class được khởi tạo

Trình biên dịch Java phân biệt giữa một phương thức và một hàm tạo theo tên và kiểu trả về của nó. Moto hàm tạo phải có **cùng tên** với class và không phải trả về bất kỳ giá trị nào

```
class ViDuConstructor {
    ViDuConstructor() {
        // Phần thân constructor
    }
}
```

Còn nếu khai báo `void` thì nó không phải là constructor

## Ví dụ về contructor

```
// Ví dụ về constructor trong Java
class ConsMain {
    private int x;

    // constructor
    private ConsMain(){
        System.out.println("Constructor được gọi");
        x = 10;
    }

    public static void main(String[] args){
        ConsMain obj = new ConsMain();
        System.out.println("Giá trị của x = " + obj.x);
    }
}
```
Khi được chạy, kết quả nhận được:
```
Constructor được gọi
Giá trị của x = 10
```
Như vậy constructor được gọi ngay khi class được tạo

Constructor có thể có hoặc không chấp nhận đối số

## Constructor không đối số (không tham số)

Constructor không có tham số nào khi định nghĩa được gọi là constructor không đối số (no-arg constructor).

```
accessModifier ClassName() {
    // constructor body
}
```
- **accessModifier** là chỉ định mức độ truy cập cho constructor
- **ClassName** là tên của class, vì tên của constructor trùng với tên của class

Ví dụ về constructor không đối số:

```
/ Ví dụ về constructor không đối số
class NoArgConstructor {

    int i;

    // Constructor không đối số
    private NoArgConstructor(){
        i = 10;
        System.out.println("Đối tượng được tạo và i = " + i);
    }

    public static void main(String[] args) {

        // Tạo đối tượng
        NoArgConstructor obj = new NoArgConstructor();
    }
}
```
Khi chạy chương trình:
```
Đối tượng được tạo và i = 10
```
Trong ví dụ trên có từ khóa `private`, chỉ định mức độ truy cập của constructor `NoArgConstructor`, làm cho nó chỉ có thể truy cập từ class của nó

## Constructor mặc định trong Java

Nếu không tự tạo constructor, trình biên dịch Java sẽ tự động tạo một constructor không có đối số trong runtime. Constructor này được gọi là **constructor mặc định**, nó sẽ khởi tạo bất kỳ biến thể hiện nào chưa được khởi tạo.

```
// Ví dụ constructor mặc định trong Java
class ConstructorMacDinh {

    // Khai báo biến, chưa khởi tạo giá trị ban đầu
    int a;
    boolean b;

    public static void main(String[] args) {

        ConstructorMacDinh obj = new ConstructorMacDinh();

        System.out.println("a = " + obj.a);
        System.out.println("b = " + obj.b);
    }
}
```
Khi chạy chương trình, kết quả nhận được là:
```
a = 0
b = false
```
Chương trình trên tương đương với:
```
// Ví dụ constructor mặc định trong Java
class ConstructorMacDinh {

    // Khai báo biến, chưa khởi tạo giá trị ban đầu
    int a;
    boolean b;

    private ConstructorMacDinh() {
        a = 0;
        b = false;
    }

    public static void main(String[] args) {

        ConstructorMacDinh obj = new ConstructorMacDinh();

        System.out.println("a = " + obj.a);
        System.out.println("b = " + obj.b);
    }
}
```

## Constructor có đối số (có tham số)

```
// Cú pháp của constructor có đối số
accessModifier ClassName(arg1, arg2, ..., argn) {
    // constructor body
}
```
Các tham số này được sử dựng để chấp nhận đối số khi khởi tạo đối tượng

# Mức độ truy cập trong Java

Có 4 mức độ truy cập trong Java:
- `Private` chỉ hiển thị trong cùng class
- `Default` chỉ hiển thị trong package (private package)
- `Protected` chỉ hiển thị bên trong package hoặc tất cả các subclass
- `Public` hiển thị mọi nơi

# Từ khóa this

Từ khóa `this` đề cập đến object hiện tại

```
// Ví dụ từ khóa this trong java
class MyClass {
    int bienTheHien;

    MyClass(int bienTheHien){
        this.bienTheHien = bienTheHien;
        System.out.println("this tham chiếu đến = " + this);
    }

    public static void main(String[] args) {
        MyClass obj = new MyClass(8);
        System.out.println("Đối tượng tham chiếu = " + obj);
    }
}
```

# Phần tiếp theo ...
https://github.com/maduc238/open5gs-docker/blob/main/Java-note/Java-OOP-2.md

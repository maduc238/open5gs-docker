# Lập trình hướng đối tượng Java (3)

# Class trừu tượng (Abstract Class) và Phương thức trừu tượng (Abstract Method)
## Class trừu tượng
Là một class không thể khởi tạo, có nghĩa là ta không thể tạo đối tượng từ class trừu tượng. Sử dụng từ khóa `abstract` để định nghĩa

```java
// Cú pháp Class trừu tượng
abstract class DongVat {
    // Thuộc tính
    // Phương thức
}
```
Do vậy nếu cố gắng khởi tạo đối tượng từ class trừu tượng này sẽ xảy ra lỗi `... is abstract; cannot be instantiated`

Tuy nhiên có thể tạo class con từ nó bằng cách tạo ra các đối tượng class con và sử dụng nó để truy cập vào các thành viên của class trừu tượng

## Phương thức trừu tượng
Sử dụng từ khóa `abstract` để khai báo một phương thức

```java
abstract void diTe();
```
Vì nó là phương thức trừu tượng nên không có phần thân. Chỉ có class trừu tượng mới có thể chứa phương thức trừu tượng, nếu không chương trình sẽ xảy ra lỗi

Một class trừu tượng có thể chứa cả phương thức trừu tượng hoặc phương thức thông thường
```java
abstract class DongVat{
    
    // Phương thức thông thường
    public void hienThiThongTin(){
        System.out.println("Tôi là Động vật");
    }
 
    // Phương thức trừu tượng
    abstract void diTe();

}
```

## Kế thừa class trừu tượng
Một class trừu tượng không thể được khởi tạo, do vậy cần thực hiện kế thừa nó
```java
abstract class DongVat{
    public void hienThiThongTin(){
        System.out.println("Tôi là Động vật");
    }
}
 
class Cho extends DongVat{
 
}
 
class Main{
    public static void main(String[] args){
        Cho cauVang = new Cho();
        cauVang.hienThiThongTin();
    }
}
```

## Ghi đè phương thức trừu tượng
```java
// Ghi đè phương thức trừu tượng
abstract class DongVat {
    abstract void diTe();
 
    public void an() {
        System.out.println("Tôi đang ăn...");
    }
}
 
class Cho extends DongVat {
 
    @override
    public void diTe() {
        System.out.println("Xồ xồ xồ...");
    }
}
class Main {
    public static void main(String[] args) {
        Cho cauVang = new Cho();
        cauVang.diTe();
        cauVang.an();
    }
}
```

## Truy cập constructor của class trừu tượng
```java
// Truy cập constructor của class trừu tượng
abstract class DongVat {
    DongVat() {
        ….
    }
}
 
class Cho extends DongVat {
    Cho() {
        super();
        ...
    }
}
```
Lưu ý: `super` nên luôn luôn là câu lệnh đầu tiên trong constructor của class

# Interface
**Interface** là một tập hợp các đặc tả mà các class khác sẽ khai triển (như namespace trong C++)
```java
interface HinhDaGiac {
    public void tinhDienTich();
}
```

## Implements trong Interface
Giống như class trừu tượng, chúng ta không thể tạo các đối tượng trực tiếp từ interface. Tuy nhiên có thể triển khai các interface trong các class khác

Chúng ta sử dụng từ khóa `implements` để thực hiện các interface
```java
interface HinhDaGiac {
    void tinhDienTich(int chieuDai, int chieuRong);
}
 
class HinhChuNhat implements HinhDaGiac {
    public void tinhDienTich(int chieuDai, int chieuRong) {
        System.out.println("Diện tích của hình chữ nhật là: " + (chieuDai * chieuRong));
    }
}
 
class Main {
    public static void main(String[] args) {
        HinhChuNhat h1 = new HinhDaGiac(){
        h1.tinhDienTich(5, 6);
    }
}
```
Kết quả nhận được:
```
Diện tích của hình chữ nhật là: 30
```
Ví dụ trên, chỉ cần truy cập interface vào h1

## Static Method và Private Method trong interface
Tương tự như một class, chúng ta có thể truy cập các phương thức static của một interface bằng cách sử dụng các tham chiếu của nó

```java
HinhDaGiac.staticMethod();
```

## Phương thức mặc định trong interface
Để khai báo phương thức mặc định bên trong các interface, chúng ta cần dùng từ khóa `default`
```java
public default tinhChuVi(){
    // Viết code như bình thường trong này
}
```
Tại sao cần phương thức mặc định?

Giả sử chúng ta thêm một phương thức mới trong interface một cách dễ dàng. Tuy nhiên nếu có nhiều class kế thừa interface này sẽ có rất nheiefu phương thức, sau đó phải theo dõi rất nhiều chỗ, lúc này sẽ dễ gặp lỗi.

Để giải quyết việc này, sử dụng **phương thức mặc định** được kế thừa như các phương thức thông thường

Ví dụ để hiểu rõ hơn về phương thức mặc định
```java
interface  HinhDaGiac {
    void tinhDienTich();
    default void soCanh() {
        System.out.println("Số cạnh của hình đa giác.");
    }
}
 
class HinhChuNhat implements HinhDaGiac {
    public void tinhDienTich() {
        int chieuDai = 5;
        int chieuRong = 6;
        int dienTich = chieuDai * chieuRong;
        System.out.println("Diện tích của hình chữ nhật là: " + dienTich);
    }
 
    public void soCanh() {
        System.out.println("Hình có 4 cạnh");
    }
}
 
class HinhVuong implements HinhDaGiac {
    public void tinhDienTich() {
        int doDaiCanh = 5;
        int dienTich = doDaiCanh * doDaiCanh;
        System.out.println("Diện tích của hình vuông là: " + dienTich);
    }
}
 
class Main {
    public static void main(String[] args) {
        HinhChuNhat hcn = new HinhChuNhat();
        hcn.tinhDienTich();
        hcn.soCanh();
 
        HinhVuong hv = new HinhVuong();
        hv.tinhDienTich();
    }
}
```
Kết quả khi chạy chương trình:
```
Diện tích của hình chữ nhật là: 30
Hình có 4 cạnh
Diện tích của hình vuông là: 25
```

## Từ khóa extends trong interface
Tương tự như class, interface có thể sử dụng từ khóa `extends` để kế thừa từ interface khác
```java
interface DuongThang {
    // Các trường
    // Các phương thức
}
 
interface HinhDaGiac extends DuongThang {
    // Kế thừa trường và phương thức của interface DuongThang
    // Các trường, phương thức riêng khác
}
```
Ngoài ra, một interface cũng có thể kế thừa nhiều interface khác nhau
```java
interface A {
    ...
}

interface B {
    ...
}

Interface C extends A, B {
    ...
}
```

# Nested class và Inner class
Phần này sẽ nói tới class lồng nhau và class bên trong thông qua các ví dụ

Có thể định nghĩa một class bên trong một class khác, như vậy được gọi là **Nested class**

```java
class OuterClass {
    ...
    class NestedClass {
        ...
 
    }
}
```

## Non-Static Nested Class
Là một class bên trong mộtt class khác, trong đó class có quyền truy cập vào các thành viên của class bên ngoài. Nó thường được gọi là **inner class** (class bên trong)

```java
class LapTop {
    double gia;
    class CPU{
        String nhaSanXuat;
        String loaiChip;
        int getTheHeCPU(){
            return 10;
        }
    }
    protected class RAM{
        String nhaSanXuat;
        String loaiRAM;
        int getBoNhoRAM(){
            return 16;
        }
    }
}
public class Main {
    public static void main(String[] args) {
        LapTop hp = new LapTop();
        LapTop.CPU cpu = hp.new CPU();
        LapTop.RAM ram = hp.new RAM();
        System.out.println("CPU thế hệ: " + cpu.getTheHeCPU() + "TH");
        System.out.println("Bộ nhớ RAM: " + ram.getBoNhoRAM() + "GB");
    }
}
```
Kết quả nhận được:
```
CPU thế thệ: 10TH
Bộ nhớ RAM: 16GB
```
Truy cập phần từ đều nhờ toán tử `dot` như: `LapTop.CPU cpu = hp.new CPU();`

Còn việc truy cập phần tử class bên ngoài từ class bên trong: Sử dụng `this`
```
Oto.this.loaiXe.equals("N20")
```

## Static inner class
Có thể định nghĩa một class static bên trong class khác. Như vậy được gọi là **static nested class**

Không giống như inner class, static nested class không thể truy cập các biến thành viên của lớp bên ngoài. Do đó, nó không có tham chiếu nào về class bên ngoài tồn tại như là `OuterClass.this`. Vì vậy có thể tạo đối tượng của static nested class trực tiếp như thế này:
```java
OuterClass.InnerClass obj = new OuterClass.InnerClass();
```
Ví dụ:
```java
class LapTop {
    String model;
    public LapTop(String model) {
        this.model = model;
    }
    static class USB{
        int usb3 = 2;
        int usbC = 1;
        int getSoCongUSB(){
            return usb3 + usbC;
        }
    }
}
public class Main {
    public static void main(String[] args) {
        LapTop.USB usb = new LapTop.USB();
        System.out.println("Tổng số cổng USB: " + usb.getSoCongUSB());
    }
}
```

# Nested Static class

Tìm hiểu thêm tại [đây](https://niithanoi.edu.vn/lap-trinh-java.html#chuong-vi-phan-2-nested-static-class-trong-java)

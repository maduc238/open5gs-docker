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


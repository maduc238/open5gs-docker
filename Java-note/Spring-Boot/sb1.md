# Chạy Spring Boot trên VS Code

Mở VS Code, nhấn `F1` để hiển thị list commands

Nhập `springcreate` để tạo một project spring boot mới

<img src="images/{E8FCEDF2-3554-49E1-8EC8-D4B013D4293B}.png.jpg">

Sau đó chọn đúng phiên bản của spring boot, tên `Group Id`, `Artifact Id`, `packaging type`... và cuối cùng là folder để chạy project

# Chạy ứng dụng

Trong Java truyền thống, khi chạy cả một project chúng ta phải định nghĩa một hàm `main()` và để nó khởi chạy đầu tiên. Với **Spring Boot** là phải chỉ cho nó biết nơi khởi chạy lần đầu để nó cài đặt mọi thứ

Cách thực hiện là thêm annotation `@SpringBootApplication` trên class chính và gọi `SpringApplication.run(App.class, args);` để chạy project - Đây chính là lệnh để tạo ***container*** sau đó tìm toàn bộ các ***dependency*** trong project của bạn và đưa vào đó

Tại đây phần chính sẽ tạo trên file `App.java`

```
package temp.demo;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```

Spring đặt tên cho ***container*** là `ApplicationContext` và đặt tên cho các ***dependency*** là `Bean`


# @Autowired - @Primary - @Qualifier

## Vấn đề của @Autowired

Trong thực tế với một interface, nếu sử dụng `@Autowired` khi Spring Boot có chứa 2 Bean trong cùng loại context, Spring lúc này sẽ bối rối không biết chọn Bean nào để inject làm đối tượng

Ví dụ với một file mới là `Naked`:
```
@Component
public class Naked implements Outfit {
    @Override
    public void wear() {
        System.out.println("Khong mac gi");
    }
}
```
Khi này chạy `App` sẽ báo lỗi

## @Primary

Một cách giai quyết cho vấn đề trên. `@Primary` là một annotation đánh dấu trên Bean giúp nó luôn được ưu tiện lựa chọn trong trường hợp nhiều Bean cùng loại trong Context

Ví dụ nếu thêm `@Primary` vào file `Naked` trước đó:
```
package temp.demo;

import org.springframework.stereotype.Component;
import org.springframework.context.annotation.Primary;

@Component
@Primary
public class Naked implements Outfit {
    @Override
    public void wear() {
        System.out.println("Khong mac gi");
    }
}
```
Lúc này `App` sẽ chạy được và nó ưu tiên `Naked` để inject vào `Girl`

## @Qualifier

Cách thứ hai, `@Qualifier` xác định tên của một Bean mà ta muốn chỉ định

Với hai Bean trước đó, đặt tên của nó như sau:

```
@Component("bikini")
public class Bikini implements Outfit {
    @Override
    public void wear() {
        System.out.println("Mac bikini");
    }
}
```
và
```
@Component("naked")
public class Naked implements Outfit {
    @Override
    public void wear() {
        System.out.println("Khong mac gi");
    }
}
```
Với `Girl`, thay vì gọi
```
public Girl(Outfit outfit) {
        this.outfit = outfit;
    }
```
Mà gọi Bean riêng biệt bằng cách gọi annotation `@Qualifier`
```
public Girl(@Qualifier("naked") Outfit outfit) {
        this.outfit = outfit;
    }
```
Với `App` thì do gọi Component riêng nên không thêm `@Autowired`. Chạy code thì kết quả thu được chính xác

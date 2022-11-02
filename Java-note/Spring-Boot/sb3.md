# Spring Bean Life Cycle, @PostConstruct và @PreDestroy

## @PostConstruct
Được đánh dấu trên một `method` **duy nhất** bên trong một Bean. Khi khởi chạy Bean nó sẽ được tạo ra và quản lý
```
@Component
public class Girl {

    @PostConstruct
    public void postConstruct(){
        System.out.println("\t>> Doi tuong Girl sau khi khoi tao xong se chay ham nay");
    }
}
```

## @PreDestroy
Được đánh dấu trên một `method` **duy nhất** bên trong một Bean. Sẽ gọi hàm này **trước khi** một Bean bị xóa hoặc không được quản lý nữa

Cũng trong `Girl`:
```
@PreDestroy
    public void preDestroy(){
        System.out.println("\t>> Doi tuong Girl truoc khi bi destroy thi chay ham nay");
    }
```

## Bean Life Cycle

![f9b4e79f-24e8-40e6-918e-f66e4fa5ee0a](https://user-images.githubusercontent.com/95759699/199367687-108f2658-57a2-4877-b370-65d983c2ae5b.jpg)

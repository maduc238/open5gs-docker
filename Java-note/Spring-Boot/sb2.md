# @Autowired - @Primary - @Qualifier

## Vấn đề của @Autowired

Trong thực tế với một interface, nếu sử dụng `@Autowired` khi Spring Boot có chứa 2 Bean trong cùng loại context, Spring lúc này sẽ bối rối không biết chọn Bean nào để inject làm đối tượng


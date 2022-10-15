# Java cơ bản

# Hề lố
Tạo một file `temp.java`
```
public class temp {
    public static void main(String[] args) {
        System.out.println("Hellooo World~~~");
    }
}
```

# StringBuffer
Ví dụ về sử dụng String Buffer
```
long start = System.nanoTime();

StringBuffer sb = new StringBuffer("Hello");
for (int i = 0; i < 1000; i++) {
    sb.append(" world");
}
String s = sb.toString();
long end = System.nanoTime();
System.out.println("Total time: "+(end-start));
```
Việc sử dụng này sẽ nhanh hơn nhiều lần cách `+=` thông thường. Vì `String` là `immutable`, nội dung của nó không được quyền thay đổi. Nên mỗi lần thêm là code tự động tạo nhiều `String` nữa gây giảm tốc độ


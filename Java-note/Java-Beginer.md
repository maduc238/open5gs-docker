# Tìm hiểu về JDK, JRE, JVM
## JVM là gì?

JVM là máy ảo Java, một máy trừu tượng cho phép máy tính bạn chạy chương trình Java

Khi chạy chương trình Java. Trước tiên trình biên dịch Java sẽ dịch mã Java thành bytecode

Sau đó JVM sẽ dịch bytecode thành mã máy gốc (tập hợp các hướng dẫn mà CPU của máy tính thực thi trực tiếp). Bởi vì khi viết Java, nó được viết cho JVM chứ không phải máy tính của bạn

```
Chương tình  --->    Java    --->  Mã máy  ---> Kết quả
    Java           Bytecode
```

## JRE là gì?

JRE (Java Runtime Enviroment) là môi trường thực thi Java

Là gói các phần mềm cung cấp các thư viện Java Class cùng với JVM và các thành phần khác để chạy các ứng dụng được viết bằng Java

```
   -- JRE
   |
   |----- JVM
   |----- Các thư viện Class
```

## JDK là gì?

JDK (Java Development Kit) là một bộ công cụ phát triển phần mềm để phát triển các ứng dụng trong Java. Khi tải JDK, JRE cũng sẽ được đi kèm.

```
   -- JRK
   |
   |----- JRE
   |----- Compilers
   |----- Debuggers
   |----- JavaDoc
```

# Biến trong Java

```
boolean

int
byte
short

float
long
double

char
String
```

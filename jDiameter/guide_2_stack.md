# Diameter Stack

Diameter Stack là thành phần core. Nó thiện hiện tất cả các tác vụ cần thiết để cho phép người dùng tương tác với mạng Diameter. Nó quản lý các Diameter ngang hàng và cho phép định tuyến các bản tin giữa chúng. [Tài liệu chi tiết](http://tools.ietf.org/html/rfc3588)

Diameter Stack hỗ trợ các phiên ứng dụng sau:
- Base
- Credit Control Application (CCA)
- Sh
- Ro
- Rf
- Cx/Dx
- Gx
- Gq'
- Rx
- S6a
- S13
- Sh
- SLg
- SLh
- ...

# Tổng quan thiết kế Diameter Stack

Diameter Stack được thiết kế để có thể mở rộng. Để đạt được điều đó, hai bộ API được định nghĩa bởi stack - một bộ xác định các contracts cơ bản giữa ứng dụng người dùng và stack, và một bộ xác định các contracts cho phép phiên bản đưa các đối tượng tùy chỉnh vào stack để thực hiện các tác vụ nhất định

# Hướng dẫn về JDiameter

# Giới thiệu về RestComm JDiameter

Diameter là giao thức mạng máy tính để Xác thực, Ủy quyền và Kế toán (được định nghĩa trong RFC3588). Nó là sự kế thừa của RADIUS và được thiết kế để khắc phục một số hạn chế của RADIUS:
- Không có độ tin cậy và tính linh hoat khi truyền (Diameter dùng TCP/SCTP thay vì UDP)
- Không có bảo mật trong giao thức (Diameter hỗ trợ IPSec (bắt buộc) và TLS (tùy chọn))
- Hạn chế không gian địa chỉ cho các AVP (Diameter sử dụng không gian địa chỉ 32 bit thay vì 8 bit)
- Chỉ có thể sử dụng chế độ stateless (Diameter hỗ trợ cả stateful và stateless)
- Static peers (Diameter cung cấp khả năng dynamic discovery, sử dụng DNS, SRV và NAPTR)
- Không có liên kết ngang hàng (Diameter giới thiệu khả năng negotiation)
- Không hỗ trợ chuyển đổi dự phòng lớp truyền tải. Diameter tuân theo RFC3539 giới thiệu các quy trình chính xác
- Hạn chế hỗ trợ chuyển vùng (Diameter giới thiệu các cơ chế chuyển vùng an toàn và có thể mở rộng)
- Không thể mở rộng (Diameter cho phép mở rộng - các lệnh mới và AVP được xác định)

Diameter cung cấp tất cả các khả năng của giao thức RADIUS và tương thích với RADIUS. Nó cũng có thẻ xác định các phần mở rộng hoặc "Applications"


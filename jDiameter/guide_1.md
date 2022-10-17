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

Mỗi ứng dụng giới thiệu các loại bản tin, mã AVP và state machines. Mỗi ứng dụng có một Application ID và Vendor ID riêng được sử dụng để phân biệt giữa các ứng dụng. Application code được dùng để báo hiệu cho các peers khác biết operation nào được hỗ trợ bởi connecting peer (Capabilities Exchange / Negotiation)

# Cấu trúc bản tin Diameter

Mỗi bản tin có cấu trúc cố định, gồm 2 phần: header và payload

Cấu trúc header là dạng phổ biến cho mỗi bản tin. Độ dài, nội dung là cố định. Nội dung header thông báo bao gồm code, application và certain bit flags, nó sẽ giúp để nhận diện bản tin trong Diameter scope

Cấu trúc payload được dựng bởi các AVP. Nội dung của chúng khác nhau đối với từng lệnh và ứng dụng, mặc dùng tất cả chúng đều xác định AVP Session-ID là bắt buộc
```
    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |    Version    |                 Message Length                |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   | command flags |                  Command-Code                 |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                         Application-ID                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                      Hop-by-Hop Identifier                    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                      End-to-End Identifier                    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  AVPs ...
   +-+-+-+-+-+-+-+-+-+-+-+-+-
```
**Version** Cho biết phiên bản của Diameter. Giá trị này luôn được đặt thành `1`

**Message Length** Độ dài bản tin Diameter, bao gồm các trường header

**Flags** Được tạo bởi 8 bit, để cung cấp thông tin liên quan đến bản tin. 4 bit đầu tiên trong flags octet có ý nghĩa:
- R = request (1) hoặc answer (0)
- P = proxiable (1) và có thể được ủy quyền, chuyển tiếp hoặc chuyển hướng, hoặc được xử lý cục bộ (0)
- E = bản tin lỗi (1) và bản tin thông thường (0)
- T = có khả năng được truyền lại (1) hoặc được gửi lần đầu tiên (0)
4 bit cuối cùng được dành để sử dụng trong tương lai nên được đặt thành 0

**Command Code** Cho biết lệnh được liên kết với bản tin

**Application ID** Xác định ứng dụng mà bản tin có thể áp dụng. Ứng dụng này là ứng dụng xác thực, kế toán hay ứng dụng cụ thể nào đó của nhà cung cấp. Trong `application-id` phần header phải giống với nội dung có trong bất kỳ AVP có liên quan nào trong bản tin

**Hop-by-Hop ID** ID duy nhất được sử dụng để so sánh các cặp request và answer tương ứng

**End-to-End ID** ID duy nhất có giới hạn thời gian được sử dụng để phát hiện các bản tin trùng lặp. ID phải là duy nhất trong ít nhất 4 phút. Người khởi tạo bản tin này phải đảm bảo rằng header này chứa cùng một giá trị có trong yêu cầu tương ứng

Payload của bản tin được dựng từ các AVP. Mỗi AVP có một dạng cấu trúc giống nhau như: một header, và encoded data. Data có thể đơn giản (như là integer, long) hoặc phức tạp (một số encoded AVP)
```
    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                           AVP Code                            |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |V M P r r r r r|                  AVP Length                   |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                        Vendor-ID (opt)                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |    Data ...
   +-+-+-+-+-+-+-+-+
```
**AVP Code** Mã định danh duy nhất cho AVP. Số AVP từ 1 đến 255 được dành riêng cho khả năng tương thích ngược với RADIUS và không yêu cầu header ID nhà cung cấp. AVP số 256 trở lên được sử dụng riêng cho Diameter và được cấp phát bởi IANA

**Flags** Cờ bit chỉ định cách xử lý từng thuộc tính. Các cờ octet có cấu trúc: V M P r r r r r. Mô tả đầy đủ có sẵn trong [Section 4.1 của RFC3588](https://www.rfc-editor.org/rfc/rfc3588#section-4.1). 3 bit đầu có nghĩa:
- V nếu được đặt cho biết rằng các optional octets (Vendor-ID) được thể hiện trong AVP header
- M nếu được đặt cho biết máy ngang hàng phải hiểu AVP này hoặc không thì gửi câu trả lời lỗi
- P nếu được đặt cho biết nhu cầu mã hóa để bảo mật đầu cuối
5 bit cuối cùng dành cho sử dụng trong tương lai và được đặt thành 0

**AVP Length** Cho biết số octet trong AVP bao gồm các thông tin: AVP Code, AVP Length, AVP Flags, Vendor-ID field (nếu xuất hiện), AVP Data

**Vendor-ID** Một optional octet xác định AVP trong không gian ứng dụng. AVP code và AVP Vendor-ID tạo ra một số định dạng duy nhất cho AVP

# Contents

Ứng dụng Diameter core được dựng dựa trên 3 thành phần cơ bản:

[***Stack***](https://github.com/maduc238/open5gs-docker/blob/main/jDiameter/guide_2_stack.md) Các Diameter Stack mở rộng, cung cấp hỗ trợ phiên cơ bản cùng với các phiên ứng dụng cụ thể

***Multiplexer (MUX)*** Diameter Stack multiplexer. Cho phép những listener khác nhau chia sẻ cùng một phiên bản stack

***Dictionary*** Diameter Message and AVP Dictionary. Cung cấp một API để truy cập thông tin về các AVP. Dictionary được nhúng vào trong MUX

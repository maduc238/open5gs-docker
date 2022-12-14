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
## Khả năng mở rộng Diameter Stack
Diameter Stack được thiết kế để có thể mở rộng. Để đạt được điều đó, hai bộ API được định nghĩa bởi stack - một bộ xác định các contracts cơ bản giữa ứng dụng người dùng và stack, và một bộ xác định các contracts cho phép phiên bản đưa các đối tượng tùy chỉnh vào stack để thực hiện các tác vụ nhất định (ví dụ như `SessionFactory`). `ISessionFactory` khai báo các phương thức bổ sung cho phép nhà phát triển khai báo hành vi tùy chỉnh (ví dụ như phiên ứng dụng truy chỉnh)
```
------------------------      --------------------      --------------------
|  SessionFactoryImpl  |----->|  ISessionFactory |----->|  SessionFactory  |
------------------------      --------------------      --------------------
```
General pattern để khai báo interface:
- Interface `ComponentInterface` khai báo một tập các phương thức tối thiểu để một thành phần thực hiện nhiệm vụ của nó
- Interface `IComponentInterface` cung cấp các phương thức hành vi bổ sung (provides additional behavior methods)

## Mô hình Diameter Stack
Diameter Stack thực hiện các tác vụ sau:
- Quản lý kết nối với các remote peer
- Quản lý session object
- Định tuyến bản tin trên hành động của session
- Nhận và quản lý gửi bản tin đến listener được chỉ định (thường là đối tượng session)

# Diameter Stack Configuration

Stack được cấu hình bằng file XML. Cấu trúc cấp cao nhất của tệp:
```
<Configuration xmlns="http://www.jdiameter.org/jdiameter-server">

	<LocalPeer></LocalPeer>
	<Parameters></Parameters>
	<Network></Network>
	<Extensions></Extensions>

</Configuration>
```
Cụ thể chi tiết phần `<LocalPeer>`: chứa các tham số ảnh hưởng đến local Diameter peer. Các phần tử và thuộc tính có sẵn được liệt kê bên dưới ví dụ: 
```
<LocalPeer>
	<URI value="aaa://localhost:3868"/>
	<IPAddresses>
		<IPAddress value="127.0.0.1"/>
	</IPAddresses>

	<Realm value="mobicents.org"/>
	<VendorID value="193"/>
	<ProductName value="jDiameter"/>
	<FirmwareRevision value="1"/>

	<OverloadMonitor>
		<Entry index="1" lowThreshold="0.5" highThreshold="0.6">
			<ApplicationID>
				<VendorId value="193"/>
				<AuthApplId value="0"/>
				<AcctApplId value="19302"/>
			</ApplicationID>
		</Entry>
	</OverloadMonitor>
	<Applications>
		<ApplicationID>
			<VendorId value="193"/>
			<AuthApplId value="0"/>
			<AcctApplId value="19302"/>
		</ApplicationID>
	</Applications>
</LocalPeer>
```
- <***URI***> chỉ định local peer. URI có định dạng `aaa://FQDN:port` (Fully qualified domain name)
- <***IPAddresses***> chứa một hoặc nhiều phần tử <IPAddress>: trong đó chứa một địa chỉ IP hợp lệ, duy nhất cho local peer được lưu trữ trong thuộc tính `value`
- <***Realm***> chỉ định realm của local peer
- <***VendorID***> chỉ định ID của vendor tương ứng do IANA phát hành
- <***ProductName***> tên product của local peer
- <***FirmwareRevision***> phiên bản của bản tin, thường là `1`
- <***OverloadMonitor***>, <***Entry***> ...
- ...
  
Các phần tử <Parameter> chỉ định các tham số cho Diameter Stack:
```
<Parameters>

	<AcceptUndefinedPeer value="true"/>
	<DuplicateProtection value="true"/>
  <DuplicateTimer value="240000"/>
  <DuplicateSize value="5000"/>
	<UseUriAsFqdn value="true"/> <!-- Needed for Ericsson SDK Emulator -->
	<QueueSize value="10000"/>
	<MessageTimeOut value="60000"/>
	<StopTimeOut value="10000"/>
	<CeaTimeOut value="10000"/>
	<IacTimeOut value="30000"/>
	<DwaTimeOut value="10000"/>
	<DpaTimeOut value="5000"/>
	<RecTimeOut value="10000"/>

	<!-- Peer FSM Thread Count Configuration -->
	<PeerFSMThreadCount value="3" />

	<Concurrent>
		<Entity name="ThreadGroup" size="64"/>
		<Entity name="ProcessingMessageTimer" size="1"/>
		<Entity name="DuplicationMessageTimer" size="1"/>
		<Entity name="RedirectMessageTimer" size="1"/>
		<Entity name="PeerOverloadTimer" size="1"/>
		<Entity name="ConnectionTimer" size="1"/>
		<Entity name="StatisticTimer" size="1"/>
		<Entity name="ApplicationSession" size="16"/>
	</Concurrent>

</Parameters>
```
- <***AcceptUndefinedPeer***> chỉ định liệu stack có chấp nhận các kết nối từ peer không xác định hay không
- <***DuplicateProtection***> chỉ định có bật tính năng bảo vệ tin trùng lặp hay không
- <***DuplicateTimer***> giá trị thời gian mỗi tin nhắn trùng lặp
- <***DuplicateSize***> số lượng request được lưu trữ để bảo vệ chống trùng lặp
- <***UseUriAsFqdn***> xem URI có được sử dụng làm FQDN hay không. Nếu là `true`, stack sẽ đợi máy đích ở định dạng `aaa://isdn.domain.com:3868` thay vì dạng thông thường `isdn.domain.com`
- <***QueueSize***> số lượng hàng đợi chứa các sự kiện và bản tin FSM
- <***MessageTimeOut***> timeout cho các bản tin không phải là bản tin protocol FSM. Tính bằng mili giây
- <***StopTimeOut***> khoảng thời gian stack chờ tất cả các tài nguyên dừng lại. Tính bằng mili giây
- ...
- <***PeerFSMThreadCount***> số thread để xử lý các sự kiện trong FSM peer

<Network> chứa các phần tử chỉ định các tham số cho peer bên ngoài:
```
<Network>
	
	<Peers>
		<!-- This peer is a server, if it's a client attempt_connect should be set to false -->
		<Peer name="aaa://127.0.0.1:3868" attempt_connect="true" rating="1"/>
	</Peers>

	<Realms>
		<Realm name="mobicents.org" peers="127.0.0.1" local_action="LOCAL" dynamic="false" exp_time="1">
			<ApplicationID>
				<VendorId value="193"/>
				<AuthApplId value="0"/>
				<AcctApplId value="19302"/>
			</ApplicationID>
		</Realm>
	</Realms>

</Network>
```
- <***Peers***> chứa các phần tử con <Peer>, chỉ định các peer bên ngoài và cách kết nối với chúng. <Peer> chỉ định tên của các peer đó, liệu chúng được coi là client hay server và rating của chúng
	+ name: Tên của peer ở dạng URI: `aaa://192.168.1.1:3868`
	+ attempt_connect: Xác định xem stack có cố gắng kết nối tới peer này hay không
	+ rating: Chỉ định hạng của peer này để đạt được ưu tiên / sắp xếp peer
- <***Realms***> chứa các phần tử <Realm> con, chỉ định tất cả các realm kết nối vào mạng Diameter. <Realm> chứa các thuộc tính và phần tử mô tả các cấu hình realm khác nhau cho Core. Nó hỗ trợ phần tử con <ApplicationID>, xác định các ứng dụng được hỗ trợ
	+ peers: Dánh sách các peer được phân tách bằng dấu phẩy. Mỗi peer được đại diện bởi một địa chỉ IP hoặc FQDN
	+ local_action: Hành động mà Local Peer này sẽ thực hiện trên realm được chỉ định
	+ dynamic: chỉ định realm này là dynamic. Có nghĩa là những peer ngang hàng kết nối với những peer có tên realm này sẽ được thêm vào danh sách ngang hàng của realm nếu chưa có mặt
	+ exp_time: Thời gian trước khi gửi một peer thuộc về realm này, nếu không sẽ bị ngắt kết nối

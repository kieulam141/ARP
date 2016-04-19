# Tổng Quan giao thức ARP
## Mục lục

[1.Khái niệm] (#1)

[2.Nguyên tắc hoạt động] (#2)

[3.Cấu trúc frame ARP] (#3)

[4.Bắt gói tin ARP] (#4)

[5.Tham Khảo] (#5)

<a name="1"></a>
### 1.Khái niệm
ARP-Address Resolution Protocol được sử dụng trên các data link multiaccess của mạng LAN đặc biệt là data link Ethernet
để cho phép tương quan giữa một địa chỉ lớp 3 (thông thường là địa chỉ IP) với một địa chỉ lớp 2 (thông thường là địa chỉ MAC)
nhằm phục vụ cho việc đóng một gói tin lớp 3 (packet) vào một frame lớp 2.

<img src="http://i.imgur.com/mKdx4lB.jpg" />


<a name="2"></a>
### 2.Nguyên tắc hoạt động
- Khi 1 thiêt bị mạng muốn biết địa chỉ Mac của thiết bị mạng nào đó nó sẽ gửi broadcast 1 ARP Request gồm: địa chỉ Mac của nó, IP của 
thiết bị mà nó cần biết địa chỉ Mac.
- Mỗi 1 thiết bị nhận được request này sẽ so sánh với IP của mình nếu giống nhau sẽ reply gói tin request có địa chỉ Mac của mình.

<img src="http://i.imgur.com/mKdx4lB.jpg" />

- Các bước tiến hành:
<ul>
	<li>PC1 broadcast 1 ARP request chứa địa chỉ Mac, IP của chính nó, IP máy nhận(192.168.1.2) và Mac máy nhận ff:ff:ff:ff:ff:ff</li>
	<li>Trong toàn miền broadcast, thì chỉ có PC2 có địa chỉ iP (192.168.1.2) nên nó sẽ unicast gói tin ARP reply trở lại PC1
	bao gồm địa chỉ Mac của nó.PC2 đồng thời cập nhật bảng ARP cache của mình với địa chỉ IP và MAC của PC1</li>
	<li>Khi PC1 nhận được gói tin ARP reply và xác định được MAC cần tìm, nó sẽ thực hiện đóng frame cho hoạt động ping giữa PC1 và PC2,
	Sau đó lưu kết quả vào bảng ARP cache của mình.</li>
	<li>Tiến hành tương tự với PC3, ta có bảng ARP cache:</li>
	<li><img src="http://i.imgur.com/aEl4zFx.jpg /"></li>
</ul>

<a name="3"></a>
### 3.Cấu trúc frame ARP
<img src="http://i.imgur.com/n71Wi7c.jpg" />
| Tên trường | Mô tả |
|------------|-------|
| Source MAC | địa chỉ MAC của thiết bị gửi đi frame Ethernet |
| Destination MAC | địa chỉ broadcast FFFF.FFFF.FFFF |
| Frame – type | loại dữ liệu được đóng gói trong frame Ethernet |
| Hard Type | Công nghệ phần cứng sử dụng |
| Protocol Type | Kiểu giao thức máy gửi cung cấp (IPv4 là 2048) |
| Hard Size | kích thước tính theo byte của địa chỉ vật lý |
| Prot Size | kích thước tính theo byte của địa chỉ logic |
| Op | 1 – ARP Request, 2 – ARP Reply, 3 – RARP Request và 4 – RARP Reply |
| Sender MAC | Địa chỉ MAC của máy gửi |
| Sender IP | Địa chỉ IP của máy gửi |
| Target MAC | Địa chỉ MAC của máy nhận |
| Target IP | Địa chỉ IP của máy nhận |

<a name="4"></a>
### 4.Bắt gói tin ARP
- hiển thị bảng ARP với cmd: arp -a
<img src="http://i.imgur.com/AA9Msqz.png" />
- Thực hiện bắt gói tin ARP với wireshark.
- Ping 192.168.100.17
<img src="http://i.imgur.com/UfmVTS9.png" />

- Bắt gói tin ARP request
<img src="http://i.imgur.com/OtuOCNG.png" />

- Bắt gói tin ARP reply
<img src="http://i.imgur.com/GNu4Hf4.png" />

- Kiểm tra lại bảng ARP cache xem cập nhật chưa
<img src="http://i.imgur.com/RMWEqNy.png" />

<a name="5"></a>
###5. Tham Khảo
- http://www.ntps.edu.vn/blog/186-ip-services-bai-so-12-address-resolution-protocol-arp

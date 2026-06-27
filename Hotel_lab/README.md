# 🏨 Cisco Lab - Vic Modern Hotel Network

## Giới Thiệu

Bài lab mô phỏng hệ thống mạng nội bộ của khách sạn **Vic Modern Hotel** - một tòa nhà 3 tầng với các phòng ban hoạt động độc lập nhưng vẫn có thể giao tiếp với nhau trong toàn bộ hệ thống.

Mỗi tầng được trang bị một switch riêng và chia thành các VLAN theo từng phòng ban. Ba router đặt tại phòng máy chủ (IT Department, tầng 3) kết nối với nhau qua Serial DCE, sử dụng OSPF để định tuyến, đảm bảo mọi thiết bị trong khách sạn đều liên lạc được với nhau.

---

## 🗺️ Mô Hình Topology

### Tổng Quan
![Topology Overview](topology-overview.png)

### Chi Tiết
![Topology Detail](topology-detail.png)

### Tầng 3 - IT & Admin
![Floor 3](topology-branch3.png)

---

## 🏗️ Phân Tầng & Phòng Ban

### 🔴 Tầng 1 (1st Floor)

| VLAN | Phòng Ban | Subnet |
|---|---|---|
| VLAN 80 | Reception | 192.168.8.0/24 |
| VLAN 70 | Store | 192.168.7.0/24 |
| VLAN 60 | Logistics | 192.168.6.0/24 |

### 🟢 Tầng 2 (2nd Floor)

| VLAN | Phòng Ban | Subnet |
|---|---|---|
| VLAN 50 | Finance | 192.168.5.0/24 |
| VLAN 40 | HR | 192.168.4.0/24 |
| VLAN 30 | Sales / Marketing | 192.168.3.0/24 |

### 🟠 Tầng 3 (3rd Floor) - Phòng Máy Chủ

| VLAN | Phòng Ban | Subnet |
|---|---|---|
| VLAN 20 | Admin | 192.168.2.0/24 |
| VLAN 10 | IT | 192.168.1.0/24 |

---

## 🌐 Kết Nối Giữa Các Router (WAN Serial)

Ba router đặt tại tầng 3 kết nối với nhau qua **Serial DCE cable**:

| Đường Truyền | Subnet |
|---|---|
| Router1 ↔ Router2 | 10.10.10.0/30 |
| Router2 ↔ Router3 | 10.10.10.4/30 |
| Router1 ↔ Router3 | 10.10.10.8/30 |

---

## ✅ Những Gì Đã Thực Hiện Được

- ✅ **Phân vùng VLAN** cho 8 phòng ban trên 3 tầng, tách biệt hoàn toàn lưu lượng nội bộ từng phòng
- ✅ **Inter-VLAN Routing** (Router-on-a-Stick) cho phép các phòng ban trong cùng tầng giao tiếp với nhau
- ✅ **Kết nối Serial DCE** giữa 3 router với 3 subnet `/30` point-to-point
- ✅ **OSPF** cấu hình định tuyến động giữa các router, đảm bảo toàn bộ thiết bị trong khách sạn liên lạc được với nhau
- ✅ **DHCP Server** cấu hình trên từng switch, tự động cấp IP cho tất cả thiết bị theo đúng VLAN
- ✅ **Wireless Access Point** triển khai tại mỗi tầng, hỗ trợ Laptop và Smartphone kết nối WiFi
- ✅ **SSH** cấu hình trên tất cả router, cho phép đăng nhập quản trị từ xa 
- ✅ **Port Security (Sticky)** cấu hình tại switch tầng 3, chỉ cho phép Test-PC truy cập cổng Fa0/1, vi phạm sẽ tự động shutdown
- ✅ **Test-PC** dùng để kiểm tra kết nối toàn mạng và thử nghiệm SSH remote login tới các router

---

## 🛠️ Công Cụ

- **Cisco Packet Tracer**

# Hướng dẫn cấu hình mạng trên Ubuntu sử dụng Netplan

## Giới thiệu về Netplan

Netplan là một công cụ quản lý mạng mới được sử dụng trên các phiên bản Ubuntu từ 17.10 trở đi. Nó sử dụng tệp cấu hình YAML để thiết lập mạng và sau đó chuyển đổi các cấu hình này sang các dịch vụ back-end như NetworkManager hoặc systemd-networkd để quản lý mạng.

## Thư mục và Tệp Cấu hình

Các tệp cấu hình `netplan` nằm trong thư mục `/etc/netplan/`. Tệp có thể có tên bất kỳ nhưng thường có đuôi `.yaml`. Ví dụ: `01-netcfg.yaml`hoặc `01-network-manager-all.yaml`

## 1. Cấu hình Mạng 

Để cấu hình địa chỉ IP tĩnh cho giao diện mạng `ens33`, bạn cần tạo hoặc chỉnh sửa tệp YAML trong thư mục `/etc/netplan/`.

- Liệt kê các tệp trong thư mục `/etc/netplan/`:
```
# ls /etc/netplan/
```
![image](https://github.com/user-attachments/assets/cdbc1d35-2d39-4020-b017-b183b0200441)

- Sửa nội dung file 
```
# nano /etc/netplan/01-network-manager-all.yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```
- Sau khi lưu tập tin áp dụng cấu hình mới:
```
# sudo netplan apply
```
- Cấu hình mạng sử dụng DHCP 
```
# nano /etc/netplan/01-network-manager-all.yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: yes
```
## **2) Các lệnh Network cơ bản**
### **2.1) Xem địa chỉ IP**
```
# ifconfig       ( Ethernet + Loopback )
# iwconfig       ( Wifi )
# ifconfig -a    ( đầy đủ thông tin )
# ip a s         ( đầy đủ thông tin )
```
### **2.2) Tắt / Bật card mạng**
```
# ifup [tên_card_mạng]       : bật card mạng
# ifdown [tên_card_mạng]     : tắt card mạng
```
### **2.3) Khởi động lại `network.service`**
```
    # service network restart
<=> # /etc/init.d/network restart
<=> # systemctl restart network.service
```
### **2.4) Xem thông tin gateway**
```
# route
# ip route
```
<br>







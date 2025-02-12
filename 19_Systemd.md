# Systemd
- **Systemd** là 1 nhóm các chương trình đặc biệt quản lý , vận hành và theo dõi các tiến trình khác hoạt động .
### **Vai trò của systemd**
- **Systemd** cung cấp 1 chương trình đầu tiên được khởi động trong hệ thống ( **PID** = `1` ) . Và khi hoạt động , `/sbin/init` sẽ giữ vai trò kích hoạt các file cấu hình cần thiết cho hệ thống , và các chương trình này sẽ nối tiếp để hoàn tất công đoạn khởi tạo .
### **Các thành phần của systemd**
- Về cơ bản thì **systemd** tương đương với 1 chương trình quản lý hệ thống và các dịch vụ trong Linux . Nó cung cấp các tiện ích sau :
    - `systemctl` : dùng để quản lý trạng thái của các dịch vụ hệ thống ( bắt đầu , kết thúc , khởi động hoặc kiểm tra trạng thái hiện tại ) .
    - `journald` : dùng để quản lý nhật ký hoạt động của hệ thống ( hay còn gọi là ghi log ) .
    - `logind` : dùng để quản lý và theo dõi việc đăng nhập / đăng xuất của người dùng .
    - `networkd` : dùng để quản lý các kết nối mạng thông qua các cấu hình mạng .
    - `timedated` : dùng để quản lý thời gian trên hệ thống hoặc mạng .
    - `udev` : dùng để quản lý các thiết bị và firmware
### **Unit file**
- Tất cả các chương trình được quản lý bởi **systemd** đều được thực thi dưới dạng **daemon** hay **background** bên dưới nền và được cấu hình thành 1 file configuration gọi là **unit file** .
- Các **unit file** này sẽ gồm 12 loại :
    - `service` : các file quản lý hoạt động của 1 số chương trình .
    - `socket` : quản lý các kết nối
    - `device` : quản lý thiết bị
    - `mount` : gắn thiết bị
    - `automount` : tự động gắn thiết bị
    - `swap` : vùng không gian bộ nhớ trên đĩa cứng
    - `target` : quản lý tạo liên kết
    - `path` : quản lý các đường dẫn
    - `timer` : dùng cho cronjob để lập lịch
    - `snapshot` : sao lưu
    - `slice` : dùng cho quản lý tiến trình
    - `scope` : quy định không gian hoạt động
### **Service**
- Mặc dù có 12 loại **unit file** trong **systemd** , tuy nhiên có lẽ `service` là loại được quan tâm nhất .
- Loại này sẽ được khởi động khi bật máy và luôn chạy ở chế độ nền ( **daemon** hoặc **background** ) .
- Các `service` thường được cấu hình trong các file riêng biệt và được quản lý thông qua **systemctl** .
- Có thể dùng các câu lệnh sau để xem các `service` :
    ```
    # systemctl list-units | grep -e '.service'
    hoặc
    # systemctl -t service
    ```

  ![image](https://github.com/user-attachments/assets/95556685-a438-4376-8a65-45f9c6e5d5f2)

    
- Các tùy chọn bật/tắt `service` trong **systemctl** :
    - `start` : bật service
    - `stop` : tắt service
    - `restart` : khởi động lại service
    - `reload` : load lại file cấu hình ( chỉ có 1 số `service` hỗ trợ như **Apache / NginX** ,... )
    - `enable` : service được khởi động cùng hệ thống
    - `disable` : service không được khởi động cùng hệ thống
    - `is-enabled`:	Kiểm tra dịch vụ có bật hay không
    - `daemon-reload`: Tải lại cấu hình systemd sau khi chỉnh sửa
###  Quản lý tiến trình với journalctl
- `journalctl` giúp xem log hệ thống và dịch vụ trong systemd:
  - `journalctl -xe`:	Xem lỗi gần nhất
  - `journalctl -u <dịch-vụ>`:	Xem log của dịch vụ
  - `journalctl --since "1 hour ago"`:	Xem log từ 1 giờ trước
  - `journalctl --since today`:	Xem log từ đầu ngày hôm nay
  - `journalctl -n 50`:	Xem 50 dòng log cuối cùng
  - `journalctl -f`:	Theo dõi log realtime (giống tail -f)
### Tạo một dịch vụ systemd mới
**Tạo file unit mới**
Tạo file `/etc/systemd/system/myservice.service` với nội dung:
```
[Unit]
Description=Dịch vụ mẫu
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/user/myscript.py
Restart=always
User=thupm
WorkingDirectory=/home/thupm

[Install]
WantedBy=multi-user.target
```
**Kích hoạt và kiểm tra dịch vụ**
```
sudo systemctl daemon-reload
sudo systemctl start myservice
sudo systemctl enable myservice
sudo systemctl status myservice
```
### Quản lý Timer (Thay thế Cronjob)
Systemd hỗ trợ Timer Unit để chạy các tác vụ định kỳ.
Ví dụ: Tạo một job chạy mỗi ngày.
**Tạo một script**
Tạo file `/home/user/script.sh:`
```
#!/bin/bash
echo "Hello Systemd Timer" >> /home/user/log.txt
```

**Cấp quyền thực thi:**
`chmod +x /home/user/script.sh`

**Tạo Service Unit**
Tạo file `/etc/systemd/system/myjob.service:`
```
[Unit]
Description=Chạy script.sh mỗi ngày

[Service]
ExecStart=/home/user/script.sh
```

**Tạo Timer Unit**
Tạo file `/etc/systemd/system/myjob.timer:`
```
[Unit]
Description=Chạy myjob.service mỗi ngày

[Timer]
OnCalendar=daily

[Install]
WantedBy=timers.target
```
**Kích hoạt Timer**
```
sudo systemctl daemon-reload
sudo systemctl start myjob.timer
sudo systemctl enable myjob.timer
```
**Kiểm tra trạng thái timer**
`
systemctl list-timers
`

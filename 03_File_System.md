# Cấu trúc File System trên Linux

<img src="https://nepalisupport.wordpress.com/wp-content/uploads/2016/06/linux-filesystem.png"> 

## 1) /Root
- Thư mục cá nhân của người dùng `root`
- Đây là nơi người dùng root có thể lưu trữ các tệp cá nhân và cấu hình riêng biệt.

## 2) /bin
- Chứa các tệp thực thi cơ bản cần thiết cho hệ thống để khởi động và vận hành ở chế độ đơn người dùng. Ví dụ: `ls, cp, mv, rm, bash`
- Lệnh Linux phổ biến sử dụng ở chế độ single-user mode nằm ở thư mục này .
- Tất cả các user hệ thống nằm tại thư mục này đều có thể sử dụng lệnh .

## 3) /boot 
- Chứa các tệp cần thiết cho quá trình khởi động hệ thống, bao gồm kernel (nhân hệ điều hành), các tệp khởi động và bộ nạp khởi động (boot loader). Ví dụ: `vmlinuz, initrd.img, grub`

## 4) /dev
- Chứa thông tin nhận biết cho các thiết bị của hệ thống , bao gồm các thiết bị đầu cuối , USB hoặc các thiết bị được gắn trên hệ thống .
- Mỗi thiết bị đều có file đại diện và được đặt tên nhất định :
    - `cdrom` : đĩa CDROM / DVD
    - `hd*` : ổ đĩa IDE , ATA
        - `hda` : ổ cứng thứ nhất
        - `hdb` :	ổ cứng thứ hai
            - `hdb1` : phân vùng thứ nhất của ổ cứng thứ nhất    
    - `sd*` : ổ đĩa SCSI , SATA ( SSD , HDD ) , USB
        - `sda` : ổ cứng thứ nhất
        - `sdb` :	ổ cứng thứ hai
            - `sdb1` : phân vùng thứ nhất của ổ cứng thứ nhất
    - `nvme0*` : ổ cứng SSD NVMe
        - `nvme0n1` : ổ nvme thứ nhất
        - `nvme0n2` : ổ nvme thứ hai
            - `nvme0n2p1` : phân vùng thứ nhất của ổ nvme thứ nhất
    - `tty*` : cổng giao tiếp ( COM ,...)
    - `eth*`: cổng Ethernet

## 5) /etc
- Chứa các tệp cấu hình hệ thống và các tệp cấu hình ứng dụng. Thư mục này không chứa các tệp thực thi. Ví dụ: `passwd, fstab, hosts, network/interface`

## 6) /home 
- Chứa thư mục cá nhân của từng người dùng. Mỗi người dùng có một thư mục con trong `/home` và có thể lưu trữ các tệp cá nhân và cấu hình riêng biệt. Ví dụ: `/home/user1, /home/user2`

## 7) /lib
- Chứa các thư viện chia sẻ cần thiết cho các chương trình trong `/bin` và `/sbin`. Thư mục này cũng chứa các mô-đun kernel. Ví dụ: `libc.so.6`, `libm.so.6`.

## 8) /media 
- Thư mục này có vai trò như đích đến của quá trình mount point . Khi gắn 1 thiết bị lưu trữ bên ngoài, để sử dụng cần mount thiết bị này vào 1 thư mục trong `/media` , từ đó , các thư mục , tập tin sẽ được chuyển vào đây ( lúc này `/media` có thể coi như ảnh chiếu của các thiết bị ).

## 9) /mnt 
- Dùng để gắn kết tạm thời các hệ thống tập tin. Thường được sử dụng bởi quản trị viên hệ thống để gắn kết các thiết bị lưu trữ hoặc phân vùng khác. Ví dụ: `/mnt/external_drive`.

## 10) /opt
- Chứa các phần mềm bổ sung và các gói phần mềm tùy chọn được cài đặt bởi người dùng. Ví dụ: `/opt/my_software`.

## 11) /sbin
- Cũng giống như `/bin`, `/sbin` cũng chứa tập tin thực thi nhị phân .
- Những lệnh trong thư mục này chỉ được dùng bởi người quản trị hệ thống - tương đương user `root` .

## 12) /srv 
- Chứa các dữ liệu liên quan đến các dịch vụ do hệ thống cung cấp, chẳng hạn như các trang web hoặc các tệp phục vụ bởi FTP. Ví dụ: `/srv/www`, `/srv/ftp`.

## 13) /tmp
- Chứa các tệp tạm thời. Các tệp trong thư mục này thường bị xóa khi hệ thống khởi động lại. 

## 14) /usr
- Chứa các ứng dụng người dùng và các tệp hệ thống dùng chung. Đây là một trong những thư mục lớn nhất và chứa nhiều thư mục con như:
    - `/usr/bin`: Chứa các chương trình thực thi của người dùng.
    - `/usr/sbin`: Chứa các chương trình quản trị hệ thống.
    - `/usr/lib`: Chứa các thư viện chia sẻ cho các chương trình trong `/usr/bin` và `/usr/sbin`.
    - `/usr/local`: Chứa các chương trình cài đặt thủ công không phải qua hệ thống quản lý gói.
    - `/usr/share`: Chứa các dữ liệu dùng chung như tài liệu, file cấu hình, và các tệp đa phương tiện.

## 15) /var
- Chứa các tệp thay đổi thường xuyên như log hệ thống, dữ liệu mail, dữ liệu cơ sở dữ liệu. Ví dụ:
    - `/var/log`: Chứa các tệp log.
    - `/var/mail`: Chứa thư điện tử của hệ thống.
    - `/var/spool`: Chứa các tệp hàng đợi xử lý như thư, công việc in ấn.
    - `/var/tmp`: Chứa các tệp tạm thời cần giữ qua quá trình khởi động lại.
## File ẩn
- Tệp ẩn là các tệp hoặc thư mục có tên bắt đầu bằng dấu chấm (.). Ví dụ: ``.bashrc`, ``.config`, ``.hidden_directory`.
## Đường dẫn tuyệt đối và đường dẫn tương đối
- Đường dẫn tuyệt đối bắt đầu từ thư mục gốc / và cung cấp đường dẫn đầy đủ từ thư mục gốc đến thư mục hoặc tệp cụ thể. Nó không phụ thuộc vào vị trí hiện tại của bạn trong hệ thống tập tin. Ví dụ:
    - `/home/user1/documents/report.txt`: Đây là đường dẫn tuyệt đối đến tệp report.txt nằm trong thư mục documents của người dùng user1.
    - `/var/log/syslog`: Đây là đường dẫn tuyệt đối đến tệp log hệ thống syslog.
- Đường dẫn tương đối bắt đầu từ thư mục hiện tại của bạn và chỉ định đường dẫn từ vị trí hiện tại đến thư mục hoặc tệp mục tiêu. Đường dẫn này thay đổi dựa trên vị trí hiện tại của bạn trong hệ thống tập tin. Ví dụ:
    - Nếu bạn đang ở trong thư mục `/home/user1` và bạn muốn truy cập `report.txt` trong thư mục `documents`, bạn có thể sử dụng đường dẫn tương đối: `documents/report.txt`
    - Nếu bạn đang ở trong thư mục `/var`, bạn có thể truy cập `syslog` trong thư mục log bằng đường dẫn tương đối: `log/syslog`

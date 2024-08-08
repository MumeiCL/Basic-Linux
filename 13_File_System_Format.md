# **Cơ chế Journaling**
- Journaling là một cơ chế được sử dụng trong một số hệ thống file để cải thiện tính ổn định và độ tin cậy của hệ thống bằng cách ghi lại các thay đổi trước khi chúng được thực hiện trên chính hệ thống file. Cơ chế này giúp ngăn ngừa sự hỏng hóc của hệ thống file trong trường hợp có sự cố như mất điện, hệ thống bị treo, hoặc các sự cố khác.

    <img src=https://i.imgur.com/Fpmp25D.png>

- **Journaling** chỉ được sử dụng khi ghi dữ liệu lên ổ cứng và đóng vai trò như những chiếc đục lỗ để ghi thông tin vào phân vùng . Đồng thời , nó cũng khắc phục vấn đề xảy ra khi ổ cứng gặp lỗi trong quá trình này , nếu không có **journal** thì hệ điều hành sẽ không thể biết được file dữ liệu có được ghi đầy đủ tới ổ cứng hay chưa .
- Cách hoạt động của Journaling:
  - Ghi vào Journal: Khi có một thay đổi cần được thực hiện trên hệ thống file (như tạo, xóa, hoặc thay đổi dữ liệu của file), hệ thống đầu tiên sẽ ghi lại các thay đổi này vào một khu vực đặc biệt gọi là "journal" (nhật ký).
  - Xác nhận Journal: Sau khi ghi vào journal, hệ thống xác nhận rằng các thay đổi đã được ghi nhận thành công.
  - Thực hiện Thay đổi: Hệ thống sau đó thực hiện các thay đổi thực tế trên chính hệ thống file.
  - Xóa Journal: Sau khi các thay đổi đã được thực hiện thành công trên hệ thống file, các bản ghi trong journal liên quan đến các thay đổi này sẽ được xóa đi, giải phóng không gian.
- Tuy nhiên , nhược điểm của việc sử dụng **journaling** là phải “đánh đổi” hiệu suất trong việc ghi dữ liệu với tính ổn định . Bên cạnh đó , còn có nhiều công đoạn khác để ghi dữ liệu vào ổ cứng nhưng với **journal** thì quá trình không thực sự là như vậy. Thay vào đó thì chỉ có *file metadata* ,  *inode* hoặc *vị trí của file* được ghi lại trước khi thực sự ghi vào ổ cứng.
## **Các kiểu file system trên Linux**
### **1) `ext` - extended file system**
- Là định dạng file hệ thống đầu tiên được thiết kế dành riêng cho Linux .
- Là phần nâng cấp từ file hệ thống **Minix** .
- Không nên sử dụng `ext` vì có nhiều hạn chế , không còn được hỗ trợ trên nhiều distribution.
### **2) `ext2`**
- Thực chất không phải là file hệ thống ***journaling*** , được phát triển để kế thừa các thuộc tính của file system cũ .
- Ext2 không sử dụng ***journal*** cho nên sẽ có ít dữ liệu được ghi vào ổ đĩa hơn .
- Hỗ trợ volume size lên đến `2-32TiB`
- Hỗ trợ file size lên đến `16GiB-2TiB`
- Có thể chứa tối đa 10<sup>18</sup> file trong 1 volume .
- Độ dài tên file tối đa là `255` kí tự .
### **3) `ext3`**
- Là `ext2` đi kèm với ***journaling*** .
- Mục đích chính của `ext3` là tương thích ngược với `ext2` , và do vậy những ổ đĩac, phân vùng có thể dễ dàng được chuyển đổi giữa 2 chế độ mà không cần phải format như trước kia .
- `Ext3` là hoạt động nhanh , ổn định hơn rất nhiều .
- Không thực sự phù hợp để làm file system dành cho máy chủ bởi vì không hỗ trợ tính năng tạo **disk snapshot** và file được khôi phục sẽ rất khó để xóa bỏ sau này .
- Hỗ trợ volume size lên đến `4-32 TiB`
- Hỗ trợ file size lên đến `16GiB-2TiB`
- Độ dài tên file tối đa là `255` kí tự .
### **4) `ext4`**
- File system này ra đời từ phiên bản `2.6.28` của Linux kernel ( 25-12-2008 )
- Nó kế thừa và phát huy các điểm mạnh của `ext3` , đồng thời `ext4` có thể giảm bớt hiện tượng phân mảnh dữ liệu trong ổ cứng , hỗ trợ file system và file có dung lượng lớn và có tốc độ hoạt động nhanh .
- Hỗ trợ volume size lên đến `1 EiB`
- Hỗ trợ file size lên đến `16 TiB`
- Có thể chứa tối đa `4 tỷ` file trong 1 volume .
- Độ dài tên file tối đa là `255` kí tự .
### **5) `xfs`**
- Đây là **file system** mặc định trên CentOS 7
- Được phát triển bởi ***Silicon Graphics*** từ nằm 1993
- Có các đặc điểm :
    - Hạn chế được tình trạng phân mảnh dữ liệu
    - Hỗ trợ volume size lên đến `8 exbibytes`
    - Hỗ trợ file size lên đến `8 exbibytes`
    - Có thể chứa tối đa 2<sup>64</sup> file trong 1 volume .
    - Độ dài tên file tối đa là `255` kí tự .
    - Cấu trúc thư mục theo dạng **B+ trees**
### **6) `Reiser4 - ReiserFS`**
- Có thể coi là 1 trong những bước tiến lớn nhất của file system Linux , lần đầu được công bố vào năm `2001` với nhiều tính năng mới mà file hệ thống `Ext` khó có thể đạt được .
- Đến năm `2004` , `ReiserFS` đã được thay thế bởi `Reiser4 ` với nhiều cải tiến hơn nữa . 
- Không hỗ trợ đầy đủ hệ thống kernel của Linux . 
- Đạt hiệu suất hoạt động rất cao đối với những file nhỏ như file log , phù hợp với database và server email .
### **7) `Btrfs`**
- Thường phát âm là `Butter` hoặc `Better FS` , hiện tại vẫn đang trong giai đoạn phát triển bởi **Oracle** và có nhiều tính năng giống với `ReiserFS` . Đại diện cho **B-Tree File System** , hỗ trợ tính năng pool trên ổ cứng , tạo và lưu trữ snapshot , nén dữ liệu ở mức độ cao , chống phân mảnh dữ liệu nhanh chóng... được thiết kế riêng biệt dành cho các doanh nghiệp có quy mô lớn .
- Mặc dù `BtrFS` không hoạt động ổn định trên 1 số nền tảng distro nhất định , nhưng cuối cùng thì nó vẫn là sự thay thế mặc định của `Ext4` và cung cấp chế độ chuyển đổi định dạng nhanh chóng từ `Ext3/4` . Do vậy, `BtrFS` rất phù hợp để hoạt động với server dựa vào hiệu suất làm việc cao , khả năng tạo snapshot nhanh chóng cũng như hỗ trợ nhiều tính năng đa dạng khác .
### **8) `Jfs`**
- `JFS` được **IBM** phát triển lần đầu tiên năm `1990` , sau đó chuyển sang Linux . 
- Điểm mạnh rất dễ nhận thấy của `JFS` là tiêu tốn ít tài nguyên hệ thống , đạt hiệu suất hoạt động tốt với nhiều file dung lượng lớn và nhỏ khác nhau . Các phân vùng `JFS` có thể thay đổi kích thước được nhưng lại không thể shrink như `ReiserFS` và `XFS` , tuy nhiên nó lại có tốc độ kiểm tra ổ đĩa nhanh nhất so với các phiên bản `Ext` .
### **9) `Zfs`**
- `ZFS` hiện tại vẫn đang trong giai đoạn phát triển bởi **Oracle** với nhiều tính năng tương tự như `Btrfs` và `ReiserFS` .
- Phụ thuộc vào thỏa thuận điều khoản sử dụng , **Sun CDDL** thì `ZFS` không tương thích với hệ thống kernel của Linux , tuy nhiên vẫn hỗ trợ toàn bộ Linux’s Filesystem in Userspace 

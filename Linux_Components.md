# Cấu trúc hệ điều hành Linux

- Kiến trúc hệ điều hành Linux chia thành 3 phần : Kernel , Shell , Application
<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230918130118/linux.jpg">

## 1. Kernel (Nhân)

- Là phần quan trọng và được ví như trái tim của HĐH, phần kernel chứa các module, thư viện để quản lý và giao tiếp với phần cứng và các ứng dụng.
  - **Quản lý tài nguyên phần cứng:** Kernel quản lý và điều phối sử dụng các tài nguyên phần cứng như bộ nhớ, CPU, ổ đĩa, thiết bị ngoại vi và mạng.
  - **Hỗ trợ hệ thống tệp:** Kernel cung cấp các dịch vụ để quản lý các hệ thống tệp, bao gồm tạo, đọc, ghi và xoá tệp, cũng như quản lý quyền truy cập.
  - Quản lý tiến trình: Kernel quản lý việc tạo, điều phối vầ chấm dứt các tiến trình trên hệ thống.
  - **Hỗ trợ giao tiếp và mạng:** Kernel cung cấp giao diện để giao tiếp giữa các ứng dụng và thiết bị, cũng như hỗ trợ các giao thức mạng như TCP/IP.
  - **Bảo mật:** Kernel cung cấp các tính năng bảo mật như quản lý quyền truy cập, kiểm soát truy cập tài nguyên và cơ chế tự bảo vệ.

- Các loại kernel:
  - **Microkernel:** Microkernel có đầy đủ các tính năng cần thiết để quản lý bộ vi xử lý , bộ nhớ và IPC . Có rất nhiều thứ khác trong máy tính có thể được nhìn thấy, tiếp xúc và quản lý trong chế độ người dùng . Microkernel có tính linh hoạt khá cao, vì vậy bạn không phải lo lắng khi thay đổi 1 thiết bị nào đó , ví dụ như card màn hình , ổ cứng lưu trữ... hoặc thậm chí là cả hệ điều hành . Microkernel với những thông số liên quan footprint rất nhỏ , tương tự với bộ nhớ và dung lượng lưu trữ , chúng còn có tính bảo mật khá cao vì chỉ định rõ ràng những tiến trình nào hoạt động trong chế độ user mode , mà không được cấp quyền như trong chế độ giám sát-supervisor mode.
  - **Monolithic Kernel:**  Với Monolithic thì khác , chúng có chức năng bao quát rộng hơn so với microkernel , không chỉ tham gia quản lý bộ vi xử lý , bộ nhớ , IRC , chúng còn can thiệp vào trình điều khiển driver, tính năng điều phối file hệ thống , các giao tiếp qua lại giữa server... Monolithic tốt hơn khi truy cập tới phần cứng và đa tác vụ , bởi vì nếu 1 chương trình muốn thu thập thông tin từ bộ nhớ và các tiến trình khác , chúng cần có quyền truy cập trực tiếp và không phải chờ đợi các tác vụ khác kết thúc . Nhưng đồng thời , chúng cũng là nguyên nhân gây ra sự bất ổn vì nhiều chương trình chạy trong chế độ supervisor mode hơn , chỉ cần 1 sự cố nhỏ cũng khiến cho cả hệ thống mất ổn định . Linux sử dụng kernel này.
  - **Hybrid Kernel:** Khác với 2 loại kernel trên , Hybrid có khả năng chọn lựa và quyết định những ứng dụng nào được phép chạy trong chế độ user hoặc supervisor . Thông thường, những thứ như driver và file hệ thống I/O sẽ hoạt động trong chế độ user mode trong khi IPC và các gói tín hiệu từ server được giữ lại trong chế độ supervisor . Tính năng này thực sự rất có ích vì chúng đảm bảo tính hiệu quả của hệ thống , phân phối và điều chỉnh công việc phù hợp, dễ quản lý . Windows và Mac OS X sử dụng kernel này.
  
- Cách kiểm tra phiên bản kernel hiện tại: 
    ```
    ~$ uname -r 
    6.5.0-41-generic
    ```
    - Trong đó: 
        - `6`: phiên bản chính. Đây là một thay đổi lớn trong kernel, thường đại diện cho các cải tiến quan trọng, tính năng mới, hoặc thay đổi kiến trúc so với các phiên bản trước đó.
        - `5`: phiên bản phụ. Số này phản ánh các cải tiến hoặc thay đổi quan trọng hơn phiên bản chính, nhưng không phải là bản phát hành lớn.
        - `0`: phiên bản phụ của bản phát hành. Phiên bản phụ của bản phát hành (patch level). Đây là số chỉ các bản sửa lỗi, bản vá, hoặc các cải tiến nhỏ hơn cho phiên bản phụ.
        - `41`: số bản phát hành hoặc cập nhập cụ thể cho kernel 6.5.0.
        - `generic`: Loại kernel phổ biến, được thiết kế để hoạt động trên nhiều loại phần cứng khác nhau mà không cần tối ưu hóa cho phần cứng hoặc mục đích cụ thể.
- Cung cấp thông tin về hệ thống bao gồm phiên bản kernel, kiến trúc, và thông tin máy chủ.
  ```
  ~$ hostnamectl
  Static hostname: Mumei-virtual-machine
       Icon name: computer-vm
         Chassis: vm
      Machine ID: 8052b1734f5446db9ad9f399d7354fef
         Boot ID: 776b40d4b9474a0d963e593b3e3892fa
  Virtualization: vmware
  Operating System: Ubuntu 22.04.4 LTS              
          Kernel: Linux 6.5.0-41-generic
    Architecture: x86-64
  Hardware Vendor: VMware, Inc.
  Hardware Model: VMware Virtual Platform
  ```

## 2. Shell
- **Shell** là 1 chương trình có chức năng thực thi các command từ người dùng hoặc từ các ứng dụng - tiện ích yêu cầu chuyển đến cho **Kernel** xử lý .
- Hoạt động của **shell** : *phân tích cú pháp lệnh -> thông dịch yêu cầu của lệnh -> truyền thông điệp tới kernel -> nhận kết quả trả về từ kernel và hiển thị ra màn hình kết quả của lệnh*.
- Bên cạnh đó , **Shell** còn có khả năng bảo vệ **Kernel** từ các yêu cầu không hợp lệ .
- Có các loại **shell** : 
    - ***sh ( the Bourne Shell )*** : đây là **shell** nguyên thủy của **UNIX** được viết bởi Stephen Bourne vào năm `1974` . Đến nay **shell sh** vẫn được sử dụng rộng rãi . **sh** đơn giản, dung lượng nhỏ, ít tính năng nhất so với các Shell ra đời sau này . **sh** thiếu hẳn các tính năng cần thiết như:
        - Tự động hoàn thành tên file , câu lệnh . Tức là , bạn chỉ cần gõ vào ký tự đầu của file , tên lệnh và nhấn phím Tab thì Shell đưa ra 1 số tên file , câu lệnh bắt đầu bằng ký tự đó .
        - Lưu lại các câu lệnh đã gõ vào bộ nhớ ( `history` ) và cho phép duyệt , chỉnh sửa hoặc sử dụng lại các câu lệnh này .
    - ***bash ( Bourne-again Shell )*** : là **shell** mặc định trên **Linux** được viết bởi **Brian Fox** và **Chet Ramey** cho dự án **GNU** ( mục đích của **GNU** là phát triển 1 hệ điều hành hoàn toàn miễn phí, toàn diện, hiệu năng cao và tương thích với Unix ) . **Bash** được cải tiến từ **sh** , nó hỗ trợ nhiều câu lệnh hơn .
    - ***csh ( the C shell )*** : **shell** được viết bằng ngôn ngữ lập trình C , được viết bởi Bill Joy năm `1978` - ông chính là tác giả của trình soạn thảo văn bản `vi` nổi tiếng và sau này là đồng sáng lập ***Sun Microsystems*** .
    - Ngoài ra còn có các loại **shell** khác như ***ash ( the Almquist shell )*** , ***tsh ( the TENEX shell )*** , ***zsh ( the Z shell )*** .
- Dấu nhắc **shell** ( **shell prompt** ) : là 1 ký tự hoặc 1 tập ký tự luôn đứng tại điểm bắt đầu của bất kỳ dòng lệnh nào , nó ám chỉ rằng Shell đã sẵn sàng nhận lệnh từ người dùng . `Shell prompt` thường kết thúc với ký tự `$` cho người dùng thông thường và ký tự `#` cho user `root` .
    ```
    mumei@Mumei-virtual-machine:~$
    root@Mumei-virtual-machine:~#
    ```
## 3. Applications
- Là các chương trình phần mềm được thiết kế để thực hiện các nhiệm vụ cụ thể hoặc cung cấp các dịch vụ cho người dùng
- Các ứng dụng Linux có thể bao gồm các công cụ văn phòng như bộ xử lý văn bản, bảng tính và trình soạn thảo văn bản; các ứng dụng trình duyệt web, email và tin nhắn...

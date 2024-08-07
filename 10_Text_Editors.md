# Text Editors
## 1) Nano
- Nano là một trình soạn thảo văn bản đơn giản nhưng mạnh mẽ, được sử dụng phổ biến trong môi trường Unix và Linux.
- Nano rất dễ sử dụng với giao diện thân thiện. Các lệnh chính được hiển thị ở cuối màn hình, giúp người dùng dễ dàng thao tác.
- cú pháp: `nano [OPTIONS] [[+LINE[,COLUMN]] FILE]...`
- Nano hỗ trợ nhiều OPTIONS để tùy chỉnh hành vi của nó:
    - `-h, --help`: Hiển thị trợ giúp.
    - `-I, --ignorercfiles`: Bỏ qua tệp cấu hình nanorc.
    - `-B, --backup`: Tạo bản sao lưu của tệp trước khi lưu thay đổi.
    - `-E, --tabstospaces`: Chuyển đổi các tab thành dấu cách.
    - `-K, --keypad`: Kích hoạt bàn phím số.
    - `-m, --mouse`: Bật chế độ sử dụng chuột.
    - `-v, --view`: Chế độ xem chỉ đọc, không cho phép chỉnh sửa.
    - `-z, --suspendable`: Cho phép dừng (suspend) nano bằng tổ hợp phím Ctrl+Z.
- Các lệnh tương tác chính trong nano:
  - Ctrl + G: Hiển thị trợ giúp.
  - Ctrl + O: Lưu tệp.
  - Ctrl + X: Thoát nano.
  - Ctrl + K: Cắt dòng hiện tại.
  - Ctrl + U: Dán nội dung đã cắt.
  - Ctrl + W: Tìm kiếm văn bản.
  - Ctrl + \: Thay thế văn bản.
- Nano cho phép tùy chỉnh qua tệp cấu hình .nanorc. Một số tùy chọn cấu hình thông dụng:
  - set autoindent: Tự động thụt đầu dòng.
  - set tabsize 4: Thiết lập kích thước tab là 4 ký tự.
  - set linenumbers: Hiển thị số dòng.
Để biết thêm chi tiết, bạn có thể xem toàn bộ trang man của nano bằng cách sử dụng lệnh man nano trong terminal. 

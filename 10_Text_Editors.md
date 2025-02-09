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
## 2) Vi
Vi là một trình soạn thảo văn bản mạnh mẽ có sẵn trên hầu hết các hệ điều hành Linux/Unix. Nó hoạt động theo nhiều chế độ khác nhau, giúp chỉnh sửa file nhanh chóng nhưng yêu cầu người dùng làm quen với các lệnh.

- Vi hoạt động với 3 chế độ chính:
    - Normal Mode : Dùng để điều hướng, xóa, sao chép, dán...	Nhấn Esc
    - Insert Mode : Nhấn i, a, o, O
    - Command Mode :Dùng để thực hiện lệnh như lưu, thoát, tìm kiếm, thay thế... Nhấn : trong Normal Mode

### Điều hướng trong Vi
- Khi ở Normal Mode, bạn có thể di chuyển con trỏ bằng các phím sau:
    - h	Di chuyển sang trái
    - l	Di chuyển sang phải
    - k	Di chuyển lên trên
    - j	Di chuyển xuống dưới
    - w	Nhảy đến từ tiếp theo
    - b	Quay lại đầu từ trước đó
    - 0	Di chuyển về đầu dòng
    - ^	Về đầu dòng (bỏ khoảng trắng)
    - $	Di chuyển về cuối dòng
    - G	Đến cuối file
    - gg	Đến đầu file
    - nG	Đến dòng thứ n
### Chỉnh sửa nội dung
**Vào chế độ Insert Mode để nhập văn bản**
- i Chèn văn bản ngay trước con trỏ
- I Chèn văn bản đầu dòng
- a Chèn văn bản ngay sau con trỏ
- A Chèn văn bản cuối dòng
- o Tạo dòng mới bên dưới và nhập văn bản
- O Tạo dòng mới bên trên và nhập văn bản

**Xóa nội dung**
- x Xóa ký tự tại con trỏ
- X Xóa ký tự trước con trỏ
- dw Xóa một từ
- d$ Xóa từ vị trí con trỏ đến cuối dòng
- dd Xóa cả dòng
- D Xóa từ vị trí con trỏ đến cuối dòng
- dG Xóa từ dòng hiện tại đến cuối file
- dgg Xóa từ dòng hiện tại đến đầu file
**Sao chép, cắt, dán**
- yy Sao chép dòng hiện tại
- nyy Sao chép n dòng
- p Dán nội dung sau con trỏ
- p Dán nội dung trước con trỏ
- dd Cắt (xóa) dòng hiện tại
- ndd Cắt (xóa) n dòng
**Hoàn tác**
- u Hoàn tác (Undo)
= Ctrl + r Làm lại (Redo)
## Tìm kiếm và thay thế
- /từ_cần_tìm Tìm kiếm xuống dưới
- ?từ_cần_tìm Tìm kiếm lên trên
- n	Tới kết quả tiếp theo
- N	Tới kết quả trước đó
- :s/old/new/ Thay "old" bằng "new" trên dòng hiện tại
- :s/old/new/g Thay tất cả "old" trên dòng hiện tại
- :%s/old/new/g Thay tất cả "old" trong file
- :%s/old/new/gc Hỏi trước khi thay từng cái
## Lưu và thoát Vi
- :w Lưu file
- :q Thoát nếu không có thay đổi
- :wq hoặc ZZ Lưu và thoát
- :q! Thoát không lưu
## Mở nhiều file cùng lúc
- vi file1 file2 Mở nhiều file cùng lúc
- :n Chuyển sang file tiếp theo
- :prev	Chuyển sang file trước đó
- :q Đóng file hiện tại

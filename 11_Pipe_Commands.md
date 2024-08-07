# Pipe Command
-  kết nối đầu ra của một lệnh với đầu vào của lệnh khác.
-  cú pháp: `# command_1 | command_2 | command_3 ...`
-  Ví dụ:
    - `# ls -l | grep 'file'` - `ls -l` liệt kê các tệp và thư mục, và `grep 'file'` lọc danh sách để chỉ hiển thị các tệp hoặc thư mục có chứa từ 'file'.
    - `# cat file.txt | wc -l` - `cat file.txt` hiển thị nội dung của file.txt, và `wc -l` đếm số dòng của nội dung đó.
    - `# grep 'error' /var/log/syslog | sort | uniq ` - `grep 'error' /var/log/syslog`: Tìm kiếm các dòng chứa từ 'error'. `sort`: Sắp xếp kết quả tìm kiếm. `uniq`: Loại bỏ các dòng trùng lặp.

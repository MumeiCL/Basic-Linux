# Inode
- **Inode** ( ***index node*** ) là  là một cấu trúc dữ liệu dùng để lưu trữ thông tin về file và thư mục. Inode không chứa dữ liệu thực tế của file mà chứa **metadata** (siêu dữ liệu) về file.
- Trong 1 **inode** có các metadata sau :
    - **File type** : Loại file (thông thường, thư mục, liên kết mềm, thiết bị, v.v.) 
    - **Permissions** : Quyền truy cập file (đọc, ghi, thực thi) cho chủ sở hữu, nhóm và người dùng khác.
    - **Owner and Group** : ID của chủ sở hữu file và nhóm sở hữu.
    - **File size** : Kích thước file tính bằng byte.
    - Hệ thống phụ và các cờ hạn chế quyền truy cập file
    - **Timestamps** : các mốc thời gian khi : bản thân inode bị thay đổi ( **ctime** ) , nội dung file bị thay đổi ( **mtime** ) và lần truy cập mới nhất ( **atime** )
    - **Link count** : số lượng ***hard link*** trỏ đến **inode** .
    - Các con trỏ ( từ `11` đến `15` con trỏ ) chỉ đến các block trên ổ cứng dùng để lưu nội dung file . Theo các con trỏ này mới biết file nằm ở đâu để đọc nội dung .
- Cách hoạt động của Inode:
  - Tạo file: Khi tạo một file mới, hệ thống file sẽ cấp phát một inode và một hoặc nhiều khối dữ liệu (data block) để lưu trữ dữ liệu của file.
  - Lưu trữ metadata: Metadata của file sẽ được lưu trong inode. Các con trỏ trong inode sẽ trỏ đến các khối dữ liệu chứa nội dung của file.
  - Liên kết giữa tên file và inode: Một thư mục trên hệ thống file thực chất là một bản đồ ánh xạ giữa tên file và inode. Khi bạn liệt kê nội dung của thư mục, hệ thống sẽ đọc các inode để lấy thông tin về các file và thư mục con.
> ***Chú ý*** :<br> - **Inode** không chứa tên file / thư mục<br>- Các con trỏ là thành phần quan trọng nhất : nó cho biết địa chỉ các **block** lưu nội dung file và tìm đến các **block** đó để có thể truy cập vào nội dung file .
- Các lệnh kiểm tra **inode** :
    - Show **số inode** :
        ```
        # ls -i <path/file_name>
        ```
        ![image](https://github.com/user-attachments/assets/edfc805f-fbb2-4ea9-9573-91c67d6d872e)

    - Cho biết chi tiết nội dung **inode**
        ```
        # stat <path/file_name>
        ```
        ![image](https://github.com/user-attachments/assets/8625aeff-ced1-4762-b0b1-8d51ea05a827)

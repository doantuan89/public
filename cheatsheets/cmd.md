# Network
ping -a 192.168.10.123 : lấy tên máy pc khi biết địa chỉ ip 

# Quản lý user login bằng net user 
1. `net user ` xem danh sách tài khoản trên máy tính.
2. `net user Administrator` xem chi tiết tài khoản "Administrator"
3. `net user UserTest 123456 /add` Tạo tài khoản mới
4. `net user UserTest 654321` Đổi mật khẩu của user UserTest thành 654321.

5. `net user UserTest /delete` Xóa tài khoản  

6. Kích hoạt hoặc vô hiệu hóa tài khoản
```
 - net user UserTest /active:yes
 - net user UserTest /active:no
```
 7. `net user %username% * ` Đặt mật khẩu mới cho user hiện tại đang login.
  Windows sẽ yêu cầu nhập mật khẩu mới.
 8. `net localgroup Administrators "Ten User" /add` Chuyển user thường thành admin
  -  Giữ nguyên dấu "" nếu tên user có khoảng trắng.
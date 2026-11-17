# Network
ping -a 192.168.10.123 : lấy tên máy pc khi biết địa chỉ ip 

# Quản lý user login bằng net user 
Mở **cmd với quyền Administrator**
1. xem danh sách tài khoản trên máy tính  
  ```cmd  
    net user
  ``` 

2. xem chi tiết tài khoản "Administrator"
  ```cmd 
  net user Administrator
  ```
3. Tạo tài khoản mới 
```cmd 
net user UserTest 123456 /add
``` 
4. Đổi mật khẩu của user UserTest thành 654321. 
```cmd 
net user UserTest 654321
```

5. Xóa tài khoản  
```cmd 
net user UserTest /delete 
```

6. Kích hoạt hoặc vô hiệu hóa tài khoản
``` cmd
 - net user UserTest /active:yes
 - net user UserTest /active:no
```
 7.Đặt mật khẩu mới cho user hiện tại đang login. 
 ```cmd 
 net user %username% * 
 ```
>Windows sẽ yêu cầu nhập mật khẩu mới.
 
 8. Chuyển user thường thành admin 
 ```cmd 
  net localgroup Administrators "Ten User" /add
```  
>Giữ nguyên dấu "" nếu tên user có khoảng trắng.
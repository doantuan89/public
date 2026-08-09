# Share printer on windows 10 and 11

- Đảm bảo 2 máy ping thấy nhau 
- Tắt mật khẩu khi share file: `Control Panel\Network and Internet\Network and Sharing Center\Advanced sharing settings`

## Trên máy chủ (máy share)

  ````text
  Tên máy chủ:  PC-PD84308 
  ````

  1. Tạo user để share print  
    - net user printuser 123456 /add  
    - net localgroup Administrators "printuser" /add (chuyển sang quyền Administrators)  
    - kiểm tra lại bằng lệnh  "net user printuser"	muc Local Group Memberships
          
  2. Add printuser vao tab Security cua may in Canon LBP2900  
    - Control panel -> Prints and scanners -> Canon LBP2900 -> chon Printer Properties  
    - Chon tab Secturity  
    - add user "printuser"  

## Trên máy khách ( máy đọc dữ liệu)

  1. Thêm  printuser vào `Windows Credentials.  
    - Vào `Control Panel\All Control Panel Items\Credential Manager`
	  - Click Add a Windows credential.  

    ````text
      internet or network address: PC-PD84308
      user: printuser
      password: 123456
    ````
  2.  Add máy in bằng  Local Port.  
	  - Control Panel\Hardware and Sound\Devices and Printers.
	  - Add a local printer or network printer with manual settings  
		- Create a new port  
		- Type of port : Local Port -> next  
		- Port Name: `\\PC-PD84308\printer-buffet (or only namePC PC-PD84308)`
		- next 
	



Quản lý user: 
1. xem danh sách tài khoản trên máy tính. 
  - net user : 
2. xem chi tiết tài khoản "Administrator"
  - net user Administrator: 

3. Tạo tài khoản mới
  - net user test123 123456 /add

4. Đổi mật khẩu
  - net user test123 654321
  Đổi mật khẩu của user test123 thành 654321.

5. Xóa tài khoản  
  -  net user test123 /delete

6. Kích hoạt hoặc vô hiệu hóa tài khoản
 - net user test123 /active:yes
 - net user test123 /active:no

 7. Đặt mật khẩu mới cho user hiện tại
  - net user %username% * 
  Windows sẽ yêu cầu nhập mật khẩu mới.


2. Tài khoản Credential:
- Control Panel\User Accounts\Credential Manager

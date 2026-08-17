# Share Printer trên Windows 10 & 11

Tags [ #printer, #share-printer ]

Hướng dẫn chia sẻ máy in giữa **Windows 10 và Windows 11** trong cùng mạng LAN.

## 1. Điều kiện trước khi cấu hình

* Hai máy phải kết nối cùng mạng LAN.
* Đảm bảo hai máy **ping thấy nhau**.
* Máy khách có thể truy cập máy chủ qua:

```text
\\PC-PD84308
```

### Tắt Password Protected Sharing

Trên máy chủ:

```text
Control Panel
-> Network and Internet
-> Network and Sharing Center
-> Advanced sharing settings
```

Tại **All Networks**:

```text
Password protected sharing
→ Turn off password protected sharing
```

> **Lưu ý:** Nếu sử dụng tài khoản `printuser` để xác thực khi kết nối máy in, có thể giữ **Password protected sharing** ở trạng thái bật. Khi đó máy khách cần lưu thông tin đăng nhập trong **Windows Credentials**.

---

# 2. Cấu hình trên máy chủ

Máy chủ:

```text
PC-PD84308
```

## 2.1. Tạo tài khoản `printuser`

Mở **Command Prompt / Terminal với quyền Administrator**:

```cmd
net user printuser 123456 /add
```

Kiểm tra tài khoản:

```cmd
net user printuser
```

> **Khuyến nghị:** Không nên cấp quyền `Administrators` cho `printuser` nếu chỉ dùng tài khoản này để kết nối máy in. Tài khoản Standard User thường là đủ và an toàn hơn.

---

## 2.2. Share máy in

Trên máy chủ:

```text
Control Panel
→ Hardware and Sound
→ Devices and Printers
```

Chọn:

```text
Canon LBP2900
→ Printer Properties
→ Sharing
```

Bật:

```text
Share this printer
```

Đặt **Share name** dễ nhớ, ví dụ:

```text
printer-buffet
```

Khi đó đường dẫn máy in sẽ là:

```text
\\PC-PD84308\printer-buffet
```

---

## 2.3. Cấu hình quyền truy cập máy in

Trong:

```text
Printer Properties
→ Security
```

Thêm user:

```text
printuser
```

Cấp các quyền cần thiết cho user này, thông thường:

```text
Print
```

là đủ.

> Không cần cấp toàn bộ quyền quản trị máy in nếu user chỉ có nhiệm vụ in tài liệu.

---

# 3. Cấu hình trên máy khách

## 3.1. Lưu thông tin đăng nhập

Trên máy khách mở:

```text
Control Panel
→ All Control Panel Items
→ Credential Manager
→ Windows Credentials
```

Chọn:

```text
Add a Windows credential
```

Nhập:

```text
Internet or network address:
PC-PD84308

User name:
PC-PD84308\printuser

Password:
123456
```

> Nên ghi đầy đủ `PC-PD84308\printuser` thay vì chỉ `printuser` để Windows xác định chính xác tài khoản trên máy chủ.

---

# 4. Thêm máy in bằng Local Port

Trên máy khách:

```text
Control Panel
→ Hardware and Sound
→ Devices and Printers
→ Add a printer
```

Chọn:

```text
The printer that I want isn't listed
```

Sau đó:

```text
Add a local printer or network printer with manual settings
```

Chọn:

```text
Create a new port
```

Tại:

```text
Type of port:
Local Port
```

Nhấn **Next**.

### Port Name

Nhập chính xác đường dẫn share của máy in:

```text
\\PC-PD84308\printer-buffet
```

Sau đó:

```text
Next
```

Windows sẽ sử dụng đường dẫn UNC này làm Local Port để gửi dữ liệu in tới máy chủ.

---

# 5. Chọn driver máy in

Khi Windows yêu cầu driver:

```text
Manufacturer:
Canon
```

Chọn đúng driver:

```text
Canon LBP2900
```

Nếu máy khách chưa có driver, cài driver Canon LBP2900 trước rồi thực hiện lại bước tạo Local Port.

---

# 6. Kiểm tra kết nối

Trên máy khách, mở:

```text
Run
```

hoặc nhấn:

```text
Win + R
```

Nhập:

```text
\\PC-PD84308
```

Nếu kết nối thành công, Windows sẽ hiển thị các tài nguyên đang được share trên máy chủ.

Kiểm tra máy in:

```text
\\PC-PD84308\printer-buffet
```

Sau đó thử **Print Test Page**.

---

# 7. Tóm tắt

### Máy chủ

```text
PC-PD84308
│
├── User: printuser
│
├── Printer: Canon LBP2900
│
└── Share name: printer-buffet
```

Đường dẫn máy in:

```text
\\PC-PD84308\printer-buffet
```

### Máy khách

```text
Windows Credentials
└── PC-PD84308\printuser
```

Local Port:

```text
\\PC-PD84308\printer-buffet
```

### Kiểm tra nhanh

```cmd
ping PC-PD84308
```

```text
\\PC-PD84308
```

```text
\\PC-PD84308\printer-buffet
```

---
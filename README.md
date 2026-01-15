# Flash Tool - Hệ thống Nạp Firmware Công nghiệp

## 1. Tổng quan
Flash Tool là giải pháp phần mềm chuyên dụng được thiết kế nhằm tối ưu hóa quy trình nạp Firmware hàng loạt cho các thiết bị nhúng chạy hệ điều hành OpenWrt hoặc các hệ thống Linux tương đương. Ứng dụng tích hợp công nghệ nạp đa luồng giúp rút ngắn thời gian sản xuất và đảm bảo độ chính xác tuyệt đối thông qua cơ chế kiểm soát tiến trình thời gian thực.

## 2. Tính năng cốt lõi

### 2.1. Động cơ nạp Firmware (Core Engine)
- **Giao thức truyền tải:** Sử dụng tổ hợp SSH (Paramiko) và SCP để truyền dữ liệu mã hóa, đảm bảo tính vẹn toàn cho gói Firmware.
- **Hỗ trợ Telnet:** Tự động kích hoạt quyền truy cập SSH thông qua xác thực Telnet âm thầm (Silent Authentication).
- **Cơ chế nạp đa luồng (Multi-threading):** Khởi tạo tiến trình nạp riêng biệt, cho phép thiết bị hoạt động liên tục mà không gây treo giao diện người dùng (UI).
- **Phản hồi thời gian thực:** Nhận diện các tín hiệu từ hệ thống (`sysupgrade`, `mtd`) để thông báo thời điểm an toàn khi ngắt kết nối thiết bị.

### 2.2. Quản lý sản lượng và Dữ liệu (Production Management)
- **Bộ đếm vĩnh viễn (Persistent Counter):** Theo dõi số lượng thiết bị nạp thành công và lưu trữ trực tiếp vào tệp cấu hình (`config.json`). Dữ liệu không bị mất khi thoát ứng dụng.
- **Tùy chỉnh linh hoạt:** Cho phép đặt lại (Reset) bộ đếm khi bắt đầu dự án mới hoặc hiệu chỉnh bằng tay (Manual Edit) số lượng mạch đã nạp.
- **Quản lý Profile:** Hỗ trợ lưu trữ cấu hình riêng biệt (IP, Username, Password, Firmware Path) cho từng model thiết bị khác nhau.

### 2.3. Hệ thống Nhật ký (Logging System)
- **Real-time Log:** Hiển thị trực quan tiến trình nạp với các mã màu quy ước (Thành công, Cảnh báo, Lỗi).
- **Nhật ký tệp (Daily File Logs):** Tự động khởi tạo tệp nhật ký hàng ngày trong thư mục `logs/` theo định dạng `flash_YYYY-MM-DD.log`.
- **Phân tách dữ liệu:** Sử dụng số thứ tự Board và đường kẻ phân cách để quản lý nhật ký giữa các lượt nạp khác nhau một cách khoa học.

### 2.4. Giao diện người dùng cao cấp (Premium UI/UX)
- **Công nghệ hiển thị:** Xây dựng trên nền tảng CustomTkinter với phong cách Dark Mode hiện đại.
- **Kiến trúc Tàng hình (Ghost Initialization):** Loại bỏ hoàn toàn hiện tượng chớp trắng (white flicker) khi khởi động ứng dụng trên Windows.
- **Typography:** Sử dụng font chữ **Inter** (phong cách Gemini/Google) tối ưu cho khả năng đọc và độ thẩm mỹ chuyên nghiệp.
- **Hệ thống Dialog tùy chỉnh:** Các hộp thoại thông báo và nhập liệu được thiết kế đồng bộ với theme hệ thống và tự động căn giữa ứng dụng.

## 3. Hướng dẫn vận hành

### Bước 1: Thiết lập Firmware
Nhấn nút **"Flash from file"** để chọn tệp nguồn (.img, .bin). Đường dẫn sẽ được lưu tự động cho các lần khởi động sau.

### Bước 2: Lựa chọn thiết bị (Target)
Chọn Model thiết bị từ Menu thả xuống. App sẽ tự động nạp các thông số IP và thông tin xác thực (SSH) tương ứng với Model đó. Có thể điều chỉnh chi tiết trong mục **Settings (⚙)**.

### Bước 3: Thực thi nạp (Action)
Nhấn nút **"Flash!"** để bắt đầu quy trình. 
- Quan sát bảng điều khiển: Trạng thái thiết bị sẽ hiển thị "Ready" khi sẵn sàng.
- Khi Log thông báo **"AN TOÀN: BẠN CÓ THỂ RÚT CÁP LAN NGAY!"**, quy trình nạp cho thiết bị đó đã hoàn tất.
- Rút thiết bị cũ, kết nối thiết bị mới. Hệ thống sẽ tự động nhận diện và nạp lượt tiếp theo.

## 4. Yêu cầu hệ thống

- **Hệ điều hành:** Windows 10/11 (Đối với bản EXE đóng gói).
- **Môi trường phát triển (nếu chạy từ source):** 
  - Python 3.10 trở lên.
  - Thư viện: `customtkinter`, `paramiko`, `scp`, `pillow`.

## 5. Cấu trúc thư mục Log
```text
logs/
 └── flash_2024-01-15.log  <-- Nhật ký chi tiết của ngày nạp
data/
 └── profiles.json         <-- Định nghĩa các dòng Board hỗ trợ
config.json               <-- Lưu trữ cấu hình người dùng và số lượng sản phẩm
```



# Flash Tool - Hệ thống Nạp Firmware

## 1. Tổng quan
Flash Tool là phần mềm hỗ trợ nạp Firmware cho các thiết bị chạy hệ điều hành OpenWrt hoặc các hệ thống Linux tương đương thông qua mạng LAN. Ứng dụng hỗ trợ quy trình nạp tự động đa luồng và quản lý dữ liệu sản xuất.

## 2. Danh mục tính năng
- **Truyền tải dữ liệu:** Sử dụng giao thức SSH/SCP (thư viện Paramiko) và hỗ trợ kích hoạt SSH qua Telnet.
- **Xử lý đa luồng:** Khởi tạo tiến trình nạp độc lập cho mỗi thiết bị, không chặn giao diện chính.
- **Theo dõi sản lượng:** Bộ đếm số lượng nạp thành công tự động lưu vào `config.json`, hỗ trợ Reset và chỉnh sửa thủ công.
- **Quản lý cấu hình:** Lưu và tải Profile (IP, thông tin xác thực, đường dẫn Firmware) riêng biệt cho từng loại bo mạch.
- **Nhật ký vận hành:** 
    - Hiển thị theo thời gian thực trên giao diện.
    - Tự động ghi tệp nhật ký hàng ngày (`logs/flash_YYYY-MM-DD.log`).
    - Phân tách nhật ký giữa các phiên làm việc của từng bo mạch.

## 3. Hướng dẫn vận hành

### Bước 1: Thiết lập Firmware
Chọn tệp nguồn bằng nút **"Flash from file"**.

### Bước 2: Lựa chọn thiết bị
Chọn loại bo mạch từ Menu. Chỉnh sửa thông số kết nối (IP, User, Pass) trong mục **Settings (⚙)** nếu cần.

### Bước 3: Thực thi nạp
- Nhấn **"Flash!"** để bắt đầu.
- Trạng thái thiết bị hiển thị "Ready" khi sẵn sàng.
- Khi xuất hiện thông báo **"AN TOÀN: BẠN CÓ THỂ RÚT CÁP LAN NGAY!"**, quy trình nạp đã hoàn tất.
- Kết nối thiết bị tiếp theo để hệ thống tự động nhận diện và nạp lượt mới.

## 4. Đặc tả kỹ thuật
- **Ngôn ngữ:** Python 3.10+
- **Thành phần chính:** `customtkinter`, `paramiko`, `scp`, `pillow`, `socket`.
- **Cơ chế lưu trữ:** JSON (Dữ liệu cấu hình và bộ đếm).
- **Cấu trúc dữ liệu Log:** Theo ngày và số thứ tự thiết bị.

## 5. Cấu trúc tệp tin liên quan
- `logs/`: Thư mục chứa nhật ký chi tiết.
- `data/profiles.json`: Định nghĩa danh mục bo mạch hỗ trợ.
- `config.json`: Lưu trữ cấu hình và số lượng nạp thành công.

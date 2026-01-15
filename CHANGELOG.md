# Nhật ký thay đổi (Changelog) - Flash Tool

Tất cả các cập nhật kỹ thuật và thay đổi kiến trúc của hệ thống Flash Tool được lưu trữ tại đây.

## [2.6.5] - 2026-01-15

### 🚀 Nâng cấp hệ thống Quản lý Sản lượng (Production Yield Tracking)
- **Kiến trúc dữ liệu:** Chuyển đổi trạng thái bộ đếm sang cơ chế lưu trữ bền vững (Persistence). Dữ liệu sản lượng hiện được đồng bộ hóa trực tiếp vào `config.json` theo thời gian thực.
- **Tính năng mở rộng:** Tích hợp công cụ hiệu chỉnh số lượng thủ công (Manual Edit) và cơ chế làm mới bộ đếm (Reset) cho các dự án mới.

### 📜 Cải tiến Hệ thống Nhật ký (Logging System)
- **Quản lý dữ liệu:** Tự động hóa quy trình khởi tạo nhật ký tệp (File Logging) theo ngày.
- **Cấu trúc hiển thị:** Rút gọn định danh luồng (Thread Name), bổ sung số thứ tự phiên bản mạch (Board Index) và biểu tượng phân tách để tối ưu hóa khả năng truy xuất thông tin lỗi.

### 🎨 Tái cấu trúc Giao diện Người dùng (UI/UX Transformation)
- **Hệ thống Thông báo (Themed Dialog System):** Thay thế toàn bộ thành phần `tkinter.messagebox` bằng hệ thống `ConfirmDialog` và `InputWindow` tùy chỉnh, đảm bảo tính đồng nhất về màu sắc (Dark Mode) và vị trí hiển thị (Centered on App).
- **Tối ưu hóa Bố cục (Layout Optimization):** 
    - Chuyển bộ đếm sản lượng xuống khu vực Chân trang (Footer Taskbar) để cân bằng thị giác.
    - Cập nhật Typography sang hệ font **Inter** quy chuẩn, tăng kích thước hiển thị cho các thông số quan trọng.

### 🛠️ Sửa lỗi kỹ thuật và Tăng cường Ổn định
- **Xử lý mạng:** Khắc phục triệt để lỗi xung đột địa chỉ IP khi bind socket thông qua cơ chế tự động xác định IP nội bộ (`get_local_ip`).
- **Xử lý hiển thị:** Loại bỏ hoàn toàn các cấu trúc thừa gây lỗi render (border_width, propagation) và hiện tượng chớp hình khi khởi động.

---

## [2.2.0] - 2026-01-14
- **Giao diện:** Chuyển đổi từ Tkinter truyền thống sang CustomTkinter.
- **Tính năng:** Bổ sung cơ chế chống lỗi nạp khi router ngắt kết nối đột ngột.

## [2.0.2] - 2025-12-20
- Phiên bản ổn định đầu tiên sử dụng giao diện đồ họa.
- Hỗ trợ nạp Firmware qua SCP.

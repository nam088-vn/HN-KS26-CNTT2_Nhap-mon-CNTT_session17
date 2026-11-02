### **Bài 8: Vá Lỗ Hổng Bảo Mật Cookie Bệnh Án Và Khắc Phục Lỗi Cache Thuốc Cũ**

### **PHẦN 1: PHÂN TÍCH LỖ HỔNG & NGUYÊN NHÂN**

#### **1\. Nguyên nhân hiển thị dữ liệu cũ** 

* **Cơ chế:** Trình duyệt lưu bản sao các tệp tĩnh vào bộ nhớ tạm. Khi bác sĩ tải lại trang, trình duyệt tự động đọc lại các tệp này trực tiếp từ máy trạm thay vì gửi yêu cầu HTTP Request đến máy chủ để lấy bản mới.

#### **2\. Hiểm họa bảo mật Cookie thiếu cờ HttpOnly và Secure**

* **Câu lệnh đánh cắp Token :**

* JavaScript

```
const doctorToken = document.cookie;
```

* **Hiểm họa Session Hijacking:**

  * **Thiếu HttpOnly:** Cho phép mã độc XSS đọc trực tiếp document.cookie để lấy carepulse\_doctor\_session.

  * **Thiếu Secure:** Cookie bị truyền qua giao thức HTTP không mã hóa, khiến hacker dễ dàng nghe lén và chộp lấy token.

  * **Hậu quả:** Hacker giả mạo phiên làm việc của bác sĩ để truy cập trái phép, sửa đổi hồ sơ bệnh án hoặc rò rỉ thông tin y tế nhạy cảm.

### **PHẦN 2: GIẢI PHÁP và THAO TÁC DEVTOOLS**

#### **3\. Hướng dẫn Bác sĩ Hard Reload** 

####   Bấm tổ hợp phím Ctrl \+ Shift \+ R để ép trình duyệt bỏ qua Cache và tải lại toàn bộ tài nguyên mới từ máy chủ. 

#### **4\. Dòng lệnh Set-Cookie chuẩn an ninh y tế**

HTTP

```
Set-Cookie: carepulse_doctor_session=TOKEN_XYZ883921983; Domain=carepulse.vn; Path=/; Expires=Wed, 21 Oct 2026 07:00:00 GMT; HttpOnly; Secure; SameSite=Strict
```

#### **5\. 3 bước kiểm tra Cookie và vô hiệu hóa Cache trên DevTools** 

1. Bật F12: Nhấn F12 mở Chrome DevTools.

2. Kiểm tra Cookie: Vào Application $\rightarrow$ Cookies $\rightarrow$ chọn \[https\://carepulse.vn\](https\://carepulse.vn) $\rightarrow$ Kiểm tra tích xanh ở cột HttpOnly và Secure.

3. Vô hiệu hóa Cache : Chuyển sang tab Network $\rightarrow$ Tích chọn ô Disable cache .


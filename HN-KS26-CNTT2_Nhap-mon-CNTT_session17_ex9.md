**Bài 9: Thiết Kế Không Gian Đa Profile Và Kiến Trúc Bookmark Cho Trạm Khám Bệnh**

### **PHẦN 1: BÁO CÁO PHÂN TÍCH KIẾN TRÚC ĐA PROFILE**

#### **1\. Nguyên nhân sâu xa của hiện tượng văng phiên đăng nhập** 

* Trình duyệt Chrome khi chạy một Profile mặc định sẽ lưu toàn bộ Cookies, LocalStorage và Session Data vào duy nhất một thư mục User Data/Default.

* Khi nhiều người cùng dùng các tài khoản khác nhau trên cùng 1 Profile, dữ liệu Cookie phiên làm việc mới sẽ ghi đè lên Cookie cũ của cùng một domain/hệ thống, dẫn đến việc tài khoản đang đăng nhập trước đó bị ngắt kết nối lập tức.

#### **2\. Thiết kế Mô hình 3 Profile chuyên dụng**

* **Profile 1: Công việc**

  * *Mục đích:* Bác sĩ trực chính & Điều dưỡng thực hiện tác nghiệp chuyên môn (Kê đơn, tra cứu bệnh án).

  * *Theme visual:* Xanh dương đậm để tránh nhầm lẫn.

  * *Dữ liệu độc lập:* Lưu Cookies CarePulse, lịch sử khám bệnh, Bookmark y tế, Extensions mật khẩu phòng khám.

* **Profile 2: Cá nhân**

  * *Mục đích:* Nhân viên đăng nhập tài khoản cá nhân trong giờ nghỉ .

  * *Theme visual:* Cam sáng .

  * *Dữ liệu độc lập:* Cookies cá nhân, lịch sử duyệt web riêng, Bookmark mua sắm/giải trí.

* **Profile 3: Thực tập và Kiểm thử**

  * *Mục đích:* Bác sĩ thực tập, sinh viên mượn máy học tập.

  * *Theme visual:* Xám / Đen .

  * *Dữ liệu độc lập:* Cookies học tập cá nhân, lịch sử tra cứu riêng, không chạm vào dữ liệu y tế.

### **PHẦN 2: THIẾT KẾ HỆ THỐNG BOOKMARK & QUY TRÌNH AN TOÀN**

#### **3\. Cấu trúc Cây thư mục Bookmark chuẩn** 

**01\_CarePulse\_Clinic**: Hệ thống Quản lý Phòng khám, Cổng Bệnh án điện tử, Cổng Tiếp nhận dữ liệu BHYT.

**02\_Pharma\_Portal**: Tra cứu Dược thư Quốc gia, Cổng Quản lý Dược , Hệ thống Mã ATC / Biệt dược.

**03\_Medical\_Tools**: Công cụ tính liều lượng thuốc , Bảng phân loại bệnh quốc tế ICD-10, Từ điển Y khoa PubMED.

#### **4\. Kỹ thuật Favicon-Only (Tiết kiệm diện tích gấp 3 lần)**

* **Cách thực hiện:** Click chuột phải vào Bookmark trên thanh công cụ $\rightarrow$ Chọn **Chỉnh sửa (Edit)**$\rightarrow$ Xóa toàn bộ ký tự trong ô **Tên (Name)** $\rightarrow$ Nhấn **Lưu (Save)**.

* **Kết quả:** Thanh Bookmark chỉ hiển thị đúng Biểu tượng (Favicon) của 4 trang: *CarePulse*, *Cổng BHYT*, *Dược thư*,*Google Dịch*, giúp chứa hơn 30+ Bookmark mà không bị tràn màn hình.

#### **5\. Xử lý Bẫy an ninh & Cảnh báo Cloud Sync**

* **Chế độ duyệt web bắt buộc chọn:** Guest Profile .

  * *Lý do:* Chế độ Khách tạo một môi trường hoàn toàn trống, không truy cập được vào Bookmark, Lịch sử, hay Mật khẩu đã lưu của các Profile phòng khám. Khi đóng cửa sổ, toàn bộ dữ liệu tạm thời sẽ bị xóa sạch ngay lập tức .

* **Cảnh báo nguy cơ bật Cloud Sync cá nhân:**

  * Nếu đăng nhập tài khoản Google cá nhân và bật Sync trên máy trạm, toàn bộ Mật khẩu y tế, Lịch sử khám bệnh và dữ liệu nội bộ có nguy cơ bị đồng bộ ngược về thiết bị cá nhân hoặc lưu trữ trên Cloud cá nhân, vi phạm nghiêm trọng quy định bảo mật thông tin bệnh nhân và ATTT y tế.


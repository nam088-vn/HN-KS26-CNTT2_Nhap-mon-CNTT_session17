**Bài 3 : Xử lý Sự cố Giao diện Website Doanh nghiệp**

### **PHẦN 1: BÁO CÁO PHÂN TÍCH VẤN ĐỀ** 

### **1\. Phác thảo Sơ đồ Box Model hiện tại** 

* **Lớp Outermost \- MARGIN :** Top: \-10px, Right: \-28px, Bottom: 0px, Left: 28px.   
* **Lớp BORDER :** Kích thước 2px, kiểu solid red bao quanh phần tử.

* **Lớp PADDING:** Top: 15px, Right: 10px, Bottom: 10px, Left: 10px.

* **Lớp Innermost \- CONTENT :** Chiều rộng thực tế hiển thị 840px x 600px.

#### **2\. Trả lời bẫy dữ liệu** 

* Khi thay đổi Margin mà không kiểm tra Padding, phần tử vẫn dùng chế độ box-sizing: content-box mặc định.  
* Lúc này, tổng chiều rộng \= Width (65%)+Padding+BorderWidth (65%)+Padding+Border. Việc chỉ chỉnh lề margin khiến tổng kích thước khối vẫn vượt quá 100%100% không gian chứa, làm giao diện tiếp tục bị đè hoặc rớt dòng.

### **PHẦN 2: THIẾT KẾ GIẢI PHÁP** 

1. **Thêm quy tắc Box Model chuẩn:**

   * Gán box-sizing: border-box \!important; cho toàn bộ phần tử để cố định kích thước khối đã bao gồm Padding và Border.

2. **Cập nhật CSS cho Khung bài học :**

   * Chiều rộng: width: 65% \!important;

   * Căn lề: float: left;

   * Triệt tiêu margin âm: margin-right: 0 \!important; và margin-left: 0 \!important;

3. **Cập nhật CSS cho Khung danh sách video :**

   * Chiều rộng: width: 33% \!important;

   * Căn lề: float: left;

   * Tạo khoảng cách giữa 2 khối: margin-left: 2% \!important; và margin-right: 0 \!important;


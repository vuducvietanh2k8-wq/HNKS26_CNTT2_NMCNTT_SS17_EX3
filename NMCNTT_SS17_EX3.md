Phần 1: Báo cáo phân tích (I/O)
1. Xác định vấn đề
Trong giao diện PTIT-LMS, khung Nội dung bài học đang bị chồng lấn lên khung Danh sách video, làm giao diện mất cân đối và gây khó khăn khi theo dõi nội dung.

Sử dụng F12 → Inspect → chọn từng phần tử → tab Computed để kiểm tra các thuộc tính:
- width, height: Kích thước vùng nội dung.
- padding: Khoảng cách từ nội dung đến đường viền.
- border: Độ dày đường viền.
- margin: Khoảng cách bên ngoài phần tử.
Lưu ý: Chưa có ảnh chụp thực tế của tab Computed nên không thể xác định chính xác các giá trị CSS hiện tại. Sơ đồ dưới đây mô tả cấu trúc Box Model cần kiểm tra.
2. Sơ đồ Box Model
Thành phần	Ý nghĩa
Content	Vùng hiển thị nội dung thực tế
Padding	Khoảng cách giữa nội dung và viền
Border	Đường viền bao quanh phần tử
Margin	Khoảng cách giữa phần tử và các phần tử khác
3. Phân tích nguyên nhân chồng lấn
Một số nguyên nhân có thể xảy ra:
- margin quá nhỏ hoặc mang giá trị âm.
- padding quá lớn khiến phần tử chiếm nhiều diện tích hơn dự kiến.
- Hai phần tử có chiều rộng vượt quá không gian chứa.
- Sử dụng position: absolute khiến phần tử thoát khỏi luồng bố cục thông thường.
- Thiếu thiết lập box-sizing: border-box.
Bẫy dữ liệu: Thay đổi Margin mà không kiểm tra Padding

Nếu chỉ tăng margin, phần tử có thể bị đẩy ra xa hơn nhưng chưa chắc giải quyết được nguyên nhân thực sự. Nếu padding quá lớn, vùng hiển thị vẫn có thể chiếm diện tích vượt dự kiến.

Nếu sử dụng margin âm, hai phần tử thậm chí có thể tiếp tục chồng lấn.
Phần 2: Thiết kế giải pháp
1. Đề xuất thông số CSS
Ưu tiên sử dụng Flexbox để sắp xếp hai khung theo chiều dọc, đồng thời thống nhất cách tính kích thước.
* {
    box-sizing: border-box;
}

/* Khung chứa hai phần tử */
.lesson-container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 100%;
}

/* Khung nội dung bài học */
.lesson-content {
    width: 100%;
    padding: 16px;
    margin: 0;
    border: 1px solid #ddd;
    position: static;
}

/* Khung danh sách video */
.video-list {
    width: 100%;
    padding: 16px;
    margin: 0;
    border: 1px solid #ddd;
    position: static;
}

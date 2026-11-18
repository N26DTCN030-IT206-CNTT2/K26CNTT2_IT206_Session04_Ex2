## 3. Bước 2: Bảng so sánh Trade-off giữa 2 giải pháp

| Tiêu chí đánh giá | Giải pháp 1 (Đơn giản - Gộp luồng) | Giải pháp 2 (Chi tiết - Prompt Chaining + CoT) |
| :--- | :--- | :--- |
| **Độ dễ hiểu & Triển khai** | **Cao:** Ngắn gọn, dễ viết, chạy 1 lần có ngay kết quả. | **Trung bình:** Cấu trúc dài, phải chạy tuần tự 2 bước và copy ngữ cảnh. |
| **Chi phí Token & Độ trễ** | **Ít:** Tiêu tốn ít token đầu vào/đầu ra, phản hồi nhanh. | **Nhiều hơn:** Tốn nhiều token hơn do phải truyền dữ liệu trung gian qua 2 lượt. |
| **Độ chính xác toán học** | **Trung bình:** Dễ bị AI tính nhẩm tắt, làm tròn sai khiến tổng % lệch khỏi 100%. | **Cực cao:** Ép hiển thị từng phép tính trung gian và có bước đối soát chéo 100%. |
| **Khả năng chặn lỗi biên** | **Thấp:** Khi thu nhập giảm sâu, AI thường xuất ra số tiền chi tiêu bị âm (`-2.000.000đ`) rất vô lý. | **Cực tốt:** Có quy tắc xử lý tình huống biên rõ ràng khi dòng tiền thiếu hụt. |
| **Chống đứt gãy & Nhất quán** | **Kém:** Dễ bị cắt ngang bảng hoặc đổi cấu trúc khi dữ liệu đầu vào phức tạp. | **Tối ưu:** Tách tải giữa bước tính toán và bước trình bày, có lệnh nối mạch chuẩn xác. |

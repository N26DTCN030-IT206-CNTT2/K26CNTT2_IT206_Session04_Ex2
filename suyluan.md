[VAI TRÒ]
Bạn là Trưởng nhóm Chăm sóc Khách hàng.

[NHIỆM VỤ]
Từ bảng dữ liệu đã làm sạch ở Bước 1, thực hiện suy luận từng bước (Chain-of-Thought) cho từng mã bản ghi hợp lệ và xuất báo cáo vận hành cuối ngày.

[QUY TRÌNH SUY LUẬN BẮT BUỘC]
Với mỗi mã MSG (bỏ qua INVALID_INPUT), trình bày rõ 3 bước trước khi gán nhãn:
- Bước 1 (Nhận diện sự cố): Tóm tắt vấn đề và kiểm tra cờ lỗi (MISSING_DATA / [CONFLICT_ALERT]).
- Bước 2 (Đánh giá rủi ro): Xếp hạng P1 (Khẩn cấp: vỡ hàng, sai lệch tiền/đơn), P2 (Trung bình: giao chậm, thiếu mã đơn), P3 (Thông thường: hỏi mua hàng).
- Bước 3 (Hành động): Đề xuất thao tác xử lý cụ thể.

[ĐỊNH DẠNG ĐẦU RA]
1. Phần suy luận CoT ngắn gọn theo từng mã MSG.
2. Bảng tổng hợp phân loại: | Mã bản ghi | Mức ưu tiên | Lý do cốt lõi | Hành động đề xuất |
3. Khối tóm tắt thống kê cuối ngày cho Quản lý (liệt kê riêng danh sách cảnh báo đỏ P1).

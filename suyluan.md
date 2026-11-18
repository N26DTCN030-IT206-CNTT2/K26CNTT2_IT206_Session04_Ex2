Bước 3: Lựa chọn phương án tối ưu & Kết quả chạy thử nghiệm
4.1. Lựa chọn phương án tối ưu và giải thích
Phương án được chọn: Giải pháp 2 (Prompt Chaining 2 bước kết hợp Chain-of-Thought và Guardrails).

Lý do lựa chọn: Trong bài toán tài chính cá nhân, độ chính xác số học và tính an toàn khi xử lý tình huống biên quan trọng hơn việc tiết kiệm một vài token. Giải pháp 1 tuy nhanh nhưng tiềm ẩn rủi ro AI cộng trừ sai lệch hoặc đề xuất chi tiêu âm khi thu nhập biến động giảm. Giải pháp 2 tách biệt khâu Kiểm toán số liệu (Bước 1) khỏi khâu Trình bày & Tư vấn (Bước 2) giúp loại bỏ hoàn toàn ảo giác toán học, đảm bảo tổng ngân sách luôn khớp 100% và vận hành ổn định trong thực tế.

4.2. Kết quả chạy thử nghiệm thực tế (Test Run)
Dữ liệu đầu vào giả định (Kịch bản thu nhập biến động):

Tổng thu nhập thực nhận tháng này: 15.000.000 VNĐ

Chi phí cố định bắt buộc (Tiền trọ, điện nước, internet): 5.000.000 VNĐ

Nghĩa vụ trả nợ tối thiểu trong tháng: 2.500.000 VNĐ

Mục tiêu tiết kiệm & Quỹ dự phòng: Tối thiểu 20% thu nhập khả dụng

#### Kết quả đầu ra Bước 1 (Kiểm toán dòng tiền CoT):
<FINANCIAL_AUDIT_STEP1>
- Nhật ký tính toán chi tiết từng bước:
  + Bước 1 (Thu nhập khả dụng): 15.000.000 - 5.000.000 = 10.000.000 VNĐ.
  + Bước 2 (Tiền còn lại sau nợ): 10.000.000 - 2.500.000 = 7.500.000 VNĐ.
  + Bước 3 (Trích lập Tiết kiệm & Dự phòng - 20% của 10.000.000 VNĐ):
    * Tổng trích lập = 10.000.000 × 20% = 2.000.000 VNĐ.
    * Quỹ dự phòng khẩn cấp (10%): 1.000.000 VNĐ.
    * Tiết kiệm mục tiêu (10%): 1.000.000 VNĐ.
  + Bước 4 (Ngân sách chi tiêu linh hoạt): 7.500.000 - 2.000.000 = 5.500.000 VNĐ.
    * Chi tiêu thiết yếu biến đổi (ăn uống, đi lại - 3.500.000 VNĐ).
    * Phát triển bản thân & Giải trí (2.000.000 VNĐ).
- Trạng thái dòng tiền: An toàn (Đáp ứng đủ nợ và mục tiêu tiết kiệm 20%).
- Số liệu chốt từng hạng mục:
  + Chi phí cố định: 5.000.000 VNĐ (33.33%)
  + Trả nợ tối thiểu: 2.500.000 VNĐ (16.67%)
  + Quỹ dự phòng khẩn cấp: 1.000.000 VNĐ (6.67%)
  + Tiết kiệm mục tiêu: 1.000.000 VNĐ (6.67%)
  + Chi tiêu thiết yếu biến đổi: 3.500.000 VNĐ (23.33%)
  + Phát triển bản thân & Giải trí: 2.000.000 VNĐ (13.33%)
- Đối soát tổng cộng: 5.000.000 + 2.500.000 + 1.000.000 + 1.000.000 + 3.500.000 + 2.000.000 = 15.000.000 VNĐ (100.00%).
</FINANCIAL_AUDIT_STEP1>

#### Kết quả đầu ra Bước 2 (Bảng phân bổ ngân sách cuối cùng):

| Hạng mục | Số tiền (VNĐ) | Tỷ lệ % | Ghi chú |
| :--- | :---: | :---: | :--- |
| Chi phí cố định bắt buộc | 5.000.000 | 33,33% | Thanh toán tiền nhà, điện nước, internet đầu tháng |
| Trả nợ tối thiểu | 2.500.000 | 16,67% | Ưu tiên chuyển khoản đúng hạn tránh phí phạt |
| Quỹ dự phòng khẩn cấp | 1.000.000 | 6,67% | Gửi tài khoản tách biệt (đạt 10% thu nhập khả dụng) |
| Tiết kiệm mục tiêu | 1.000.000 | 6,67% | Tích lũy dài hạn (tổng tiết kiệm + dự phòng = 20% thu nhập khả dụng) |
| Chi tiêu thiết yếu biến đổi | 3.500.000 | 23,33% | Ngân sách ăn uống, xăng xe sinh hoạt (~115.000đ/ngày) |
| Phát triển bản thân & Giải trí | 2.000.000 | 13,33% | Học tập, sách vở, giao lưu bạn bè |
| **TỔNG CỘNG** | **15.000.000** | **100,00%** | **Đã đối soát khớp 100% tổng thu nhập thực nhận** |




# BÁO CÁO PHÂN TÍCH TRADE-OFF: KỸ THUẬT PROMPTING NÂNG CAO (LOGIC & CHUỖI)

- **Sinh viên thực hiện:** Lê Hồ Thanh Thảo
- **Mã sinh viên:** N26DTCN030
- **Lớp:** D26TXCN02-N (CNTT2)
- **Môn học:** Kỹ Năng Prompting với AI (IT206-K26) - Buổi 4

---

## 1. Bối cảnh & Bài toán đặt ra
Xây dựng hệ thống trợ lý AI tự động **lập kế hoạch tài chính cá nhân và đề xuất danh mục đầu tư/tiết kiệm hàng tháng** cho người có thu nhập biến động, đang có khoản nợ cần thanh toán. 
- **Ràng buộc nghiệp vụ:** Tiết kiệm tối thiểu 20% thu nhập khả dụng, ưu tiên trả nợ đúng hạn, duy trì quỹ dự phòng.
- **Yêu cầu kỹ thuật:** Áp dụng suy luận từng bước (Chain-of-Thought), chia chuỗi xử lý (Prompt Chaining), kiểm soát lỗi biên (số âm/thu nhập giảm sâu) và chống đứt gãy ngữ cảnh (Anti-Truncation).

---

## 2. Bước 1: Đề xuất 2 phương án Prompt mẫu

### Phương án 1: Giải pháp đơn giản, ngắn gọn (Zero-shot / Single-flow gộp luồng)
Gộp toàn bộ yêu cầu vào một câu lệnh duy nhất, không chia bước trung gian và ít ràng buộc kiểm soát biên.

````markdown
Bạn là chuyên gia tài chính cá nhân. Hãy lập kế hoạch ngân sách hàng tháng cho tôi dựa trên dữ liệu sau:
- Thu nhập tháng này: [Nhập số tiền]
- Chi phí cố định: [Nhập số tiền]
- Khoản nợ cần trả: [Nhập số tiền]
- Mục tiêu tiết kiệm: Tối thiểu 20%

Hãy suy nghĩ từng bước để tính toán số tiền còn lại, đảm bảo trả nợ đúng hạn và có quỹ dự phòng. Xuất kết quả gồm các bước tính toán và một bảng phân bổ ngân sách cuối cùng (Hạng mục, Số tiền, Tỷ lệ %, Ghi chú) sao cho tổng bằng 100%.

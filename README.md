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
````
Chuỗi Bước 1: Prompt Tính toán & Kiểm toán Dòng tiền (Chain-of-Thought)
# VAI TRÒ
Bạn là Chuyên gia Hoạch định Tài chính Cá nhân (CFP) với tư duy logic và độ chính xác toán học tuyệt đối.

# CHỈ THỊ KÍCH HOẠT SUY LUẬN (CoT)
Hãy suy nghĩ từng bước một và tính toán chi tiết trước khi đưa ra quyết định. Hiển thị đầy đủ mọi phép tính cộng (+), trừ (-), nhân (×), chia (÷) trung gian, không làm tròn sai lệch, không dùng code Python.

# DỮ LIỆU ĐẦU VÀO
- Tổng thu nhập thực nhận: [Nhập số tiền]
- Chi phí cố định bắt buộc: [Nhập số tiền]
- Nghĩa vụ trả nợ tối thiểu trong tháng: [Nhập số tiền]
- Mục tiêu tiết kiệm & Quỹ dự phòng: [Tối thiểu 20% thu nhập khả dụng]

# QUY TRÌNH XỬ LÝ & CHẶN LỖI BIÊN
1. Bước 1: Thu nhập khả dụng = Tổng thu nhập - Chi phí cố định.
2. Bước 2: Tiền sau nợ = Thu nhập khả dụng - Trả nợ tối thiểu.
3. Bước 3: Trích lập Tiết kiệm & Dự phòng (>= 20% Thu nhập khả dụng). Chia rõ % Quỹ dự phòng và % Tiết kiệm mục tiêu.
4. Bước 4: Ngân sách chi tiêu linh hoạt = Tiền sau nợ - Tổng Tiết kiệm & Dự phòng.
- **Chặn lỗi biên (Edge-case):** Nếu ở bất kỳ bước nào số tiền bị âm (< 0) hoặc không đủ 20% tiết kiệm, lập tức kích hoạt chế độ "Thắt lưng buộc bụng": cắt 100% giải trí, hạ tiết kiệm về mức sàn an toàn và cảnh báo rủi ro.

# ĐỊNH DẠNG ĐẦU RA BẮT BUỘC
Chỉ xuất kết quả trong cặp thẻ dưới đây để làm đầu vào cho Bước 2:
<FINANCIAL_AUDIT_STEP1>
- Nhật ký tính toán chi tiết từng bước: ...
- Trạng thái dòng tiền (An toàn / Cảnh báo rủi ro): ...
- Số liệu chốt từng hạng mục (VNĐ & % trên Tổng thu nhập): ...
- Đối soát tổng cộng: [Phải bằng chính xác 100% Tổng thu nhập]
</FINANCIAL_AUDIT_STEP1>

Chuỗi Bước 2: Prompt Lập Bảng Phân Bổ & Đề Xuất Hành Động (Kèm chống đứt gãy)
# VAI TRÒ
Bạn là Cố vấn Quản lý Tài sản & Tối ưu Chi tiêu.

# NGỮ CẢNH ĐẦU VÀO BẮT BUỘC
Sử dụng duy nhất số liệu đã kiểm toán trong thẻ `<FINANCIAL_AUDIT_STEP1>` dưới đây (không tự ý sửa số liệu):
[DÁN TOÀN BỘ THẺ <FINANCIAL_AUDIT_STEP1> TỪ BƯỚC 1 VÀO ĐÂY]

# NHIỆM VỤ & QUY TẮC CHỐNG ĐỨT GÃY NGỮ CẢNH
1. Xuất bảng phân bổ ngân sách chuẩn Markdown gồm 4 cột: `Hạng mục | Số tiền (VNĐ) | Tỷ lệ % | Ghi chú` (tổng bằng chính xác 100%).
2. Đưa ra 3 khuyến nghị hành động thực tế cho tháng này.
3. **Chống đứt gãy (Anti-Truncation):** Nếu phản hồi quá dài chạm giới hạn token và bị ngắt giữa chừng, hãy dừng đúng tại chữ cuối cùng, không tóm tắt vội. Khi nhận lệnh: *"Tiếp tục từ cụm từ: [10 từ cuối]"*, hãy nối khớp hoàn hảo với câu trước đó.



# K26CNTT2_IT206_Session04_Ex2
# BÁO CÁO PHÂN TÍCH TRADE-OFF CÁC GIẢI PHÁP PROMPTING NÂNG CAO (LOGIC & CHUỖI)

**Môn học:** Kỹ năng Prompting với AI (IT206-K26)  
**Buổi học:** Buổi 4 - Kỹ thuật Prompting Nâng cao (Logic & Chuỗi)  
**Bài tập:** Bài 2 - So sánh Trade-off các giải pháp ra lệnh  
**Sinh viên thực hiện:** Lê Hồ Thanh Thảo  
**MSSV:** N26DTCN030  

---

## 1. Mục tiêu bài tập
* Rèn luyện tư duy phản biện thông qua việc thiết kế và đối chiếu 2 phương án viết Prompt khác nhau cho cùng một bài toán nghiệp vụ ứng dụng **Kỹ thuật Prompting Nâng cao (Logic & Chuỗi)**.
* Đánh giá sự đánh đổi (**Trade-off**) giữa chi phí vận hành (số lượng token, độ phức tạp) và chất lượng đầu ra (tính chính xác, khả năng suy luận logic và chặn lỗi biên) để chọn ra giải pháp tối ưu nhất.

---

## 2. Bối cảnh & Yêu cầu bài toán
* **Bối cảnh thực tế:** Bộ phận vận hành của một cửa hàng thương mại điện tử cần xử lý danh sách phản hồi/khiếu nại đơn hàng cuối ngày từ khách hàng (bao gồm cả đơn hợp lệ, đơn thiếu thông tin, đơn mâu thuẫn trạng thái và danh sách dài dễ bị cắt ngắt ngữ cảnh).
* **Yêu cầu kỹ thuật:** Thiết kế quy trình ra lệnh tối ưu hóa 3 kỹ thuật cốt lõi:
  1. **Chain-of-Thought (CoT):** Ép AI suy luận từng bước trước khi kết luận mức độ ưu tiên.
  2. **Prompt Chaining:** Phân tách luồng xử lý thành các bước nối tiếp nhau (Làm sạch dữ liệu -> Phân loại -> Xuất báo cáo).
  3. **Xử lý đứt gãy ngữ cảnh:** Đánh chỉ mục bản ghi để AI tiếp tục xuất dữ liệu chính xác nếu bị giới hạn độ dài phản hồi.

---

## 3. Quy tắc nghiệp vụ & Ràng buộc dữ liệu
* **Giải pháp 1 (Đơn giản, ngắn gọn):** Viết Prompt gộp chung các yêu cầu trong một lượt hỏi ngắn, dùng ngôn ngữ tự nhiên, ít ràng buộc định dạng và không cài đặt cơ chế bẫy lỗi chi tiết.
* **Giải pháp 2 (Chi tiết, nhiều ràng buộc):** Áp dụng kiến trúc Prompt Chaining kết hợp Chain-of-Thought tường minh, đóng gói dữ liệu trong thẻ XML, quy định từ khóa chặn lỗi biên (`MISSING_DATA`, `INVALID_INPUT`, `[CONFLICT_ALERT]`) và cơ chế đánh số thứ tự chống đứt gãy ngữ cảnh.

---

## 4. Bước 1: Đề xuất 2 Prompt mẫu

### 4.1. Giải pháp 1: Prompt đơn giản, ngắn gọn (Zero-shot gộp luồng)

```text
Bạn là nhân viên chăm sóc khách hàng. Hãy đọc danh sách tin nhắn khách hàng dưới đây, suy nghĩ từng bước để phân loại mức độ ưu tiên (Cao, Trung bình, Thấp), lọc bỏ tin nhắn rác và viết báo cáo tổng hợp ngắn gọn cuối ngày. Nếu danh sách dài quá thì dừng lại để tôi bảo viết tiếp.

Dữ liệu:
1. Chị Lan (0912345678): Đơn DH102 mở hộp ra bị vỡ bình giữ nhiệt rồi em ơi, đổi gấp giúp chị!
2. Minh Tuấn: Áo khoác đen size L còn ở chi nhánh Quận 1 không shop?
3. ...
4. Khách ẩn danh (0988777666): Đơn DH105 báo đã giao thành công và hoàn tiền nhưng thực tế anh chưa nhận được hàng lẫn tiền?!
5. 0909111222: Giao hàng chậm quá đi mất, đặt 4 ngày rồi chưa thấy đâu.

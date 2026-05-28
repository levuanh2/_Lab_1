# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *Khi temperature thấp như 0.0, phản hồi thường ổn định, ngắn gọn và ít thay đổi giữa các lần gọi. Khi tăng lên 0.5 hoặc 1.0, câu trả lời bắt đầu đa dạng và tự nhiên hơn. Ở mức 1.5, phản hồi có thể sáng tạo hơn nhưng cũng dễ lan man hoặc kém chính xác hơn.*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Khi temperature thấp như 0.0, phản hồi thường ổn định, ngắn gọn và ít thay đổi giữa các lần gọi. Khi tăng lên 0.5 hoặc 1.0, câu trả lời bắt đầu đa dạng và tự nhiên hơn. Ở mức 1.5, phản hồi có thể sáng tạo hơn nhưng cũng dễ lan man hoặc kém chính xác hơn.*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
>*10.000 * 3 * 350 = 10.500.000 token/ngày*
*gpt-4o      = 0.010 USD / 1K output tokens*
*gpt-4o-mini = 0.0006 USD / 1K output tokens*
*Chi phí GPT-4o: 10.500.000 / 1000 * 0.010 = 105 USD/ngày*
*Chi phí GPT-4o-mini: 10.500.000 / 1000 * 0.0006 = 6.3 USD/ngày*
*GPT-4o đắt hơn: 105 / 6.3 ≈ 16.67 lần*
*Với workload này, GPT-4o đắt hơn GPT-4o-mini khoảng 16.67 lần. Cụ thể, nếu chỉ tính output token theo giá trong bài, GPT-4o tốn khoảng 105 USD/ngày, còn GPT-4o-mini tốn khoảng 6.3 USD/ngày.*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *GPT-4o xứng đáng dùng trong các trường hợp cần chất lượng suy luận cao, ví dụ phân tích tài liệu phức tạp, hỗ trợ ra quyết định quan trọng, viết báo cáo chuyên sâu hoặc xử lý yêu cầu có nhiều ngữ cảnh. GPT-4o-mini phù hợp hơn cho các tác vụ đơn giản, số lượng lớn và cần tiết kiệm chi phí như chatbot FAQ, phân loại nội dung, tóm tắt ngắn, tạo câu trả lời mẫu hoặc xử lý các request lặp lại hằng ngày.*

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming quan trọng nhất trong các trường hợp phản hồi dài hoặc người dùng cần thấy kết quả ngay lập tức, ví dụ chatbot, trợ lý viết nội dung, giải thích bài học, phân tích tài liệu hoặc sinh code. Khi có streaming, người dùng không phải chờ toàn bộ câu trả lời hoàn thành mà có thể đọc dần từng phần, giúp trải nghiệm mượt hơn. Ngược lại, non-streaming phù hợp hơn khi phản hồi ngắn, cần xử lý toàn bộ kết quả trước khi hiển thị, hoặc hệ thống cần lưu log, kiểm duyệt, định dạng JSON hay kiểm tra output trước khi trả về cho người dùng.*


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 

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
> Khi temperature tăng dần từ 0.0 lên 1.5, câu trả lời chuyển từ trạng thái an toàn, dập khuôn, mang tính xác thực cao (0.0) sang trạng thái văn phong mượt mà, sáng tạo hơn (0.5-1.0). Tuy nhiên, khi đạt đến mức 1.5, LLM bắt đầu sinh ra các từ ngữ lộn xộn, thiếu logic, mất cấu trúc ngữ pháp và có hiện tượng bịa đặt thông tin (hallucination).

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Mình sẽ đặt temperature ở mức rất thấp, khoảng 0.0 đến 0.2. Bởi vì chatbot hỗ trợ khách hàng cần sự chính xác, nhất quán và tuân thủ chặt chẽ các chính sách/thông tin sản phẩm, không được phép "sáng tạo" hay tự bịa đặt thông tin sai lệch làm ảnh hưởng đến trải nghiệm và quyền lợi của khách hàng. 

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Dựa trên bảng giá đầu ra, GPT-4o tốn $0.010/1K token, trong khi GPT-4o-mini tốn $0.0006/1K token. Tỷ lệ chênh lệch là 0.010 / 0.0006 ≈ 16.67 lần. Vậy GPT-4o đắt hơn GPT-4o-mini khoảng gần 17 lần cho cùng một khối lượng công việc.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi: Hệ thống cần xử lý các tác vụ phức tạp đòi hỏi suy luận logic sâu, hiểu ngữ cảnh phức tạp, viết code khó hoặc phân tích dữ liệu chuyên sâu (VD: Trợ lý luật sư, trợ lý lập trình).GPT-4o-mini tốt hơn khi: Cần xử lý khối lượng dữ liệu lớn với các tác vụ đơn giản, lặp đi lặp lại như tóm tắt văn bản, trích xuất thực thể (NER), dịch thuật cơ bản, hoặc chatbot hỏi đáp FAQ thông thường để tối ưu chi phí và tốc độ.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng tương tác trực tiếp với người dùng (như chatbot ChatGPT), giúp giảm độ trễ cảm nhận (perceived latency) vì người dùng có thể đọc ngay từng chữ được sinh ra mà không phải nhìn màn hình "đơ" chờ đợi toàn bộ câu trả lời. Ngược lại, non-streaming phù hợp với các tác vụ xử lý ngầm (background jobs, ETL, batch processing) hoặc trong các pipeline Agent/RAG tự động, nơi hệ thống máy tính chỉ cần nhận toàn bộ kết quả cuối cùng để phân tích hoặc chuyển sang bước tiếp theo chứ không cần hiển thị hiệu ứng gõ chữ cho con người xem.


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 

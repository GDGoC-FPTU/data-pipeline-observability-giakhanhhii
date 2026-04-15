# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600225
**Name:** Nguyễn Triệu Gia Khánh
**Date:** 15/04/2026

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.0. | 9 | Dữ liệu sạch, category electronics đúng định dạng, giá trị giá hợp lệ nên Agent truy vấn đúng. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 3 | Agent không crash, nhưng bị outlier giá cực lớn dẫn hướng kết quả sai lệch và không thực tế. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi dùng garbage data, Agent không chỉ trả lời kém chính xác mà còn có thể bị crash vì dữ liệu không đạt chuẩn. Đầu tiên, sai kiểu dữ liệu ở cột `price` (chuỗi "ten dollars") làm pandas không thể so sánh giá trị lớn nhất một cách ổn định, dẫn đến lỗi runtime trong nhiều trường hợp. Thứ hai, duplicate ID làm mơ hồ nguồn gốc dữ liệu và có thể gây trùng lặp thông tin khi truy vấn. Thứ ba, outlier rất lớn như giá 999999 có thể đánh lừa mô hình ra quyết định sai, ưu tiên sản phẩm bất thường thay vì giá trị thực. Cuối cùng, null values ở `id` và `category` làm mất ngữ cảnh và giảm khả năng lọc dữ liệu đúng nhóm. Tất cả lỗi này cho thấy chất lượng dữ liệu là điều kiện tiên quyết để Agent hoạt động ổn định.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** (Đồng ý hay không? Giải thích ngắn gọn.)

Đồng ý. Prompt tốt chỉ giúp đặt câu hỏi rõ ràng, nhưng nếu dữ liệu nền bị bẩn, sai kiểu, hoặc thiếu ngữ cảnh thì Agent vẫn đưa ra kết quả sai hoặc không thể trả lời. Data quality tốt giúp Agent suy luận đúng và ổn định hơn trong mỗi lần truy vấn.

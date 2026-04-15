[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574033&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.khanhntg@vinuni.edu.vn
**Name:** Nguyễn Triệu Gia Khánh - 2A202600225


---

## Mo ta

Trong bài lab này, em xây dựng ETL pipeline tự động gồm 4 bước: `extract`, `validate`, `transform`, `load`.
Pipeline đọc dữ liệu từ `raw_data.json`, loại bỏ các record không hợp lệ (giá <= 0 hoặc `category` rỗng), sau đó tính giá giảm 10%, chuẩn hóa category về Title Case và thêm timestamp xử lý.
Kết quả cuối cùng được lưu vào file `processed_data.csv` để sử dụng cho bài toán quan sát chất lượng dữ liệu và stress test AI Agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chạy ETL Pipeline
```bash
python solution.py
```

Sau khi chạy xong, kiểm tra file output:
```bash
dir processed_data.csv
```

### Chay Agent Simulation (Stress Test)
```bash
# Mô tả cách bạn chạy thí nghiệm Clean vs Garbage data
python generate_garbage.py
python agent_simulation.py
```

Bước này sẽ so sánh phản hồi Agent giữa:
- Clean Data: `processed_data.csv`
- Garbage Data: `garbage_data.csv`

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output của pipeline
├── experiment_report.md     # Báo cáo thí nghiệm
└── README.md                # File này
```

---

## Ket qua

Kết quả ETL từ bộ dữ liệu mẫu:
- Tổng records đầu vào: 5
- Records hợp lệ sau validation: 3
- Records bị loại: 2 (1 record giá âm, 1 record category rỗng)
- Records được ghi vào `processed_data.csv`: 3

Pipeline đã đáp ứng các yêu cầu observability:
- Có log số record hợp lệ/không hợp lệ
- Có cột `processed_at` để theo dõi thời điểm xử lý

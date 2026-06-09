# LAB 2 - AIoT Public Dataset Deploy

## 1. Giới thiệu

Dự án **Lab 2 - AIoT Public Dataset Deploy** xây dựng một hệ thống Machine Learning cơ bản cho bài toán nhận diện trạng thái có người trong phòng dựa trên dữ liệu cảm biến IoT.

Hệ thống sử dụng dữ liệu cảm biến như:

* Nhiệt độ
* Độ ẩm
* Ánh sáng
* CO2
* Humidity Ratio

Từ các dữ liệu này, mô hình sẽ dự đoán trạng thái:

* `0`: Không có người
* `1`: Có người

Dự án bao gồm các bước chính: chuẩn bị dữ liệu, huấn luyện mô hình, đánh giá kết quả, lưu mô hình và triển khai API bằng FastAPI.

---

## 2. Mục tiêu bài Lab

Mục tiêu của Lab 2 là giúp sinh viên hiểu quy trình xây dựng một hệ thống AIoT cơ bản từ dữ liệu cảm biến đến triển khai mô hình.

Cụ thể:

* Sử dụng public dataset cho bài toán AIoT
* Tiền xử lý dữ liệu cảm biến
* Huấn luyện mô hình Machine Learning
* Đánh giá mô hình bằng các chỉ số như Accuracy, Precision, Recall, F1-score
* Lưu mô hình sau khi huấn luyện
* Xây dựng API để dự đoán dữ liệu mới
* Kiểm thử API bằng dữ liệu mẫu

---

## 3. Cấu trúc thư mục dự án

```text
lab2_aiot_public_dataset_deploy/
├── data/
│   ├── DATA_SOURCES.md
│   └── occupancy_fallback_same_schema.csv
│
├── notebooks/
│   └── 01_data_prep_baseline_deploy_ready.ipynb
│
├── src/
│   ├── data_utils.py
│   ├── download_data.py
│   ├── run_training_pipeline.py
│   ├── app.py
│   ├── test_api.py
│   └── check_outputs.py
│
├── models/
│   └── occupancy_baseline.joblib
│
├── outputs/
│   ├── metrics.json
│   ├── decision_log.csv
│   └── figures/
│
├── docs/
│   ├── sample_payload_predict.json
│   └── teacher_checklist.md
│
├── README.md
└── requirements.txt
```

---

## 4. Công nghệ sử dụng

Dự án sử dụng các công nghệ chính:

* Python
* Pandas
* NumPy
* Scikit-learn
* Joblib
* FastAPI
* Uvicorn
* Matplotlib
* Jupyter Notebook

---

## 5. Cài đặt môi trường

### Bước 1: Clone project từ GitHub

```bash
git clone https://github.com/Phuong1702/lab2_aiot_public_dataset_deploy_2.git
cd lab2_aiot_public_dataset_deploy_2
```

### Bước 2: Tạo môi trường ảo

```bash
python -m venv venv
```

Kích hoạt môi trường ảo trên Windows:

```bash
venv\Scripts\activate
```

### Bước 3: Cài đặt thư viện

```bash
pip install -r requirements.txt
```

---

## 6. Chạy huấn luyện mô hình

Để chạy pipeline huấn luyện mô hình, sử dụng lệnh:

```bash
python src/run_training_pipeline.py
```

Sau khi chạy thành công, hệ thống sẽ tạo ra:

```text
models/occupancy_baseline.joblib
outputs/metrics.json
outputs/decision_log.csv
```

Trong đó:

* `occupancy_baseline.joblib`: file mô hình đã huấn luyện
* `metrics.json`: kết quả đánh giá mô hình
* `decision_log.csv`: log kết quả dự đoán và quyết định

---

## 7. Chạy API dự đoán

Chạy server FastAPI bằng lệnh:

```bash
uvicorn src.app:app --reload
```

Sau khi chạy thành công, mở trình duyệt tại:

```text
http://127.0.0.1:8000
```

Trang tài liệu API:

```text
http://127.0.0.1:8000/docs
```

Kiểm tra trạng thái hệ thống:

```text
http://127.0.0.1:8000/health
```

---

## 8. Ví dụ dữ liệu đầu vào

API `/predict` nhận dữ liệu cảm biến dạng JSON:

```json
{
  "temperature": 23.18,
  "humidity": 27.27,
  "light": 426.0,
  "co2": 721.25,
  "humidity_ratio": 0.004793
}
```

---

## 9. Ví dụ kết quả đầu ra

Kết quả dự đoán có thể có dạng:

```json
{
  "prediction": 1,
  "label": "occupied",
  "meaning": "Có người trong phòng",
  "confidence": 0.92
}
```

Ý nghĩa:

* `prediction = 1`: Có người trong phòng
* `prediction = 0`: Không có người trong phòng
* `confidence`: độ tin cậy của mô hình

---

## 10. Kiểm thử API

Có thể chạy file kiểm thử API bằng lệnh:

```bash
python src/test_api.py
```

Hoặc gửi request trực tiếp trong giao diện Swagger tại:

```text
http://127.0.0.1:8000/docs
```

---

## 11. Kết quả đạt được

Sau khi hoàn thành Lab 2, hệ thống có thể:

* Đọc và xử lý dữ liệu cảm biến IoT
* Huấn luyện mô hình nhận diện trạng thái phòng
* Đánh giá hiệu quả mô hình
* Lưu mô hình để tái sử dụng
* Triển khai API dự đoán bằng FastAPI
* Nhận dữ liệu mới và trả về kết quả dự đoán

---

## 12. Ý nghĩa thực tế

Bài toán có thể áp dụng trong các hệ thống AIoT như:

* Nhà thông minh
* Phòng học thông minh
* Văn phòng thông minh
* Hệ thống tiết kiệm năng lượng
* Tự động bật/tắt thiết bị theo trạng thái có người

Ví dụ:

Nếu mô hình dự đoán phòng không có người, hệ thống có thể gợi ý tắt đèn hoặc điều hòa để tiết kiệm điện. Tuy nhiên, trong thực tế không nên điều khiển thiết bị hoàn toàn tự động nếu độ tin cậy thấp, mà cần kết hợp thêm rule an toàn.

---

# CSC14004 - Data Mining - Project 1
## Tiền xử lý dữ liệu (Data Preprocessing)

### Thành viên nhóm
| Tên | MSSV |
|-----|------|
| (Điền tên) | (Điền MSSV) |

---

### Mô tả tập dữ liệu

**Phần 2 – Dữ liệu bảng:** Mental Health Survey Dataset
- **Nguồn:** Kaggle – Exploring Mental Health Data
- **Kích thước:** 140,700 records (train)
- **Thuộc tính:** 19 cột bao gồm thông tin nhân khẩu học, áp lực học tập/công việc, thói quen sinh hoạt
- **Nhãn:** `Depression` (0: không, 1: có) — mất cân bằng lớp (~18% positive)
- **Đặc điểm nổi bật:** Thiếu dữ liệu có cấu trúc (MAR) — sinh viên và người đi làm có tập thuộc tính khác nhau
- **Files:**
  - `data/raw/mental_health_train.csv` — Tập huấn luyện gốc (140,700 records)
  - `data/raw/mental_health_test.csv` — Tập kiểm tra gốc

---

### Kết quả chính (Section 2.2)

#### 2.2.1 — Tiêu chí tập dữ liệu
| Tiêu chí | Yêu cầu | Thực tế | Kết quả |
|---|---|---|---|
| Số records | ≥ 10,000 | 140,700 | ✓ |
| Số thuộc tính | ≥ 10 | 17 features | ✓ |
| Kết hợp số + phân loại | Có | 8 số + 9 phân loại | ✓ |
| Tỉ lệ thiếu ≥ 5% | Có | 80.17% (Academic Pressure) | ✓ |

#### 2.2.2 — EDA Chuyên Sâu
- **Phân phối:** Tất cả 8 thuộc tính số đều KHÔNG chuẩn (D'Agostino-Pearson p≈0), kurtosis ≈ −1.2 (phân phối đều)
- **Tương quan:** Age là predictor mạnh nhất với Depression (Pearson r=−0.565, Spearman ρ=−0.541)
- **Giá trị thiếu:** Chủ yếu là MAR — sinh viên thiếu Work Pressure/Job Satisfaction; người đi làm thiếu Academic Pressure/CGPA/Study Satisfaction

#### 2.2.3 — Tiền Xử Lý & Đánh Giá

| Kỹ thuật | Phương pháp tốt nhất | Phương pháp tệ nhất | Ghi chú |
|---|---|---|---|
| (a) Điền khuyết | Mean (RMSE=5.78) | Mode (RMSE=9.03, +66%) | kNN/MICE = Mean trong đánh giá 1D |
| (b) Ngoại lai | IsoForest (contamination=0.05) | — | KS test: tất cả phương pháp thay đổi phân phối đáng kể |
| (c) Chuẩn hóa | Robust Scaling | Quantile Transform (mất cấu trúc) | Dữ liệu gần đều → Robust phù hợp hơn Z-score |
| (d) Mã hóa | Binary Encoding (VIF=4.21) | Frequency (VIF=890) | Target Encoding cũng cao VIF=95 |
| (e) Chọn đặc trưng | RF Importance (k=10: F1=0.809) | MI (k=5: F1=0.713) | Bão hòa tại k≥15 (F1≈0.813) |
| (f) Cân bằng lớp | SMOTE (F1-macro=0.883) | Random Under-sampling (F1=0.866) | Baseline AUC-ROC=0.969 vẫn cạnh tranh |

---

### Cấu trúc thư mục

```
DM/
|-- README.md
|-- requirements.txt
|-- data/
|   |-- raw/
|   |   |-- mental_health_train.csv     # Dữ liệu gốc
|   |   |-- mental_health_test.csv
|   |-- processed/                      # Dữ liệu và kết quả sau tiền xử lý
|       |-- after_imputation.csv        # Dataset sau điền khuyết
|       |-- normality_results.csv       # Kết quả D'Agostino-Pearson
|       |-- pearson_correlation.csv     # Ma trận tương quan Pearson
|       |-- spearman_correlation.csv    # Ma trận tương quan Spearman
|       |-- imputation_rmse.csv         # So sánh RMSE 5 chiến lược điền khuyết
|       |-- outlier_ks_test.csv         # KS test sau loại ngoại lai
|       |-- encoding_vif.csv            # VIF 5 phương pháp mã hóa
|       |-- feature_selection_f1.csv    # F1 theo số lượng đặc trưng
|       |-- imbalance_results.csv       # Kết quả SMOTE/ADASYN/RUS
|       |-- *.png                       # Biểu đồ trực quan hóa
|-- notebooks/
|   |-- 03_EDA_tabular.ipynb           # Section 2.2.2: EDA chuyên sâu
|   |-- 04_preprocessing_tabular.ipynb # Section 2.2.3: Tiền xử lý + đánh giá
|-- docs/
|   |-- Report.pdf                     # Báo cáo PDF
```

---

### Hướng dẫn cài đặt môi trường

```bash
# Dùng conda (khuyến nghị)
conda create -n dm_env python=3.11
conda activate dm_env
pip install -r requirements.txt

# Hoặc virtualenv
python -m venv venv
source venv/bin/activate    # Linux/Mac
venv\Scripts\activate       # Windows
pip install -r requirements.txt

# Khởi động Jupyter
jupyter notebook
```

### Chạy notebook

1. Mở `notebooks/03_EDA_tabular.ipynb` — chạy **Kernel → Restart & Run All**
2. Mở `notebooks/04_preprocessing_tabular.ipynb` — chạy **Kernel → Restart & Run All**

> **Lưu ý:** Chạy `03_EDA_tabular.ipynb` trước để sinh file `data/processed/column_info.json` cần thiết cho notebook 04.

---

### Phân công công việc

| Phần | Nội dung | Người thực hiện |
|------|----------|-----------------|
| 2.2.1 | Lựa chọn & kiểm tra tiêu chí tập dữ liệu | |
| 2.2.2a | EDA: kiểm định phân phối D'Agostino-Pearson | |
| 2.2.2b | EDA: phân tích tương quan Pearson + Spearman | |
| 2.2.2c | EDA: phân tích giá trị thiếu + Little's MCAR | |
| 2.2.3a | Xử lý giá trị thiếu (5 chiến lược + RMSE) | |
| 2.2.3b | Phát hiện ngoại lai (IQR, Z-score, IsoForest, LOF, DBSCAN) | |
| 2.2.3c | Chuẩn hóa dữ liệu + Levene's test + violin plots | |
| 2.2.3d | Mã hóa biến phân loại (5 phương pháp + VIF) | |
| 2.2.3e | Lựa chọn & giảm chiều đặc trưng + CV F1 | |
| 2.2.3f | [Nâng cao] Xử lý mất cân bằng lớp (SMOTE, ADASYN, RUS) | |

---

### Link tài nguyên

- Dataset: https://www.kaggle.com/competitions/playground-series-s4e11
- Đề bài: `CSC14004 - Data Mining - P1.pdf`

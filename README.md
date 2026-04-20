# Data Mining Lab 1: Data Preprocessing

Dự án tập trung vào tiền xử lý và phân tích khám phá cho 3 loại dữ liệu:

- `Dữ liệu ảnh`: phân tích và tiền xử lý tập ảnh phân loại cảnh.
- `Dữ liệu bảng`: phân tích dữ liệu khảo sát sức khỏe tinh thần.
- `Dữ liệu chuỗi thời gian`: tiền xử lý dữ liệu tải điện theo giờ.

Kết quả chính của dự án được thể hiện qua:

- Các notebook trong thư mục `notebooks/`
- Dữ liệu đầu ra trong `data/processed/`
- Báo cáo tổng hợp tại `report/main.pdf`

## Thành viên

- `22120457` - Khưu Hải Châu
- `23122006` - Lưu Thượng Hồng
- `23122020` - Nguyễn Thiên Ấn
- `23122034` - Lê Nguyên Khang
- `23122036` - Nguyễn Ngọc Khoa

## Cấu trúc thư mục

```text
.
├── data/
│   ├── raw/            # Dữ liệu gốc
│   └── processed/      # Dữ liệu và hình ảnh sau tiền xử lý
├── docs/
│   ├── report/         # Mã nguồn LaTex
│   └── Report.pdf      # Báo cáo
├── notebooks/          # Notebook cho EDA và preprocessing
│   ├──01_EDA_image_local.ipynb
│   ├──01_EDA_image.ipynb
│   ├──02_preprocess_image_local.ipynb
│   ├──02_preprocess_image.ipynb
│   ├──03_EDA_tabular.ipynb
│   ├──04_preprocessing_tabular.ipynb
│   ├──05_EDA_temporal.ipynb
│   ├──06_preprocessing_temporal.ipynb
│   └──07_feature-engineering_temporal.ipynb
├── requirements.txt    # Danh sách thư viện Python
└── README.md
```

## Tài nguyên dữ liệu

### 1. Dữ liệu ảnh

- Tên bộ dữ liệu: `Intel Image Classification Dataset`
- Nguồn tham khảo: [Hugging Face](https://huggingface.co/datasets/sfarrukhm/intel-image-classification)
- Link tải nhanh nhóm đang dùng: [Google Drive](https://drive.google.com/drive/folders/1_Lsyg5JcQHV8w2sPigDQqSUlOBQ0Jp8a?usp=drive_link)
- Thư mục local mong đợi: `data/raw/intel_images/`

Notebook local:

- `notebooks/01_EDA_image_local.ipynb`
- `notebooks/02_preprocess_image_local.ipynb`

Notebook Colab:

- `notebooks/01_EDA_image.ipynb`
- `notebooks/02_preprocess_image.ipynb`

### 2. Dữ liệu bảng

- Tên bộ dữ liệu: `Mental Health Survey Dataset`
- Nguồn: [Kaggle Playground Series S4E11](https://www.kaggle.com/competitions/playground-series-s4e11/data)
- File hiện có trong repo:
  - `data/raw/mental_health_train.csv`
  - `data/raw/mental_health_test.csv`

Notebook:

- `notebooks/03_EDA_tabular.ipynb`
- `notebooks/04_preprocessing_tabular.ipynb`

### 3. Dữ liệu chuỗi thời gian

- Tên bộ dữ liệu: `Spain Energy Consumption Dataset`
- Nguồn: [Kaggle - Hourly energy demand generation and weather](https://www.kaggle.com/datasets/nicholasjhana/energy-consumption-generation-prices-and-weather/?select=energy_dataset.csv)
- File hiện có trong repo: `data/raw/P4_energy_dataset.csv`

Notebook:

- `notebooks/05_EDA_temporal.ipynb`
- `notebooks/06_preprocessing_temporal.ipynb`
- `notebooks/07_feature-engineering_temporal.ipynb`

## Yêu cầu môi trường

- `Python 3.12.13`
- Khuyến nghị dùng `venv`
- Hệ điều hành: Linux/macOS/WSL đều phù hợp

Kiểm tra phiên bản Python:

```bash
python3 --version
```

Nếu máy có nhiều phiên bản Python, hãy dùng đúng `Python 3.12.13`.

## Hướng dẫn chạy

### 1. Clone dự án

```bash
git clone <repo-url>
cd lab1
```

### 2. Tạo môi trường ảo với Python 3.12.13

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python --version
```

Kỳ vọng đầu ra:

```text
Python 3.12.13
```

### 3. Cài dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Chuẩn bị dữ liệu

Repo đã kèm sẵn các file CSV cho dữ liệu bảng và chuỗi thời gian. Với dữ liệu ảnh, tải dataset về và đặt theo cấu trúc:

```text
data/raw/intel_images/
├── train/
└── test/
```

Nếu chỉ muốn chạy trên máy local, ưu tiên dùng các notebook có hậu tố `_local`.

### 5. Mở Jupyter

```bash
jupyter lab
```

Hoặc:

```bash
jupyter notebook
```

### 6. Thứ tự chạy notebook khuyến nghị

```text
Ảnh:
1. notebooks/01_EDA_image_local.ipynb
2. notebooks/02_preprocess_image_local.ipynb

Dữ liệu bảng:
1. notebooks/03_EDA_tabular.ipynb
2. notebooks/04_preprocessing_tabular.ipynb

Chuỗi thời gian:
1. notebooks/05_EDA_temporal.ipynb
2. notebooks/06_preprocessing_temporal.ipynb
3. notebooks/07_feature-engineering_temporal.ipynb
```

## Đầu ra chính

- `data/processed/final_preprocessed.csv`: tập dữ liệu bảng sau tiền xử lý
- `data/processed/P4_energy_dataset_processed.csv`: dữ liệu chuỗi thời gian sau tiền xử lý
- `data/processed/*.png`, `report/img/*.png`: các hình minh họa và kết quả đánh giá
- `report/main.pdf`: báo cáo hoàn chỉnh

## Ghi chú

- Các notebook `01_EDA_image.ipynb` và `02_preprocess_image.ipynb` chứa luồng làm việc cho Google Colab.
- Các notebook `_local.ipynb` phù hợp hơn khi chạy trực tiếp trong repo này.
- File `environment.yml` hiện không còn trong thư mục dự án, nên cách chạy được tài liệu hóa theo `venv + requirements.txt`.

## License

Dự án được phát hành theo giấy phép [MIT](LICENSE).

# Data Directory

Dữ liệu được quản lý bằng **DVC** (Data Version Control) và lưu trữ trên Google Drive.

## Cấu trúc thư mục

```
data/
├── raw/                # Dataset gốc (DVC tracked)
│   ├── games.json      # Game metadata (~268MB, ~50K+ games)
│   └── Game Reviews/   # Player reviews (~23K+ CSV files)
├── processed/          # Dữ liệu sau ETL (Parquet format)
├── features/           # Feature store cho training
├── raw.dvc             # DVC tracking file
└── README.md           # File này
```

## 🔽 Cách tải dữ liệu

### Bước 1: Cài DVC
```bash
pip install dvc dvc-gdrive
```

### Bước 2: Cấu hình OAuth credentials

Cần file `client_secret_*.json` (liên hệ team để nhận). Sau đó chạy:

```bash
# Cách 1: Dùng file JSON
dvc remote modify --local gdrive gdrive_client_id "CLIENT_ID_TRONG_FILE_JSON"
dvc remote modify --local gdrive gdrive_client_secret "CLIENT_SECRET_TRONG_FILE_JSON"

# Cách 2: Được cấp Service Account
dvc remote modify --local gdrive gdrive_use_service_account true
dvc remote modify --local gdrive gdrive_service_account_json_file_path "path/to/service-account.json"
```

### Bước 3: Pull dữ liệu
```bash
dvc pull                  # Tải toàn bộ data
dvc pull data/raw.dvc     # Chỉ tải raw data
```

Trình duyệt sẽ mở để đăng nhập Google (lần đầu). Cần có quyền truy cập folder Drive của project.

## ⚠️ Lưu ý
- **KHÔNG** commit file `client_secret*.json` hoặc `service_account*.json` lên Git
- File `.dvc/config.local` chứa credentials cá nhân, đã nằm trong `.gitignore`
- Khi thay đổi data → chạy `dvc add data/<folder>` → `dvc push` → `git add .` → `git commit`

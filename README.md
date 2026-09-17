# USFG: Uncertainty-Stratified Faithfulness Gap

Code cho nghiên cứu kiểm định xem bất định của mô hình (epistemic/aleatoric) có thực sự
gắn với độ trung thực (faithfulness) của giải thích SHAP/LIME trong bài toán chấm điểm
tín dụng hay không — và kiểm định luôn chính công cụ đo dùng để trả lời câu hỏi đó,
trên ba bộ dữ liệu tín dụng công khai (Home Credit Default Risk, Taiwan Credit Default,
Give Me Some Credit).

Phát hiện chính: phần lớn mối liên hệ "bất định cao → giải thích kém trung thực" quy
được về một biến gây nhiễu chung là vị trí xác suất dự báo, chứ không phải một hiệu ứng
độc lập của bất định lên chất lượng giải thích.

## Cấu trúc pipeline

Tám sổ tay tính toán (notebook), chạy tuần tự:

| Notebook | Vai trò | Môi trường chạy |
|---|---|---|
| `NB1_preprocess.ipynb` | Tiền xử lý ba bộ dữ liệu, chia tập | Kaggle |
| `NB2_train_M1_xgboost.ipynb` | Huấn luyện mốc XGBoost (M1) | Kaggle |
| `NB3_train_basins.ipynb` | Huấn luyện 50 lòng chảo mạng nơ-ron | Kaggle (GPU) |
| `NB4_budget_grid.ipynb` | Lưới ngân sách M × T = 50, dựng bốn kiến trúc M2–M5 | Kaggle |
| `NB5_compute_xai.ipynb` | Sinh giải thích SHAP/LIME, đo Comprehensiveness/Sufficiency | Kaggle (GPU) |
| `NB6_table.ipynb` | Tổng hợp bảng kết quả từ đầu ra NB1–NB5 | Local |
| `NB7_visualize.ipynb` | Dựng toàn bộ hình trong bài | Local |
| `NB8_validate_usfg.ipynb` | Kiểm định cấu trúc chỉ số USFG-c trên dữ liệu mô phỏng | Local |

`NB1`–`NB5` cần chạy trên Kaggle (đọc dữ liệu qua `/kaggle/input/...`, cần GPU cho `NB3`
và `NB5`). `NB6`–`NB8` chạy trên máy cá nhân, đọc kết quả trung gian qua đường dẫn tương
đối `../kaggle-output/` và ghi bảng/hình cuối vào `../result/`.

## Tái lập kết quả

1. Trên Kaggle, tạo notebook mới cho từng `NB1`–`NB5`, đính kèm ba bộ dữ liệu:
   - [Home Credit Default Risk](https://www.kaggle.com/competitions/home-credit-default-risk)
   - [Taiwan Credit Default (UCI, qua Kaggle)](https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset)
   - [Give Me Some Credit](https://www.kaggle.com/competitions/GiveMeSomeCredit)
2. Chạy lần lượt `NB1` → `NB2` → `NB3` → `NB4` → `NB5`, tải đầu ra `/kaggle/working/` về
   máy, sắp vào `kaggle-output/` theo cấu trúc mô tả ở `kaggle-output/README.md`.
3. Chạy `NB6`, `NB7`, `NB8` tại thư mục `notebooks/` (đường dẫn tương đối `../result/`,
   `../kaggle-output/` giả định notebook đang chạy từ đúng vị trí này).

Hạt giống ngẫu nhiên gốc cố định ở 42, mọi hạt giống dẫn xuất sinh tất định từ nó, trừ
một ngoại lệ: phép đo độ tái lập của giải thích dựa vào bộ sinh số ngẫu nhiên nội tại
của công cụ giải thích (SHAP/LIME), nên riêng bảng độ ổn định không tái lập được từng
chữ số giữa các lần chạy.

## `result/`

Bảng và hình đã tổng hợp sẵn (đầu ra của `NB6`–`NB8`), đủ nhỏ và không chứa thông tin
định danh cá nhân nên được đưa thẳng lên repo để người đọc xem/dùng lại mà không cần
chạy lại toàn bộ pipeline.

## Giấy phép

Mã nguồn trong repo này phát hành theo giấy phép MIT (xem `LICENSE`). Giấy phép này áp
dụng cho *code*; ba bộ dữ liệu tín dụng dùng trong nghiên cứu tuân theo điều khoản sử
dụng riêng của từng competition/dataset trên Kaggle, không thuộc phạm vi MIT nói trên và
không được đóng gói lại trong repo này.

## Trích dẫn

Nếu dùng lại mã nguồn hoặc kết quả trong repo này, vui lòng trích dẫn báo cáo nghiên
cứu tương ứng (BIT GENESIS RESEARCH AWARDS 2026, Đại học Kinh tế Thành phố Hồ Chí Minh).

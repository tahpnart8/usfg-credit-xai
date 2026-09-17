# kaggle-output/

Thư mục này giữ chỗ cho kết quả trung gian do `NB1`–`NB5` sinh ra khi chạy trên Kaggle
(mô hình đã huấn luyện, giải thích SHAP/LIME, bảng bất định theo từng hồ sơ...). Nội
dung không được đưa lên repo vì dung lượng lớn và vì dữ liệu ba bộ tín dụng gốc chỉ
được phép dùng trong phạm vi từng competition Kaggle, không được phát tán lại.

Để tái lập, tự tạo cấu trúc sau sau khi chạy `NB1`–`NB5` trên Kaggle và tải kết quả về:

```
kaggle-output/
  NB1-outputs/       # NB1_preprocess.ipynb
  NB2-outputs/        # NB2_train_M1_xgboost.ipynb
  NB3-outputs/
    NB3-result/        # NB3_train_basins.ipynb
  NB4-outputs/        # NB4_budget_grid.ipynb
  NB5-outputs/        # NB5_compute_xai.ipynb
```

Xem hướng dẫn đầy đủ ở `README.md` tại thư mục gốc của repo.

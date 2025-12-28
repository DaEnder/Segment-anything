# Đánh giá và So sánh SAM vs SAM 2 trên nhiều bộ dữ liệu phân đoạn ảnh

Đồ án này thực hiện **đánh giá có hệ thống** và **so sánh hiệu năng** giữa:

- **SAM – Segment Anything Model (2023)**
- **SAM 2 – Segment Anything Model 2 (2024)**

trên nhiều bộ dữ liệu phân đoạn ảnh phổ biến, nhằm làm rõ:
- **Chất lượng phân đoạn** (IoU, Dice)
- **Hiệu năng suy luận (Inference Time)**
- **Độ ổn định của mô hình** trên các loại dữ liệu khác nhau

---

## Cấu trúc Project
```bash
Segment-anything/
│
├── segment-anything # Folder chứa SAM
├── segment-anything-2 # Folder chứa SAM 2
├── sam_vit_h_4b8939.pt # Checkpoint SAM
├── sam2.1_hiera_large.pth # Checkpoint SAM 2 - large
├── sam2.1_hiera_base_plus.pth # Checkpoint SAM 2 - b+
├── sam2.1_hiera_tiny.pth # Checkpoint SAM 2 - tiny
├── SAM_Eval.ipynb # Notebook đánh giá & so sánh mô hình
├── data_split.ipynb # Notebook chia & chuẩn hóa dữ liệu
└── README.md
```
---

## Các mô hình được đánh giá

###  SAM (Segment Anything Model)
- Backbone: **ViT-H**
- Công bố bởi Meta AI (2023)
- Mô hình phân đoạn tổng quát, không cần huấn luyện lại

###  SAM 2
- Kiến trúc phân cấp (Hierarchical)
- Có cơ chế **memory-aware**
- Công bố bởi Meta AI (2024)
- Được tối ưu về **độ chính xác và tốc độ**

Cả hai mô hình đều được đánh giá trong **kịch bản zero-shot**, sử dụng:
- **1 điểm prompt dương** tại **tâm ảnh**

---

## Datasets

Dự án sử dụng **5 Datasets**, bao phủ nhiều bài toán khác nhau:

| Dataset | Mô tả |
|------|------|
| [**COD10K**](https://drive.usercontent.google.com/download?id=1YGa3v-MiXy-3MMJDkidLXPt0KQwygt-Z&export=download&authuser=0&confirm=t&uuid=21c6c762-ba65-49e5-8b6585483538402c&at=ANTm3cxnfZXpwj3Em62HWXAFJgUa%3A1766393574376](https://drive.google.com/file/d/1vRYAie0JcNStcSwagmCq55eirGyMYGm5/view?usp=sharing)) | Phân đoạn vật thể ngụy trang, độ tương phản thấp |
| [**DUTS-TE**](https://www.kaggle.com/datasets/balraj98/duts-saliency-detection-dataset) | Salient Object Detection quy mô lớn |
| [**ECSSD**](https://www.kaggle.com/datasets/xwdcrab/sod-ecssd-dataset) | Ảnh tự nhiên với nền phức tạp |
| [**Kvasir-SEG**](https://www.kaggle.com/datasets/debeshjha1/kvasirseg) | Phân đoạn ảnh y tế (nội soi tiêu hóa) |
| [**MSRA-B**](http://mftp.mmcheng.net/Data/MSRA-B.zip) | Bộ dữ liệu cổ điển cho bài toán saliency |

Các bộ dữ liệu được **tiền xử lý và chia lại** bằng `Data_split.ipynb`, sau khi cho chạy file sẽ cho ra dạng.


---


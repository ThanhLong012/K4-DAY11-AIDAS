# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `9454ebc817665f1d785aa6c5f6b70842187b66990aa6a9e0243aba40a190272d`; slice `B4-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_270517.jpg, adasind_271039.jpg, adasind_295948.jpg. Frame thiếu trong export: không.
TP=16; FP=5; FN=4; số lần đối chiếu=23; mean IoU của TP=0.895.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.696 | 0.922 | 0.870 |
| precision | 0.762 | 0.760 | 0.500 |
| recall | 0.800 | 0.836 | 0.667 |
| jaccard | 0.640 | 0.625 | 0.500 |
| dice | 0.780 | 0.767 | 0.667 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 1 | 0.957 | 1.000 | 0.667 | 0.667 | 0.800 |
| Car | 4 | 1 | 1 | 0.913 | 0.800 | 0.800 | 0.667 | 0.800 |
| Pedestrian | 5 | 1 | 2 | 0.870 | 0.833 | 0.714 | 0.625 | 0.769 |
| ThreeWheeler | 4 | 2 | 0 | 0.913 | 0.667 | 1.000 | 0.667 | 0.800 |
| Truck | 1 | 1 | 0 | 0.957 | 0.500 | 1.000 | 0.500 | 0.667 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_270517.jpg | 7 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_271039.jpg | 8 | 2 | 2 | 0.667 | 0.800 | 0.800 |
| adasind_295948.jpg | 1 | 3 | 2 | 0.250 | 0.250 | 0.333 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 2 | 0 | 1 | 0 | 0 | 0 |
| Car | 0 | 4 | 0 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 5 | 0 | 0 | 2 |
| ThreeWheeler | 0 | 0 | 0 | 4 | 0 | 0 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 0 | 1 | 0 | 2 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.

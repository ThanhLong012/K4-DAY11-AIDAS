# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | DUPLICATE | 1 |
| center | B4 | IGNORE_SCOPE | 1 |
| center | B4 | MISSING | 6 |
| center | B4 | SPURIOUS | 12 |
| center | B4 | WRONG_CLASS | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B4 | MISSING | 4 |
| edge | B4 | SPURIOUS | 1 |
| edge | C0 | SPURIOUS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B4 | IGNORE_SCOPE | 4 |
| mid | B4 | MISSING | 2 |
| mid | B4 | SPURIOUS | 5 |
| mid | B4 | WRONG_CLASS | 1 |
| unknown | B4 | MISSING | 3 |
| unknown | B4 | WRONG_CLASS | 3 |

## Top defects
- SPURIOUS: 21 (ví dụ frame adasind_019560.jpg)
- MISSING: 15 (ví dụ frame adasind_271039.jpg)
- WRONG_CLASS: 6 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: lỗi nổi bật nhất là **SPURIOUS (21)**, tập trung ở **center/B4 (12)**. Tách theo `why`: 10/21 là `E4_model_domain` của model YOLO (các dòng `M_only` ở `adasind_270517.jpg` M5, M6, M7, M9, M10, M11 và `adasind_271039.jpg` M8, M9, M11, M12). Model lặp đúng hai kiểu sai: (a) gọi xe ba bánh là `Car`/`Truck` (5 xe trên 2 frame, ví dụ `270517` M7 trên L3/R2), (b) vẽ box `Pedestrian` cho người ngồi trong xe ba bánh (`270517` M5, M10, M11), trái R03. Vì lặp lại trên nhiều xe và nhiều frame nên đây là lỗi domain (xe ba bánh Ấn Độ ít trong dữ liệu train), không phải một box lệch ngẫu nhiên. Spurious của annotator chỉ có 3 ở C0 (tách rider, R03) và 3 ở B4 mà reference không box (`271039` L2, L3 xe bị che: `E2_guideline_gap`; `295948` L9: `E5_unresolved`).
- Cách sửa và ai nhận việc (`owner`): lỗi model giao `ai_team`: thêm ảnh xe ba bánh và người ngồi trong xe vào tập train/fine-tune, và không dùng pre-label của model cho class `ThreeWheeler` khi chưa sửa; người gán nhãn không cần rework các ca này (`keep_with_reason`). Lỗi luật giao `guideline`: đề xuất R11 trong `20_guideline_patch.md`. Lỗi annotator duy nhất ở B4 là bỏ sót người (`271039` R4, R10, `E1`, `annotator`): đã rework R4, R10 còn mở (`rework/delta.md`).
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `r3_diag/model_compare.md` (bảng Zone × cell: center có 5 `M_only`); các dòng `r3_diag` có `why=E4_model_domain` trong `findings.csv`; rule R03, R04. Ảnh `screenshots/295948-reference-ego-body-rectangle.jpg` cho ca reference (IGNORE_SCOPE mid 4) không tính là lỗi annotator. Giới hạn: bảng đếm chung cả dòng model, annotator và reference, nên số SPURIOUS không phải chỉ số chất lượng nhãn của nhóm.

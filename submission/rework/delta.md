# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 10 | 10 | 2 | 2 | 4 | 5 |
| mid | 4 | 4 | 1 | 1 | 1 | 1 |
| edge | 2 | 3 | 1 | 0 | 0 | 0 |

## Findings action=rework
- adasind_271039.jpg R4 MISSING: đã sửa
- adasind_271039.jpg R10 MISSING: chưa sửa
- adasind_271039.jpg R4+M4 MISSING: đã sửa
- adasind_271039.jpg R10 MISSING: chưa sửa

## Nhận xét

- Rework trên bản export `B4-center-update.zip` (A sửa trên CVAT task #28 sau P4), khoá mã `4B5A-FC5E`; so với bản khoá `r1_craft` mã `9454-EBC8`.
- **Đã sửa 1/2 ca:** người ở mép phải `adasind_271039.jpg` (R4, zone edge) đã có box → edge matched 2→3, missing 1→0.
- **Chưa sửa R10:** người áo vàng bị che trong cụm đi bộ (≈261–289, 824–909) vẫn chưa có box → center missing giữ 2.
- **Thêm 1 spurious ở center (4→5):** A vẽ thêm box Pedestrian (392,821)–(424,915) nằm gần như trong box L10 đã có (391,822)–(439,943), tức là box trùng trên cùng một người, không phải người R10. Box (433,816)–(461,897) nằm trong vùng `unreadable` của reference nên không được chấm.
- Kết luận: rework cải thiện zone edge nhưng tạo thêm một lỗi DUPLICATE ở center; nhóm giữ nguyên số, không sửa báo cáo. Ca R10 và box trùng cần một vòng sửa nữa nếu còn thời gian (ghi ở decision log D10).

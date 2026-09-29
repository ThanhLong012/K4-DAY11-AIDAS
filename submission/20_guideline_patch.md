# Guideline patch

- **Rule mới đề xuất:**
  - **R03a — Lái hay dắt khi không thấy yên:** nếu không thấy người ngồi trên yên/bàn đạp và có chân chạm đất cạnh xe
    hai bánh, gán `Pedestrian` + `Bike` tách riêng (người dắt). Chỉ gán một `Bike` khi thấy người đang ngồi lái. Nếu
    frame đơn không đủ, ghi `E5_unresolved` và xem frame liền kề thay vì đoán.
  - **R11 — Vật bị che nhiều:** vật trong vùng hợp lệ cao ≥ 40 px, bị che nhưng vẫn **nhận ra class và biên trái/phải**
    thì vẽ box theo phần nhìn thấy với `occluded=true`. Chỉ dùng `ignore_region` `reason=unreadable` khi không nhận ra
    class hoặc không tách được biên của từng vật.
- **Áp dụng cho:** class `Bike`, `Pedestrian` (R03a); mọi class động, attribute `occluded` và `ignore_region`
  `reason=unreadable` (R11); cả ba zone.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:**
  - R03 phân biệt "lái" và "dắt" nhưng không nói làm gì khi ảnh không cho thấy người có ngồi trên xe hay không. Ở
    `adasind_295948.jpg` L3/R3, annotator và QA chọn `Pedestrian`, reference chọn `Bike` trên cùng một người
    (`30_escalation_ticket.md` Ticket 3, `screenshots/295948-L3-rider-or-walker.jpg`).
  - R01 bắt box vật ≥ 40 px, R06 cho phép `unreadable`, nhưng không nói ranh giới giữa hai lựa chọn. Ở
    `adasind_271039.jpg`, hai xe ba bánh đỗ sau nhóm người (L2, L3) được annotator box, reference bỏ qua, model gộp thành
    một `Car` (M11): ba bên xử lý ba kiểu (`findings.csv` dòng `r3_diag` L2, L3, `E2_guideline_gap`).
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** round `rework` trở đi của slice sau; các finding `r1_craft`/`r3_diag` hiện tại vẫn chấm theo v1.0.0.
  Hai ca trên cần người soát phân xử lại theo v1.1.0 trước khi dùng làm reference.

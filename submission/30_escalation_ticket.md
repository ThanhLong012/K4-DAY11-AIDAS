# Escalation ticket

## Ticket 1 — `ego_body` của reference trùm người đi đường

- **Frame:** `adasind_295948.jpg`
- **Ảnh chụp:** `submission/screenshots/295948-reference-ego-body-rectangle.jpg` (khung vàng bên trái là polygon `ego_body` của reference)
- **Expected impact:** Polygon `ego_body` của reference là một hình chữ nhật x 0–229, y 915–1736, trùm cả người đạp xe chở thùng "PDF", hai người đứng lề trái và người che ô hồng ở xa. Các vật này là người tham gia giao thông, không phải thân xe ego (R07). Vì R09 coi box trong ignore là don't-care, 5 box của annotator (L1, L2, L6, L7, L8) bị báo `IGNORE_SCOPE` và không được chấm; số matched/missing ở zone mid và center của frame này bị thấp hơn thực tế. Theo R10 đây là mức P0 vì ignore che nhầm vùng.
- **Owner:** `data_ops`
- **Recommendation:** Vẽ lại `ego_body` của reference ở `adasind_295948.jpg` bám theo phần áo kẻ ca-rô/thân người ngồi cùng xe ở góc dưới trái (tham khảo polygon của annotator: x 0–273, y 1181–1724), bỏ phần từ y≈915 trở lên. Sau khi sửa, chạy lại `compare r1_craft` để chấm 5 box đang bị bỏ qua.

## Ticket 2 — Reference gán xe tải nhỏ là `Car`

- **Frame:** `adasind_295948.jpg`
- **Ảnh chụp:** `submission/screenshots/295948-reference-ego-body-rectangle.jpg` (hộp `R1 Car` ở giữa ảnh)
- **Expected impact:** Xe tải nhỏ có thùng hàng (455,894,654,1077) bị reference gán `Car`; annotator (L4) và model (M2) đều gán `Truck`. Theo R04, xe tải nhỏ/pickup là `Truck`. Lỗi này tạo một `WRONG_CLASS` giả cho annotator và một `LM_noR` giả cho model ở zone center.
- **Owner:** `data_ops`
- **Recommendation:** Sửa class của R1 ở `adasind_295948.jpg` thành `Truck` trong teaching reference; không bắt annotator rework ca này.

## Ticket 3 — Người quấn khăn: đang lái hay đang dắt xe đạp?

- **Frame:** `adasind_295948.jpg`
- **Ảnh chụp:** `submission/screenshots/295948-L3-rider-or-walker.jpg`
- **Expected impact:** Annotator (L3) và QA gán `Pedestrian` (người dắt xe, cần thêm `Bike` riêng); reference (R3) gán một `Bike` (người đang lái). Ảnh chỉ thấy tay cầm ghi đông, bánh xe phía sau và bàn chân mang dép chạm mặt đường; không thấy yên hay bàn đạp. Chọn sai sẽ tạo 1 `WRONG_CLASS` và có thể 1 `MISSING` ở zone mid, và luật R03 sẽ được áp không nhất quán giữa người soát.
- **Owner:** `qa`
- **Recommendation:** Người soát xem frame liền trước/sau trong video ADASIND để biết người này có đang di chuyển trên xe không, rồi thống nhất một nhãn. Đồng thời bổ sung R03 (xem `20_guideline_patch.md`): khi không thấy người ngồi trên yên và chân chạm đất thì gán `Pedestrian` + `Bike`.

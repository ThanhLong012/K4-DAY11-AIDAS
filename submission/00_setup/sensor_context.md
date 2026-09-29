# Sensor context

Nguồn quan sát: frame C0 [`adasind_019560.jpg`](../../assets/images/adasind_019560.jpg) và ba frame slice `B4-center` ([`adasind_270517.jpg`](../../assets/images/adasind_270517.jpg),
[`adasind_271039.jpg`](../../assets/images/adasind_271039.jpg), [`adasind_295948.jpg`](../../assets/images/adasind_295948.jpg)). Mọi ý dưới đây là quan sát trên ảnh, không phải thông số rig.

- Rig: ảnh dọc 1080×1920, **một camera** fisheye nhìn về phía trước theo hướng di chuyển. Theo quan sát, ảnh được
  quay khi đang đi **xe máy**, có vẻ do **người ngồi sau cầm camera** chứ không phải camera gắn cố định trên xe
  (ở mép trái thấy áo, tay, chân của người trên xe; ở C0 thấy bóng xe và người đổ trên mặt đường). Vì cầm tay nên
  vị trí và góc camera có thể thay đổi giữa các frame. Nhóm không biết chiều cao lắp, góc nghiêng hay intrinsics: ADASIND không kèm
  tài liệu rig hay calibration, nên không dùng ảnh này để kết luận khoảng cách thật hay ghép với camera khác.
  Trong bộ ảnh cũng không có camera thứ hai.
- `ego_body`: nếu có thì nằm ở **mép trái, nửa dưới** của vòng kính.
  - C0 [`adasind_019560.jpg`](../../assets/images/adasind_019560.jpg): vùng tối sát mép trái, khoảng y≈1080–1560. Bóng đổ trên mặt đường là bóng, không phải thân xe.
  - [`adasind_270517.jpg`](../../assets/images/adasind_270517.jpg): áo kẻ ca-rô, cánh tay và chân (dép) ở mép trái, khoảng y≈1020–1720.
  - [`adasind_295948.jpg`](../../assets/images/adasind_295948.jpg): áo kẻ ca-rô ở góc dưới bên trái.
  - [`adasind_271039.jpg`](../../assets/images/adasind_271039.jpg): **không thấy thân xe ego**, nên không vẽ polygon `ego_body` (R07).
- Vòng kính: là một vòng sáng gần tròn, hơi dẹt theo chiều dọc, **tâm lệch nhẹ lên trên** so với tâm khung hình.
  - Chiều dọc khoảng y≈80–180 đến y≈1650–1760, tức khoảng 80–85% chiều cao ảnh.
  - Chiều ngang rộng hơn khung hình nên bị cắt ở hai mép trái/phải (khoảng giữa ảnh).
  - Vùng hợp lệ chiếm khoảng 3/4 diện tích khung hình. Vành đen/xám có vân nằm ở bốn góc, dải trên và dải dưới
    (dải dưới dày hơn); `lens_border` phủ phần này.
  - Gần viền vòng kính thì méo mạnh: cột điện và mép nhà bị cong, vật ở rìa bị kéo giãn và dễ bị cắt (`truncated`).
  - Có lóa và phản xạ: [`adasind_295948.jpg`](../../assets/images/adasind_295948.jpg) bị lóa nắng mạnh ở nửa trên, [`adasind_271039.jpg`](../../assets/images/adasind_271039.jpg) có vệt phản xạ cong chạy dọc giữa ảnh.

# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Cảnh đông người đi bộ và xe đỗ bị che, zone center/edge — `adasind_271039.jpg` | 2 MISSING do annotator (R4 mép phải, R10 trong cụm, `E1`); 2 SPURIOUS vì luật mơ hồ (L2, L3, `E2`); rework chỉ sửa 1/2 và sinh 1 DUPLICATE | Là lỗi thật duy nhất của annotator trên slice và rework chưa xong; cảnh đông dễ bỏ sót người nhỏ và vẽ trùng | `compare.html` r1_craft, `rework/delta.md`, dòng `rework` trong findings, ảnh gốc frame |
| Cảnh có người/phương tiện sát xe ego và lóa nắng, zone mid — `adasind_295948.jpg` | 5 IGNORE_SCOPE do `ego_body` reference sai (`E0`, P0); 1 WRONG_CLASS reference (xe tải nhỏ gán Car); 1 ca rider/dắt xe chưa rõ (`E5`) | Lỗi ở phạm vi dữ liệu (P0) làm sai mọi số của frame; phải sửa reference trước khi so tiếp | 3 ticket trong `30_escalation_ticket.md`, 2 ảnh `screenshots/295948-*`, decision log D06–D08 |

Giới hạn của kết luận từ ba frame ADASIND: chỉ 20 vật reference, zone edge có 3 vật nên một lỗi đã là 33%. Ba frame
cùng một block (B4) và cùng kiểu đường phố ban ngày, nên không nói được gì về đêm, mưa hay đường cao tốc. Một phần
chênh lệch đến từ reference (sửa tay, có thể sai), nên số matched/missing không phải điểm chất lượng của annotator.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: chọn frame theo
**cảnh**, không theo frame liên tiếp: mỗi đoạn video/cảnh chỉ lấy tối đa 1–2 frame cách nhau đủ xa, và gắn nhãn cảnh
(camera, normal/hard, loại khó như đông người, xe ba bánh, lóa, vật sát xe) để đếm độ phủ theo từng ô trong bảng
8 ô. Trước khi review, kiểm mỗi ô có đủ số cảnh khác nhau chứ không chỉ đủ số frame. Mẫu hard được chọn có chủ đích
theo rủi ro (từ lỗi ở trên: người bị che trong cụm, xe ba bánh, người sát xe ego), nên nó **lệch** về ca khó: dùng để
tìm và sửa lỗi hệ thống, không dùng để suy ra tỷ lệ lỗi của cả 50.000 frame. Muốn đo tỷ lệ lỗi cần thêm một mẫu ngẫu
nhiên riêng theo từng camera.

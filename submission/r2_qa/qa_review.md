# QA review · B4-center

Mã khóa: 9454-EBC8

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| 271039 | Nhóm người sát nhau gần car đỏ | R01 | Trong cụm người đứng sát nhau có thêm 2 người nhìn thấy được. 2 người này vẫn phân biệt được với người bên cạnh nên cần các box riêng; việc các box gần/chạm nhau không phải lý do để bỏ qua. |
| 271039 | Người đứng cạnh biển đỏ bên phải ảnh | R01 | Có một Pedestrian ở mép phải nằm trong vùng hợp lệ nhưng hiện chưa có box. Cần thêm box. |
| 271039 | Người đứng cạnh biển đỏ bên phải ảnh | R01 | Có một Pedestrian ở mép phải nằm trong vùng hợp lệ nhưng hiện chưa có box. Cần thêm box. |
| 271039 | Car #16 | R04 | Xe trắng góc trái. Van chở người (Car) hay e-rickshaw (ThreeWheeler)? Cần kiểm tra lại. |
| 295948 | Bike #24 | R03 | Bị che nhiều, không đủ rõ để xác định chắc chắn là bike, cần kiểm tra lại |
| 295948 | Pedestrian #32 | R03 | Bị che nhiều, không đủ rõ để xác định là người dắt xe (một box Pedestrian và một box Bike tách riêng) hay người đang ngồi lái xe (một box Bike) |
| 295948 | Pedestrian #26 | R03 | Người lớn ở tiền cảnh đang dắt xe hai bánh; thấy phần xe/bánh ở phía dưới. Theo R03 nên là một box Pedestrian và một box Bike tách riêng. |
| TODO | TODO | TODO | TODO |
| TODO | TODO | TODO | TODO |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.



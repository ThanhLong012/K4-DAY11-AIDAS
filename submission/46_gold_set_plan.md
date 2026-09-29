# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Cảnh đông xe máy/rider, người đi bộ cắt ngang, lóa nắng trước mặt, vật nhỏ ở xa | Tách rider thành `Pedestrian` + `Bike` thay vì một `Bike`; bỏ sót vật nhỏ; box lỏng khi bị lóa | Giữ nhãn trên ảnh fisheye gốc (không vẽ trên BEV); ghi phiên bản calibration và timestamp của từng frame | Hai người gán độc lập, người thứ ba phân xử ca bất đồng theo rule_id; chỉ gọi là gold khi hết ca mở |
| rear | Lùi xe gần người/vật thấp, ánh đèn xe sau ban đêm, vật sát thân xe | Vật thấp sát xe bị méo, bị cắt bởi vòng kính; nhầm thân xe ego với vật | Giữ polygon `ego_body` và `lens_border` riêng cho camera sau; cùng annotation space với front | Soát riêng `ego_body`/`lens_border` trước, rồi mới soát box; kiểm lại ca `truncated` |
| left | Vật ở rìa vòng kính, xe máy vượt sát, vỉa hè đông người, vùng seam với front/rear | Méo mạnh ở zone edge làm box lệch hoặc thiếu; dễ trùng box ở seam | Ghi calibration để biết vùng seam ở góc xe nằm đâu trên ảnh gốc | Reviewer độc lập soát riêng zone edge; ca seam đưa vào danh sách chờ policy cross-camera |
| right | Xe ở làn bên đi ngược/vượt, vật ở seam, vật bị gương che | Tương tự left; thêm `occluded` bị bỏ qua khi gương che | Như left; giữ cùng rule version cho cả bốn camera | Như left; so tỉ lệ bất đồng giữa left/right để phát hiện lệch rule |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): khi đổi hoặc lắp lại camera, khi calibration thay đổi, khi rule/guideline lên phiên bản mới (ví dụ sau `20_guideline_patch.md`), hoặc khi dữ liệu mới có điều kiện chưa có trong gold (đêm, mưa). Frame cũ gán theo rule cũ phải soát lại, không trộn hai phiên bản.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: một xe máy ở góc trước-trái xuất hiện cùng lúc trên front (zone edge) và left (zone mid) với hai box khác nhau. Chưa được coi là `DUPLICATE` hay xoá một box khi chưa có timestamp đồng bộ, calibration hai camera và policy output đích (giữ cả hai hay hợp nhất trên BEV).
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: lab chỉ có một camera fisheye ADASIND cầm tay, không có seam, không có calibration và không có track qua camera. Hai người đồng ý với nhau chỉ cho thấy họ áp rule giống nhau, không chứng minh nhãn đúng; teaching reference cũng đã sửa tay và có thể sai. Các ca riêng của từng camera và ca seam chưa hề được thử.

_Bản nháp P0: sau P4 bổ sung lý do dựa trên lỗi thực tế thấy trên slice `B4-center`._

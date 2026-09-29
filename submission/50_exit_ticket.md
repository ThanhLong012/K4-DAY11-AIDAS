# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao?
   **Cần quy tắc riêng, không tính là `DUPLICATE`.** `DUPLICATE` là hai box cho cùng một vật **trên cùng một ảnh**.
   Ở seam, mỗi camera là một ảnh gốc riêng và vật thật sự xuất hiện trên cả hai (có thể là `edge` ở camera này, `mid`
   ở camera kia), nên mỗi ảnh vẫn cần box của nó theo R02 (vẽ trên ảnh gốc). Việc hai box là một vật hay không là
   quyết định ở tầng hợp nhất (BEV/fusion), cần timestamp đồng bộ, calibration hai camera và policy output đích (giữ
   cả hai hay hợp nhất). Không xoá box nào ở tầng gán nhãn khi chưa có policy đó.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.
   **Giữ cùng track ID** khi vẫn là cùng một vật và còn quan sát được liên tục, kể cả khi bị che ngắn. **Thêm
   keyframe** khi hình học đổi lớn (vật đi từ center ra edge bị méo fisheye, bị che/lộ ra, đổi kích thước nhanh).
   **Đặt Outside** khi vật ra khỏi vòng kính hoặc bị che hoàn toàn; nếu quay lại mà không chắc là cùng vật thì mở
   track mới. **Trước khi nối track qua hai camera** cần: timestamp đồng bộ giữa hai camera, calibration (intrinsic +
   extrinsic) để chiếu vị trí về cùng hệ toạ độ, vật nằm trong vùng chồng (seam) tại cùng thời điểm, và đặc điểm
   khớp (class, màu, kích thước). ADASIND chỉ có một camera cầm tay, không có calibration, nên bài lab không đủ bằng
   chứng để nối track qua camera.

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?
   Ở `adasind_295948.jpg`, xe tải nhỏ có thùng hàng (L4) nhóm gán `Truck`, reference (R1) gán `Car`. Nhóm tin nhãn
   của mình đúng theo R04 (xe tải nhỏ là `Truck`) và model cũng gán `Truck`, nên giữ nhãn, ghi `E0_reference_defect`
   và escalate (Ticket 2, D07) thay vì sửa theo reference. Ngược lại, ca người quấn khăn (L3/R3) nhóm không đủ chắc
   nên ghi `E5_unresolved` và escalate chứ không khẳng định bên nào đúng. Nếu làm lại: (a) trước khi khoá, soát riêng
   các cụm người đông theo từng người một, vì hai lỗi thật của annotator (R4, R10 ở `271039`) đều là bỏ sót người;
   (b) khi rework, đánh dấu vị trí cần sửa lên ảnh trước rồi mới vẽ, để tránh vẽ nhầm người và tạo box trùng như ở
   `rework` (L6); (c) chạy lại `selfqc` sau mỗi lần sửa để `selfqc.md` không còn cảnh báo cũ.

## Đóng góp A/B/C cho ba câu trả lời

- **A · Trương Công Hoài Nam:** cung cấp ca thực tế cho câu 3 (cách vẽ xe tải nhỏ `295948` L4 là `Truck`, người quấn khăn L3 là `Pedestrian`) và kinh nghiệm khi rework (vẽ nhầm người, tạo box trùng L6).
- **B · Nghiêm Trà My:** cung cấp các bất đồng từ QA mù cho câu 3 (xe trắng `271039` Car #16, người dắt xe `295948` Pedestrian #26) và kết quả kiểm lại ca sửa.
- **C · Bùi Thành Long:** tổng hợp và viết câu 1–2 theo `docs/10-svm360-reading-vi.md`, viết câu 3 từ decision log D07, D08, D10.

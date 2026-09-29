# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4
- Tên nhóm: AIDAS
- Repo Public: https://github.com/ThanhLong012/K4-DAY11-AIDAS
- Máy giữ hồ sơ chính / người quản lý: máy của Bùi Thành Long
- Slice chung lấy từ mode.json: B4-center
- Tên định danh vai A dùng cho --self: nam
- Kênh trao đổi nội bộ: Discord
- Đại diện nộp (vai C): Bùi Thành Long, 02147
- Commit chốt bài: https://github.com/ThanhLong012/K4-DAY11-AIDAS/commit/9d0bd3fbd48e2db057b56450d6c1e459a7edd71f

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Trương Công Hoài Nam | 02137 | nam | Parking/C0/slice, self-QC, lock, rework | Parking export (1049d43); C0 lock/compare (4f9e709); gán nhãn và khoá B4-center 9454-EBC8 (04758d9, 8b1c1d7, 64a4cf6); degrade stretch/k12 (6c9ae7c); bản rework `B4-center-update.zip` (f6f41b5) |
| B · QA độc lập | Nghiêm Trà My | 02239 | my | Review trước reference, finding QA, kiểm lại ca sửa | QA mù `r2_qa/qa_review.md`, `qa_overlay.html` và 6 dòng `r2_qa` trong findings (7d1188a, 4c0e9ea, 2071bd4, b6d3806); viết lại `parking/observations.md` (8d01970, 1d8c351) |
| C · Chẩn đoán & điều phối | Bùi Thành Long | 02147 | long | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | Setup và phân vai (6ee2b50), `sensor_context.md` (08e9832), findings C0 và bản nháp kế hoạch (844a385); P4 chẩn đoán `r3_diag`, zone table, 3 escalation ticket, decision log D01–D10; lock rework và `delta.md`; P6 error card, guideline patch, review plan, exit ticket, hoàn thiện 45/46; `check` |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung (B4-center) và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | C → A, B | mode.json (slice B4-center, --self nam), phân vai, sensor_context.md; commit 6ee2b50, 08e9832 | B: chạy doctor trên máy mình, không có dòng ✗ (Python 3.12, CVAT 2.74.1); repo xác nhận Public qua GitHub API | Xong. Parking: A vẽ và export (1049d43), C viết observations (844a385), B chỉnh lại (8d01970) |
| P2 · Khóa bản đầu | A → B, C | r1_craft/annotations.xml, lock.txt, selfqc.md, r1-final.zip; slice B4-center; mã 9454-EBC8; commit 8b1c1d7, 64a4cf6 | C: SHA của XML trong r1-final.zip và trên GitHub khớp lock.txt; 3 frame đủ, 271039 không có ego_body; chạy lại selfqc trên bản khoá chỉ còn cảnh báo tên task (đã kiểm trên CVAT là đúng, D04) | Đã khoá. Degrade stretch, k12 (D03). Máy C lệch SHA do autocrlf, đã xử lý (D05); B dùng r1-final.zip khi chạy qa |
| P3 · Chốt QA mù | B → C, A | `r2_qa/qa_review.md`, `qa_overlay.html`, 6 dòng `r2_qa`; commit 7d1188a → b6d3806 | C: QA chạy với mã 9454-EBC8 trước khi mở reference; 6 nhận xét có frame và rule_id; C điền `slice` và tên frame đầy đủ để `triage` hợp lệ | Xong. Nhận xét dùng số ID CVAT (#16, #24…) thay mã L và chưa có nhận xét cho `270517`; C đối chiếu sang mã L trong cột `note` |
| P4 · Quyết định sửa | C → A, B | findings `r3_diag`, `zone_table.md`, `30_escalation_ticket.md`, decision log D06–D09; chọn rework R4, R10 ở `271039` | A: nhận 2 ca rework và ảnh đánh dấu vị trí | Xong. 3 ca escalate (ego_body reference, xe tải nhỏ, lái/dắt xe) |
| P5 · Kiểm bản sửa | A → B → C | `B4-center-update.zip` (f6f41b5) → `rework/annotations-v2.xml`, `lock2.txt` mã 4B5A-FC5E, `delta.md` | C: so bản sửa với bản khoá: thêm R4 đúng, chưa có R10, thêm 1 box trùng (L6); edge missing 1→0, center spurious 4→5 | Khoá với kết quả 1/2 ca (D10). B đã kiểm lại `delta.md` và ảnh, xác nhận qua Discord |
| P6 · Chốt nộp | A, B → C | `manifest.json`, commit chốt 9d0bd3f | C: `python3 lab11.py check` báo "Hồ sơ hình thức đầy đủ" | Chờ A, B xác nhận mục 5 rồi push |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: `adasind_271039.jpg` xe trắng góc trái (QA gọi Car #16, là L5), R04. B hỏi là van chở người (Car) hay e-rickshaw (ThreeWheeler); A gán Car, reference R7 cũng Car, ảnh cho thấy ô tô con. C quyết định giữ Car (ghi trong `note` của dòng `r2_qa` Car #16).
- Ca còn mở: (1) `adasind_295948.jpg` L3/R3, lái hay dắt xe đạp (R03): A và B chọn Pedestrian, reference chọn Bike; người theo dõi qa; phép kiểm tiếp theo là xem frame liền kề (Ticket 3, D08). (2) R10 ở `271039` và box trùng L6 sau rework chưa sửa (D10).
- Đóng góp của A/B/C vào kế hoạch và exit ticket: C viết `45_sampling_plan.csv`, `46_gold_set_plan.md`, `45_review_plan.md`, `50_exit_ticket.md` dựa trên lỗi A gặp (bỏ sót người trong cụm) và các ca B nêu (xe trắng, lái/dắt xe); phần đóng góp từng người ghi cuối `50_exit_ticket.md`.
- Người soạn / người kiểm từng kế hoạch:

  | File | Người soạn | Người kiểm |
  |---|---|---|
  | `45_sampling_plan.csv` | C · Bùi Thành Long | B · Nghiêm Trà My |
  | `46_gold_set_plan.md` | C · Bùi Thành Long | B · Nghiêm Trà My |
  | `45_review_plan.md` | C · Bùi Thành Long | B · Nghiêm Trà My |
  | `50_exit_ticket.md` | C · Bùi Thành Long (tổng hợp ý A, B) | B · Nghiêm Trà My |
- Thay đổi phân công nếu có: không đổi vai. C viết `parking/observations.md` thay A ở P0 để kịp giờ, sau đó B chỉnh lại.

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Trương Công Hoài Nam / `r1-final.zip` khớp lock 9454-EBC8 (8b1c1d7); `B4-center-update.zip` khớp lock2 4B5A-FC5E (f6f41b5)
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Nghiêm Trà My / QA mù push lúc 22:26–22:32 (7d1188a → b6d3806), trước khi mở reference (22:38, `r1_craft/reference.txt`); đã kiểm lại ca sửa P5 (`rework/delta.md`, ảnh `adasind_271039.jpg`) và xác nhận qua Discord
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Bùi Thành Long / `python3 lab11.py check` exit 0, "Hồ sơ hình thức đầy đủ"
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

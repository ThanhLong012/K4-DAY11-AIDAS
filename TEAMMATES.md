# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4
- Tên nhóm: AIDAS
- Repo Public: https://github.com/ThanhLong012/K4-DAY11-AIDAS
- Máy giữ hồ sơ chính / người quản lý: máy của Bùi Thành Long
- Slice chung lấy từ mode.json: B4-center
- Tên định danh vai A dùng cho --self: nam
- Kênh trao đổi nội bộ: [Điền]
- Đại diện nộp (vai C): Bùi Thành Long, 02147
- Commit chốt bài: [SHA hoặc URL commit]

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Trương Công Hoài Nam | 02137 | nam | Parking/C0/slice, self-QC, lock, rework | [Link file/commit và mô tả phần đã làm] |
| B · QA độc lập | Nghiêm Trà My | 02239 | my | Review trước reference, finding QA, kiểm lại ca sửa | [Link file/commit và mô tả phần đã làm] |
| C · Chẩn đoán & điều phối | Bùi Thành Long | 02147 | long | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | [Link file/commit và mô tả phần đã làm] |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung (B4-center) và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | C → A, B | mode.json (slice B4-center), phân vai, [commit] | [Điền] | [Điền] |
| P2 · Khóa bản đầu | A → B, C | [XML, lock.txt, slice, code, commit] | [Điền] | [Điền] |
| P3 · Chốt QA mù | B → C, A | [review, findings, ảnh, commit] | [Điền] | [Điền] |
| P4 · Quyết định sửa | C → A, B | [finding, decision log, commit] | [Điền] | [Điền] |
| P5 · Kiểm bản sửa | A → B → C | [v2, lock2, review kiểm lại, delta] | [Điền] | [Điền] |
| P6 · Chốt nộp | A, B → C | [manifest, commit chốt] | [Điền] | [Điền] |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: [Frame/object/rule; ý kiến A/B; bằng chứng; quyết định và link]
- Ca còn mở: [Nội dung, người theo dõi, phép kiểm tiếp theo; nếu không còn thì ghi rõ]
- Đóng góp của A/B/C vào kế hoạch và exit ticket: [Điền phần việc thực tế]
- Thay đổi phân công nếu có: [Thời điểm, lý do, người nhận; nếu không đổi thì ghi rõ]

## 5. Xác nhận trước khi nộp

- [ ] A xác nhận nhãn và export đúng phiên bản: [Tên / bằng chứng]
- [ ] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: [Tên / bằng chứng]
- [ ] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: [Tên / bằng chứng]
- [ ] manifest.json tại commit chốt có failed_gates rỗng.
- [ ] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [ ] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

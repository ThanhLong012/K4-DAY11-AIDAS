# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 12 | 2 | 4 | 4 | 7 | SPURIOUS (3) |
| mid | 5 | 1 | 1 | 2 | 4 | WRONG_CLASS (1) |
| edge | 3 | 1 | 0 | 1 | 1 | MISSING (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: **center** có nhiều lỗi nhất về số tuyệt đối ở cả hai phía (L: 2 missing + 4 spurious trên n_ref=12; M: 4 missing + 7 thừa). Nhưng center cũng chứa nhiều vật nhất; tính theo tỉ lệ thì L gãy ở **edge** (1/3 vật reference bị thiếu, là người R4 ở mép phải `271039`) còn M thừa nhiều nhất ở **mid** (4 box thừa trên n_ref=5). 3 trong 4 spurious center của L (`271039` L2, L3; `295948` L9) là vật reference không box chứ không phải annotator vẽ bậy.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: (1) Lỗi của **L** chủ yếu là bỏ sót người nhỏ hoặc bị che trong cụm đông (`271039` R4, R10), không do méo fisheye: box khớp reference đều bám sát. (2) Lỗi của **M** có mẫu lặp: gọi xe ba bánh (auto-rickshaw) là Car/Truck ở 5 xe trên 2 frame và vẽ box cho người ngồi trong xe ba bánh (R03), nên là lỗi domain của model chứ không phải một box lệch. (3) Một phần chênh lệch đến từ **reference**: `ego_body` hình chữ nhật ở `295948` trùm cả người đi đường (5 box L thành IGNORE_SCOPE), và xe tải nhỏ bị gán Car. (4) Giới hạn: chỉ 3 frame, 20 vật reference, edge chỉ có 3 vật nên một lỗi đã là 33%; không đủ để kết luận zone nào khó hơn, chỉ đủ nêu giả thuyết cần kiểm trên slice lớn hơn.

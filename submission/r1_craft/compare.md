# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_270517.jpg
## adasind_271039.jpg
- L2 center SPURIOUS
- L3 center SPURIOUS
- R4 edge MISSING
- R10 center MISSING
## adasind_295948.jpg
- L1 mid IGNORE_SCOPE
- L2 mid IGNORE_SCOPE
- L6 center IGNORE_SCOPE
- L7 mid IGNORE_SCOPE
- L8 mid IGNORE_SCOPE
- L3+R3 mid WRONG_CLASS
- L4+R1 center WRONG_CLASS
- L9 center SPURIOUS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 12 | 10 | 2 | 4 |
| mid | 5 | 4 | 1 | 1 |
| edge | 3 | 2 | 1 | 0 |

# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): (1) vạch chia ô ở hàng giữa, bên trái, chạy chéo từ
  khoảng (170, 520) xuống (247, 563); (2) vạch chia ô ở tiền cảnh bên phải, từ khoảng (698, 622) tới mép phải ảnh
  (960, 685). Cả hai là đoạn sơn trắng ngăn hai ô đỗ cạnh nhau, polyline dừng ở chỗ vạch hết sơn hoặc ra khỏi khung.
  Tổng cộng export có 22 `parking_line`, gồm các vạch chia ô ở hàng xa, hàng giữa và tiền cảnh.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: dấu sơn trắng sát mép dưới giữa ảnh (khoảng x≈340–390,
  y≈712–720) chỉ thấy một phần nhỏ, không xác định được là vạch chia ô hay ký hiệu mặt đường, nên không gọi là
  `parking_line`. Các vạch ở hàng xa nhất gần xe đỏ (y < 485) quá nhỏ và mờ, không phân biệt được từng ô nên cũng
  không vẽ.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: polygon chính phủ lối xe chạy giữa hàng ô giữa và hàng ô
  tiền cảnh, cạnh trên dừng ở đầu các vạch hàng giữa (y≈520–580), cạnh dưới dừng ở đầu các vạch tiền cảnh
  (y≈590–680), trải hết chiều ngang ảnh. Hai polygon mảnh phía xa (y≈485–522) là lối xe chạy giữa các hàng ô xa.
  Bãi gần như trống nên không có xe hay vật che trong các polygon; xe đỏ ở xa nằm ngoài polygon.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): (1) hai polyline dài nằm ngang chạy dọc giữa hàng ô
  giữa (từ (1, 542) tới (659, 518) và từ (553, 508) tới (834, 531)): có thể là vạch giữa hai dãy ô quay đầu vào nhau
  (chia ô), nhưng cũng có thể là dải sơn dẫn lối xe, khi đó không phải `parking_line`. (2) Các vạch ở hàng xa bị mờ
  và rất ngắn (vài pixel) nên khó chắc là vạch chia ô; hai polygon `free_space` phía xa cũng mảnh và ranh giới kém
  chắc chắn hơn polygon chính.

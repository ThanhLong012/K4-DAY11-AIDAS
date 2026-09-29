# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh):
  Vạch 1 là gạch sơn trắng gần thẳng đứng ở phía trái ảnh, cách mép trái khoảng 1/8 chiều ngang. Gạch này là ranh giới giữa hai ô đỗ liền kề, thấy rõ nên vẽ polyline dọc theo tâm vạch và dừng đúng chỗ sơn kết thúc.
  Vạch 2 là gạch sơn trắng ngắn nghiêng ở giữa-trái ảnh, cách mép trái khoảng 1/5 chiều ngang. Gạch này là cạnh bên của một ô đỗ, bị nghiêng do phối cảnh, được vẽ bằng một polyline ngắn, chỉ phần sơn nhìn thấy.

- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao:
 Các vạch rất nhỏ sát đường chân trời (xa camera, vùng mặt đường bị cháy sáng) cũng không vẽ hết vì quá mờ và chỉ dài vài pixel, không xác định được hướng và vị trí.

- Polygon `free_space` dừng ở đâu; có phần bị che nào không:
  Polygon `free_space` phủ dải mặt nhựa trống ở tiền cảnh, từ mép trái đến mép phải ảnh. Cạnh trên dừng ở hàng vạch ô đỗ phía xa, cạnh dưới dừng ở hàng vạch trắng dày gần camera. Xe, cây, hàng rào và cột đèn đều nằm ngoài polygon. Không có vật nào che mặt đường trong vùng này. Phía xa mặt đường bị cháy sáng nên ranh giới ở đó chỉ là ước lượng.

- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”):
  Phần phía xa, gần đường chân trời: mặt đường bị cháy sáng và các vạch quá nhỏ, mờ nên không rõ ở đó có vạch ô đỗ thật hay không.
  Vùng giữa `free_space` và `parking_line` ở phía xa: chỉ thấy vạch trắng ngang/chéo, không có vạch dọc để chia thành từng ô, nên không rõ đây có phải chỗ đỗ xe hay chỉ là làn đường di chuyển. Cần người soát xác nhận vùng này có nên tính là `free_space` (chỗ đỗ trống) hay không.

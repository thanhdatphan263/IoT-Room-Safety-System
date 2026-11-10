# IoT-Room-Safety-System
Hệ thống an ninh và cắt điện khẩn cấp chống cháy nổ 


## 1. Giới thiệu đề tài
Đề tài xây dựng một thiết bị phần cứng thông minh ứng dụng vi điều khiển ESP32, kết hợp giao thức truyền thông MQTT và hệ thống giám sát Node-RED Dashboard. Thiết bị này đóng vai trò như một trạm kiểm soát môi trường và ngắt điện tự động nhằm phòng chống cháy nổ cho các khu phòng trọ hoặc chung cư mini.

## 2. Vấn đề thực tế và giải pháp

* Trong đời sống hiện nay, tình trạng sử dụng nhiều thiết bị điện cắm sạc qua đêm như laptop, xe điện, điện thoại tại các phòng trọ sinh viên tiềm ẩn nguy cơ chập cháy, rò rỉ khí gas rất cao nhưng người vắng nhà không thể hay biết kịp thời.
  
* Các thiết bị báo cháy thông thường chỉ phát ra tiếng kêu tại chỗ, không có khả năng tự động xử lý nguồn điện hay cảnh báo từ xa cho người dùng khi có sự cố xảy ra đột ngột.
  
* Đề tài tạo ra một hệ thống bảo vệ chủ động. Hệ thống liên tục đo đạc các thông số môi trường như nhiệt độ, độ ẩm, khói, khí gas, lửa. Khi phát hiện các dấu hiệu bất thường vượt ngưỡng an toàn, ESP32 sẽ lập tức tự động kích hoạt Module Relay để cắt nguồn điện của khu vực nguy cơ, đồng thời bật còi hú báo động tại chỗ và bắn tín hiệu khẩn cấp qua MQTT về giao diện Node-RED để đẩy thông báo lập tức về điện thoại, giúp ngăn chặn hỏa hoạn từ sớm.

## 3. Danh mục phần cứng 
* Vi điều khiển ESP32 Dev Board.
* Cảm biến khói và khí gas MQ-2.
* Cảm biến lửa và cảm biến nhiệt độ, độ ẩm DHT22.
* Module Relay 5V đóng vai trò công tắc tự động ngắt nguồn điện ổ cắm.
* Còi báo động công suất cao và đèn LED cảnh báo.

## 4. Nguyên lý hoạt động
* Giám sát môi trường: Cảm biến liên tục đo đạc nhiệt độ, độ ẩm và nồng độ khí gas/khói trong phòng, truyền dữ liệu qua MQTT để hiển thị biểu đồ theo dõi trực quan trên Node-RED Dashboard.
* Trạng thái bình thường: Hệ thống hoạt động ổn định, duy trì cấp điện và cập nhật thông số liên tục lên đám mây.
* Xử lý sự cố khẩn cấp: Khi cảm biến phát hiện khói, khí gas rò rỉ hoặc nhiệt độ tăng đột biến, ESP32 ngay lập tức ngắt Relay để cắt điện ổ cắm, kích hoạt còi hú lớn tại phòng, đồng thời gửi bản tin cảnh báo khẩn cấp qua MQTT lên Node-RED để đẩy thông báo về điện thoại của người dùng.

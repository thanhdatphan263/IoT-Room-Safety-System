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
  
 <img width="433" height="176" alt="ESP32" src="https://github.com/user-attachments/assets/1735eec2-0252-49ac-9c02-af34375850f7" />
 
* Cảm biến khói và khí gas MQ-2.
  
 <img width="224" height="149" alt="cam_bien_gas_MQ-2" src="https://github.com/user-attachments/assets/3ab718a1-680b-4f48-84ba-199447c78d49" />
 
* Cảm biến lửa và cảm biến nhiệt độ, độ ẩm DHT22.
  
 <img width="256" height="268" alt="cam_bien_DHT22" src="https://github.com/user-attachments/assets/6663055e-5127-4d3c-832c-24b01aacc0bf" />
 
* Module Relay 5V đóng vai trò công tắc tự động ngắt nguồn điện ổ cắm.
  
 <img width="263" height="211" alt="RELAY_5V" src="https://github.com/user-attachments/assets/d5147bed-15be-4972-80d8-a40d93196f25" />
 
* Còi báo động công suất cao.
  
<img width="265" height="221" alt="LED" src="https://github.com/user-attachments/assets/8e76f9b4-cca6-4b09-b365-65813fd4b46f" />

*đèn LED cảnh báo

<img width="254" height="117" alt="BUZZER" src="https://github.com/user-attachments/assets/89e3eae8-7bbd-42ca-9f91-6fa12755f9f9" />
## 4. Sơ đồ khối kết nối

<img width="1626" height="497" alt="so_do_room" src="https://github.com/user-attachments/assets/40055805-c35b-4d66-a9cc-8c19ad3dc915" />


## 5. Nguyên lý hoạt động
* Giám sát môi trường: Cảm biến liên tục đo đạc nhiệt độ, độ ẩm và nồng độ khí gas/khói trong phòng, truyền dữ liệu qua MQTT để hiển thị biểu đồ theo dõi trực quan trên Node-RED Dashboard.
* Trạng thái bình thường: Hệ thống hoạt động ổn định, duy trì cấp điện và cập nhật thông số liên tục lên đám mây.
* Xử lý sự cố khẩn cấp: Khi cảm biến phát hiện khói, khí gas rò rỉ hoặc nhiệt độ tăng đột biến, ESP32 ngay lập tức ngắt Relay để cắt điện ổ cắm, kích hoạt còi hú lớn tại phòng, đồng thời gửi bản tin cảnh báo khẩn cấp qua MQTT lên Node-RED để đẩy thông báo về điện thoại của người dùng.

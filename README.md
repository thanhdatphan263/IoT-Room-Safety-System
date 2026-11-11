# IoT-Room-Safety-System
Hệ thống an ninh và cắt điện khẩn cấp chống cháy nổ 

## 1. Giới thiệu đề tài
Đề tài xây dựng một thiết bị phần cứng thông minh ứng dụng vi điều khiển ESP32, kết hợp giao thức truyền thông MQTT và hệ thống giám sát Node-RED Dashboard. Thiết bị này đóng vai trò như một trạm kiểm soát môi trường và ngắt điện tự động nhằm phòng chống cháy nổ cho các khu phòng trọ hoặc chung cư mini.

## 2. Vấn đề thực tế và giải pháp

* Trong đời sống hiện nay, tình trạng sử dụng nhiều thiết bị điện cắm sạc qua đêm như laptop, xe điện, điện thoại tại các phòng trọ sinh viên tiềm ẩn nguy cơ chập cháy, rò rỉ khí gas rất cao nhưng người vắng nhà không thể hay biết kịp thời.
  
* Các thiết bị báo cháy thông thường chỉ phát ra tiếng kêu tại chỗ, không có khả năng tự động xử lý nguồn điện hay cảnh báo từ xa cho người dùng khi có sự cố xảy ra đột ngột.
  
* Đề tài tạo ra một hệ thống bảo vệ chủ động. Hệ thống liên tục đo đạc các thông số môi trường như nhiệt độ, độ ẩm, khói, khí gas, lửa. Khi phát hiện các dấu hiệu bất thường vượt ngưỡng an toàn, ESP32 sẽ lập tức tự động kích hoạt Module Relay để cắt nguồn điện của khu vực nguy cơ, đồng thời bật còi hú báo động tại chỗ và bắn tín hiệu khẩn cấp qua MQTT về giao diện Node-RED để đẩy thông báo lập tức về điện thoại, giúp ngăn chặn hỏa hoạn từ sớm.

## 3. Danh mục phần cứng 

| STT | Tên linh kiện | Số lượng | Chức năng |
| :---: | :--- | :---: | :--- |
| 1 | **Vi điều khiển ESP32 Dev Board**<br><br><img width="150" src="https://github.com/user-attachments/assets/1735eec2-0252-49ac-9c02-af34375850f7" /> | 1 | - Quản lý logic toàn bộ hệ thống an ninh và phòng chống cháy nổ.<br>- Đọc dữ liệu liên tục từ các cảm biến (MQ-2, DHT22, cảm biến lửa).<br>- Điều khiển module relay cắt điện, kích hoạt còi và đèn LED, đồng thời truyền tải trạng thái qua giao thức MQTT lên Node-RED. |
| 2 | **Cảm biến khói và khí gas MQ-2**<br><br><img width="120" src="https://github.com/user-attachments/assets/3ab718a1-680b-4f48-84ba-199447c78d49" /> | 1 | - Phát hiện sự xuất hiện của khói, khí gas rò rỉ (LPG, Propane, Methane) trong phòng.<br>- Cung cấp tín hiệu cảnh báo khi nồng độ khí cháy vượt ngưỡng an toàn. |
| 3 | **Cảm biến nhiệt độ, độ ẩm DHT22**<br><br><img width="120" src="https://github.com/user-attachments/assets/6663055e-5127-4d3c-832c-24b01aacc0bf" /> | 1 | - Đo lường chính xác nhiệt độ và độ ẩm không khí môi trường thời gian thực.<br>- Cung cấp dữ liệu nhiệt độ phòng để giám sát sớm nguy cơ quá nhiệt gây cháy nổ. |
| 4 | **Cảm biến lửa (Flame Sensor)**<br><br><img width="120" src="https://github.com/user-attachments/assets/cc8dfb6c-e9dc-4316-ba5c-1c4f72fbd771" /> | 1 | - Phát hiện bức xạ ánh sáng hồng ngoại phát ra từ ngọn lửa trần.<br>- Giúp hệ thống nhận diện nhanh chóng sự cố hỏa hoạn để kích hoạt quy trình cắt điện khẩn cấp. |
| 5 | **Module Relay 5V**<br><br><img width="120" src="https://github.com/user-attachments/assets/d5147bed-15be-4972-80d8-a40d93196f25" /> | 1 | - Đóng vai trò là công tắc điện tử công suất lớn.<br>- Tự động ngắt nguồn điện ổ cắm hoặc thiết bị điện ngay lập tức khi ESP32 phát hiện tín hiệu nguy hiểm từ các cảm biến. |
| 6 | **Đèn LED báo hiệu**<br><br><img width="120" src="https://github.com/user-attachments/assets/8e76f9b4-cca6-4b09-b365-65813fd4b46f" /> | 1 | - Cung cấp tín hiệu cảnh báo trực quan tại chỗ.<br>- Hiển thị trạng thái hoạt động bình thường hoặc chớp nháy cảnh báo khi có sự cố nguy hiểm xảy ra trong phòng. |
| 7 | **Còi Buzzer**<br><br><img width="120" src="https://github.com/user-attachments/assets/89e3eae8-7bbd-42ca-9f91-6fa12755f9f9" /> | 1 | - Phát ra âm thanh cảnh báo lớn tại chỗ.<br>- Cảnh báo trực tiếp cho người trong phòng ngay khi phát hiện khói, khí gas rò rỉ hoặc có ngọn lửa. |

## 4. Sơ đồ khối kết nối

<img width="835" height="549" alt="IOT_ROOM_SODOKHOI" src="https://github.com/user-attachments/assets/d0466328-98cf-4be7-8e28-0223066e8871" />



## 5. Nguyên lý hoạt động
* Giám sát môi trường: Cảm biến liên tục đo đạc nhiệt độ, độ ẩm và nồng độ khí gas/khói trong phòng, truyền dữ liệu qua MQTT để hiển thị biểu đồ theo dõi trực quan trên Node-RED Dashboard.
* Trạng thái bình thường: Hệ thống hoạt động ổn định, duy trì cấp điện và cập nhật thông số liên tục lên đám mây.
* Xử lý sự cố khẩn cấp: Khi cảm biến phát hiện khói, khí gas rò rỉ hoặc nhiệt độ tăng đột biến, ESP32 ngay lập tức ngắt Relay để cắt điện ổ cắm, kích hoạt còi hú lớn tại phòng, đồng thời gửi bản tin cảnh báo khẩn cấp qua MQTT lên Node-RED để đẩy thông báo về điện thoại của người dùng.

## 6. Lưu đồ thuật toán

<img width="269" height="498" alt="luu_do_thuat_toan ROOM" src="https://github.com/user-attachments/assets/60490453-1daf-4699-8331-df0037b0d30b" />

  
## 7. Tài liệu tham khảo & Datasheet

* [ESP32 Datasheet - Espressif Systems](https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf)
* [MQ-2 Gas Sensor Datasheet - SparkFun](https://www.sparkfun.com/datasheets/Sensors/Biometric/MQ-2.pdf)
* [Flame Sensor Module Specification - Components101](https://components101.com/sensors/flame-sensor-module)
* [Relay and Contactor Application Guide - Electronics Tutorials](https://www.electronics-tutorials.info/io/io_7.html)
* [Piezo Buzzer Working Principle - Electronic Hub](https://www.electronicshub.org/piezo-buzzer/)
* [PubSubClient MQTT Library Documentation](https://github.com/knolleary/pubsubclient)
* [Node-RED Documentation](https://nodered.org/docs/)

# ESP32 Traffic-Light Control — Web UI + MD5-auth JSON

Hệ thống điều khiển **14 cột đèn giao thông** trên bản đồ qua Web UI, hỗ trợ **Manual/Auto**, đặt thời gian **G/Y/R**, và đồng bộ **phase + countdown** theo thời gian thực (poll 1s). Đi kèm **Python CLI** để build/gửi gói **JSON + MD5** qua Serial và verify phản hồi.

## Tech stack
- **Firmware/IoT:** ESP32 (Arduino)
- **Frontend:** HTML, CSS, JavaScript
- **Tools:** Python 3 (pyserial, hashlib), JSON

## Tính năng chính
- **Bản đồ + 14 đèn:** click đổi trạng thái R/Y/G, popup chọn màu.
- **Chế độ Manual/Auto** + đặt **thời gian G/Y/R** (Apply).
- **Realtime status:** cập nhật mode, phase, và countdown mỗi giây.
- **Chống ghi đè khi nhập:** edit-lock theo trường trong UI.
- **Python CLI (`esp32_pkt_tool.py`):**
  - Build gói JSON theo thứ tự khóa `id_src, id_des, opcode, time, data, auth`.
  - Tạo **auth MD5** từ payload + key; gửi qua Serial (tùy chọn baud, LF/CRLF/CR).
  - **Verify** phản hồi (so khớp MD5) để đảm bảo toàn vẹn.

## Kết quả
Điều khiển đồng thời 14 cột đèn, chuyển Manual/Auto tức thời, đếm ngược rõ ràng; kênh lệnh **có kiểm chứng toàn vẹn** (MD5) chiều đi/về.

---

### (EN) Resume Summary
**ESP32 Traffic-Light Control — Web UI & MD5-secured JSON.**  
Interactive map controlling **14 traffic lights** with **Manual/Auto** modes and configurable **G/Y/R** timings; **1-second polling** for real-time phase & countdown. Authored a **Python CLI** to build/send **MD5-signed JSON** over Serial and **verify** responses for integrity. Tech: ESP32 (Arduino), HTML/CSS/JS, Python.

## 📦 Thư viện sử dụng
Project sử dụng các thư viện chính sau:
- **Wifi** –  WiFi SoftAP cho ESP32 
- **WebServer** – HTTP server nhúng (port 80)
- **Wire** – I2C dùng cho PCF8575
- **PCF8575** – Dùng thư viện của xreef
- **SPIFFS** – Lưu các file trong thư mục data vào flash. Link video hướng dẫn cài tool: https://youtu.be/9i1nDUoDRcI?si=-pUQmOpcrhJP6nr6  
- **ArduinoJson** – Parse/serialize JSON cho HTTP/Serial
- **MD5Builder** – Tạo MD5


## 📂 Cấu trúc dự án
Project/    
    ├── Image
    ├── Schematic
    ├── Sourcecode/
        └── Source code
            ├── Sourcode.ino     #code firmware 
            ├── data/       # data để lưu vào flash của esp32
                    ├── Index.html  # Giao diện webapp
                    ├── script.js   # Thực thi chắc năng webapp
                    ├── style.css   # phong cách của webapp
                    ├── map.PNG
                    ├── traffic_base.PNG
                    ├── traffic_green.PNG
                    ├── traffic_yellow.PNG
                    ├── traffic_red.PNG       
        └──esp32_pkt_tool.py  # công cụ tạo file JSON

## ⚙️ Cách cài đặt
- Hướng dẫn cài tool SPIFFS: https://youtu.be/9i1nDUoDRcI?si=-pUQmOpcrhJP6nr6  

## ⬆️ Hướng dẫn upload firmware
- Arduino IDE cài đặt các thư viện cần thiết, và tool để up file quá SPIFFS theo video hướng dẫn ở trên. Biên dịch và nạp code
- Chọn board esp32s3-devmodule
- Chọn COM phù hợp sau đó nhấn upload
Lưu ý:
- Phiên bản esp32 2.0.15
- Thư viện PCF8575 của XREEF. Link tải: https://github.com/xreef/PCF8575_library

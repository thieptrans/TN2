### Xác định lỗi XSS

![image](https://github.com/user-attachments/assets/40359f29-da49-4ce0-bef2-b0908673a9ae)

Thử nhập dữ liệu và xem kết quả

![image](https://github.com/user-attachments/assets/545a6269-6aee-485b-966a-e9b75e27d97b)

Kết quả cho thấy kết quả trả về khi nhập dữ liệu gửi lên server

### kiểm tra XSS

Thử chèn một đoạn js vào xem 
> <script>alert("XSS")</script>

![image](https://github.com/user-attachments/assets/c20851a1-3942-4eac-881a-0b11c3cafb9d)

Xác định dính XSS

View source thấy đoạn js đã được lưu vào server nên mỗi khi ta nhập cái gì đó thì cái xss cũ lại chạy

![image](https://github.com/user-attachments/assets/2f979c09-6ea0-49ff-b7a5-788f56383e33)

### Khai thác

Sử dụng trang web phishing như bài eval

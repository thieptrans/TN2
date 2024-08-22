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

Tương tự như case Low, ta encode 

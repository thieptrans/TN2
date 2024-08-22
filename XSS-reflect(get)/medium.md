Thực hiện như case Low, ta thấy khi nhập js vào ô bất kì đều không có respond.

![image](https://github.com/user-attachments/assets/50fcf1b2-09d2-4e96-9d61-ab86e2ea66a2)

Kiểm tra mã nguồn ta thấy vẫn có dòng 

![image](https://github.com/user-attachments/assets/ae6beda1-3c26-4dc6-adce-732b2454f0f6)

Đoạn java script không được thực hiện do cơ chế lọc kí tự. Bây giờ thử 1 số cách đã được nêu trong phần giới thiệu. Khi thực hiện truyền 1 đoạn java script <script>alert(String.fromCharCode(88, 83, 83))</script> thu được kết quả:

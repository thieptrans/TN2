### Xác định lỗi XSS

Thử nhập họ tên vào ô tìm kiếm ta thấy nó trả về tên ta nhập

![image](https://github.com/user-attachments/assets/19b1795e-3b9d-41ed-a3d6-60b0b9161109)

Chèn thử dòng js vào để check XSS và thấy nó trả về kết quả rất kì lạ

![image](https://github.com/user-attachments/assets/e5fc5be5-11ab-485e-bf0c-d9dd6586fb5b)

Nhập tên bất kì rồi View source, ta chú ý đến dòng chưa dữ liệu vừa nhập

![image](https://github.com/user-attachments/assets/6c545d31-ea44-440f-97ed-026b0e45bc04)

Lí do đoạn js trước đó không chạy là do đầu vào đang nằm sẵn trong một đoạn js

>var JSONResponseString = '{"movies":[{"response":"check here??? Sorry, we don&#039;t have that movie :("}]}';

Đoạn Js này được kết thúc bởi **"}]}';**

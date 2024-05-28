# Types of Internet Security Protocols
## Summary
- [Overview](#Overview)
- [TLS protocol](#TLSPotocol)
- [Exploit to RCE ](#Exploit-to-RCE )
## Overview
Trong thế giới ngày nay, chúng ta truyền dữ liệu với số lượng lớn và tính bảo mật của dữ liệu này là rất quan trọng, vì vậy bảo mật Internet cung cấp tính năng đó, tức là bảo vệ dữ liệu. Có nhiều loại giao thức khác nhau tồn tại như định tuyến, chuyển thư và giao thức liên lạc từ xa
## 1. TLS Potocol
Ở đây mình sẽ không đề cập tới SSL nữa vì TLS chính là cải thiện tốt hơn của SSL. Vậy TLS là gì, TLS - transport layer secure nó được sinh ra để đảm bảo 3 tính chất bảo mật sau: 
- Data encryption
- Authentication
- Data intergrity

<p align="center">
  <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/6fbbadee-3e3d-406a-9355-11d13cd23c45" alt="Dữ liệu truyền đi cần đảm bảo 3 tính bảo mật trên CIA">
</p>

Vậy để hiểu rõ hơn TLS là gì chúng ta sẽ lấy ví dụ thực tế sau: 
- Tại các dịch vụ của ngân hàng hoặc các dịch vụ khác số thẻ tín dụng, thông tin đăng nhập và thông tin nhạy cảm khác có thể bị kẻ tấn công chặn và đọc.
- Tại sao? Vì bất kỳ ai có ý định tốt hay xấu thì họ đều có thể phân tích lưu lượng mạng ( wireshark - phần mềm miễn phí) để có thể thu thập dữ liệu khi truyền tải. Vậy nếu dữ liệu không đảm bảo 3 yếu tố CIA trên thì nó sẽ bị sao?:
  - Thông tin có thể bị chặn và đọc được bởi attacker
  - Nếu không có TLS bạn sẽ không biết được bạn có đang giao tiếp với một trang web hợp pháp hay không. Vì hiện nay các trang web bị giả mạo rất nhiều chúng lừa người dùng truy cập vào trang web giả mạo đó và yêu cầu các thông tin nhạy cảm từ người dùng từ đó chúng sẽ dùng thông tin đánh cắp được để đăng nhập vào trang web hợp pháp.
  - Nếu không có TLS thì dữ liệu trên đường truyền có thể bị đánh cắp và sửa đổi dẫn đến nạn nhân nhận được những thông tin sai lệch
### 1.1 TLS hoạt động như thế nào
TLS bao gốm 2 giai đoạn:
- Giai đoạn 1: Handshake phase
- Giai đoạn 2: Encryption phase
- <p align="center">
  <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/8a03bc88-abc0-4a96-8227-4cb962cacbc8" alt="">
</p>

#### 1.1.1 Handshake phase 
- Mục đích chính của giai đoạn bắt tay này là **Authentication** vì trước khi làm bất cứ điều gì thì client cần tin tưởng vào danh tính của máy chủ mà nó đang giao tiếp.
- Vậy để tạo sự tin tưởng này máy chủ cần cung cấp một chứng chỉ TLS được cung cấp bởi bên thứ 3 và sau đó họ sử dụng phương thức khóa bất đối xứng để xác thực. Vậy làm thế nào để web server có được TLS certificate này:
  - **TLS certificate là một tệp dữ liệu chứa tên miền, cá nhân hoặc tổ chức sở hữu chứng chỉ, cơ quan cấp chứng chỉ, khóa chung của máy chủ và các dữ liệu khác**
    ![image](https://github.com/Giaduoc0211/5G-Security/assets/71538455/e9a901c9-b335-410b-9f17-0a39f5b8c5a0)

  - Để chứng chỉ TLS hợp lệ, nó cần phải được lấy từ certificate authority(CA).
    - CA là một tổ chức bên ngoài, một bên thứ ba đáng tin cậy tạo và cấp chứng chỉ TLS (SSL).

    - CA cũng sẽ ký điện tử vào chứng chỉ bằng khóa riêng của họ, cho phép các thiết bị khách xác minh nó.
  
    - Sau khi chứng chỉ được cấp, nó cần được cài đặt và kích hoạt trên máy chủ của trang web .
  
    - Dịch vụ lưu trữ web thường có thể xử lý việc này cho các nhà điều hành trang web.

    - Sau khi được kích hoạt trên máy chủ, trang web sẽ có thể tải qua HTTPS và tất cả lưu lượng truy cập đến và đi từ trang web sẽ được mã hóa và bảo mật.
      ![image](https://github.com/Giaduoc0211/5G-Security/assets/71538455/257fe9bc-8d13-4ebf-a7e3-1c61de791180)


- Mục đích thứ 2 của giai đoạn này là tạo được khóa chung giữa client và server được gọi là **symmetric key**. Khóa này sẽ được dùng ở giao đoạn thứ 2
- 
- 




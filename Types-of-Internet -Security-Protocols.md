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
- Vậy để tạo sự tin tưởng này máy chủ cần cung cấp một chứng chỉ TLS được cung cấp bởi bên thứ 3 và sau đó họ sử dụng phương thức khóa bất đối xứng để xác thực. Cùng phân tích cách hoạt động của nó ở dưới:
    - 
![image](https://github.com/Giaduoc0211/5G-Security/assets/71538455/7e5d94a1-308d-4968-991f-be711dac79b8)



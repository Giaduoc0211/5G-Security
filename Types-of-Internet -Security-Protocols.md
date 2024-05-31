# Types of Internet Security Protocols
## Summary
- [Overview](#Overview)
- [TLS protocol](#1._TLS_Potocol)
- [HTTPS protocol ](#HTTPSprotocol)
## Overview
Trong thế giới ngày nay, chúng ta truyền dữ liệu với số lượng lớn và tính bảo mật của dữ liệu này là rất quan trọng, vì vậy bảo mật Internet cung cấp tính năng đó, tức là bảo vệ dữ liệu. Có nhiều loại giao thức khác nhau tồn tại như định tuyến, chuyển thư và giao thức liên lạc từ xa
## 1. **TLS Potocol**
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
    <p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/e9a901c9-b335-410b-9f17-0a39f5b8c5a0" alt="">
    </p>
  - Để chứng chỉ TLS hợp lệ, nó cần phải được lấy từ certificate authority(CA).
    - CA là một tổ chức bên ngoài, một bên thứ ba đáng tin cậy tạo và cấp chứng chỉ TLS (SSL).

    - CA cũng sẽ ký điện tử vào chứng chỉ bằng khóa riêng của họ, cho phép các thiết bị khách xác minh nó.
  
    - Sau khi chứng chỉ được cấp, nó cần được cài đặt và kích hoạt trên máy chủ của trang web .
  
    - Dịch vụ lưu trữ web thường có thể xử lý việc này cho các nhà điều hành trang web.

    - Sau khi được kích hoạt trên máy chủ, trang web sẽ có thể tải qua HTTPS và tất cả lưu lượng truy cập đến và đi từ trang web sẽ được mã hóa và bảo mật.
    <p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/257fe9bc-8d13-4ebf-a7e3-1c61de791180" alt="">
    </p>
  
- Mục đích thứ 2 của giai đoạn này là tạo được khóa chung giữa client và server được gọi là **symmetric key**. Khóa này sẽ được dùng ở giao đoạn thứ 2.
- **Quá trình trao đổi tại giai đoạn 1 được thực hiện như sau:**
  - Webserver sẽ gửi cho client một TLS certificate và một public
     <p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/3f9b4a02-55ff-426e-8da3-ee4f40d3bb21" alt="">
    </p>
  -  Client xác thực TLS certificate mà server gửi tới. TLS certificate sẽ được xác minh bởi CA xem nó có bị chỉnh sửa hoặc thay đổi gì hay không
     <p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/689a1c9f-cb7a-4d96-8c44-21dc2f058314" alt="">
    </p>
  - Sau khi xác thực chứng chỉ xong Client sẽ tạo ra một chuôi random và sử dụng public key của web server để mã hóa và gửi lại cho server
   
  - Server sử dụng khóa private để giải mã và lấy ra chuỗi random client gửi tới
     <p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/fbbedebf-5887-4b8d-91d3-5471e2b6a3e8" alt="">
    </p>
  - Client và server sử dụng chuỗi random chung này để tạo ra khóa chung là session key
    <p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/7d8d8038-c480-4c77-9a70-c1fe62b5eddd" alt="">
    </p>
#### **1.1.2 Encryption phase**
- Sau giai đoạn bắt tay thì cả client và server đều có chung session key rồi
- Vậy chúng ta đã đảm bảo được tính chất bảo mật đầu tiên là authentication vậy còn 2 tính chất bảo mật nữa là intergrity và encryption.
- Ở giải đoạn 2 này TLS sử dụng thuật toán hash và mã hóa để đảm bảo 2 tính chất bảo mật ở trên
- Cứ mỗi lần dữ liệu được gửi đi nó sẽ được mã hóa và được hash bằng khóa MAC bí mật. Sau khi server gửi dữ liệu và client nhận được để đảm bảo dữ liệu không bị thay đổi trên đường truyền client sẽ xác thực chữ ký MAC nếu đúng thì tức là dữ liệu không bị thay đổi
  <p align="center">
        <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/a9b6f6c9-3590-4a3a-92c5-ead28928e484" alt="">
  </p>
### **1.2 TLS ảnh hưởng tới hiệu suất như nào**
- Hiện nay thì giao thức TLS 1.3 nó đã được hỗ trợ và nó giảm thiểu khá nhiều thời gian trong giai đoạn bắt tay. 
  <p align="center">
          <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/5489be60-2416-463f-865e-f8c1c0f37661" alt="">
  </p>

- Dưới đây là ảnh so sánh giữa TLS 1.2 và TLS 1.3
  <p align="center">
          <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/2dc7f54c-e734-41a5-b909-33904e7c0c6f" alt="">
  </p>
- Khác với TLS 1.2 thì TLS 1.3 nó thực hiện việc trao đổi khóa trong 2 bước đầu tiên thay vì tới tận bước 6 như của TLS 1.2.
- Phía client sẽ thực hiện liệt kê các giải thuật mã hóa mà phía bên server có thể lựa chọn để mã hóa và gửi nó tới cho server.
- Vì đã được liệt kê sẵn nên Server sẽ chọn một giải thuật mã hóa trong đó để mã hóa và từ đó client và server đều có khóa chung. Để hiểu rõ hơn mình sẽ mô tả một ví dụ cụ thể dưới đây.
  <p align="center">
          <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/2cc2e7ad-e1e0-46be-bfc0-832824b0cd54" alt="">
  </p>
- Như hình trên chúng ta có thể thấy thay vì chỉ gửi tin nhắn hello thì client đã gửi luôn cả các thông tin mã hóa của nó tới cho servre( cụ thể là client sử dụng giao thức Diffie-Hellman). Phía server nhận được thông tin này thì server cũng sử dụng loại giao thức tương ứng kết hợp với public key và thông tin của client gửi tới và tạo ra được khóa chung giữa client và server luôn.
## **2. HTTPS protocol**
HTTPS là giao thức mở rộng của HTTP và kết hợp lớp bảo mật. Khi một trình duyệt truy cập một trang web qua HTTPS, nó sẽ thiết lập một kết nối bảo mật sử dụng SSL/TLS để mã hóa dữ liệu được truyền tải giữa trình duyệt và máy chủ web.
⇒ Vậy tức là việc bảo mật của HTTP giống với TLS ở phần 1 mà mình đã mô tả
## **3. IPSEC protocol**
- **IPsec- IP security** là một giao thức được sử dụng để bảo mật dữ liệu khi truyền tải qua mạng internet đặc biệt là trong các kết nối VPN (Virtual Private Network).
- Vậy **VPN** là gì?VPN - Virtual private network là một dịch vụ bảo mật Internet cho phép người dùng truy cập Internet như thể họ được kết nối với mạng riêng. VPN mã hóa
  thông tin liên lạc trên Internet cũng như cung cấp mức độ ẩn danh cao.
- IPsec hoạt động tại lớp 3 - lớp network của mô hình OSI. Mục đích của IPsec là:
  - VPN (Virtual Private Network): Bảo vệ dữ liệu truyền qua các mạng không an toàn như Internet.
  - Bảo mật truyền thông: Bảo vệ các gói tin trong các mạng nội bộ và giữa các chi nhánh.
  - Remote Access: Cung cấp kết nối an toàn cho người dùng từ xa
- **Các chế độ hoạt động của IPsec**: Cả 2 chế độ này đều đảm bảo tính bảo mật toàn vẹn và replay tuy nhiên nó sẽ có mức độ bảo mật khác nhau và cách thức hoạt động khác nhau:
  - **Transport mode**: Trong chế độ này, chỉ có dữ liệu người dùng được mã hóa và bảo vệ, IP Header không bị thay đổi hay mã hóa. Transport Mode được sử dụng cho các kết nối VPN client-to-site.
  - **Các thức hoạt động:**
    - Mã hóa và xác thực: Trong chế độ vận chuyển, IPSec chỉ mã hóa và/hoặc xác thực phần tải dữ liệu (payload) của gói IP. Phần tiêu đề IP ban đầu không được mã hóa và vẫn còn nguyên vẹn.
    - Cơ chế bảo vệ: Chế độ này đảm bảo tính bảo mật và tính toàn vẹn của dữ liệu trong các gói tin, nhưng không che giấu địa chỉ IP gốc của các thiết bị giao tiếp.
  - **Ứng dụng**:
    - Giao tiếp giữa các thiết bị: Thường được sử dụng để bảo vệ giao tiếp giữa các thiết bị cá nhân, máy chủ, hoặc giữa máy chủ và máy khách. Ví dụ: bảo vệ dữ liệu truyền giữa một máy tính cá nhân và một máy chủ trong cùng một mạng nội bộ hoặc qua Internet.
    - Hiệu suất: Do chỉ mã hóa phần dữ liệu, chế độ vận chuyển có thể có hiệu suất tốt hơn so với chế độ đường hầm, nhất là khi không cần bảo mật toàn bộ gói IP.
  - **Tunnel mode:** Trong chế độ Tunnel, toàn bộ gói tin sẽ được bảo vệ, gồm IP header và payload. IPSec gói gói dữ liệu bên trong một packet mới, mã hóa nó và thêm một IP header mới. Nó thường được ứng dụng trong thiết lập VPN site-to-site.
    - **Hoạt động:**
      - Mã hóa toàn bộ gói IP: Trong chế độ đường hầm, toàn bộ gói IP gốc được mã hóa và đóng gói (encapsulated) trong một gói IP mới. Phần tiêu đề IP mới được thêm vào, và toàn bộ gói tin ban đầu (bao gồm cả tiêu đề IP gốc) được bảo vệ bên trong.
      - Bảo mật mạnh mẽ: Chế độ này cung cấp mức độ bảo mật cao hơn bằng cách che giấu toàn bộ thông tin trong gói tin ban đầu, bao gồm cả địa chỉ IP nguồn và đích.
    - **Ứng dụng:**
        - VPN (Virtual Private Network): Chế độ đường hầm chủ yếu được sử dụng để thiết lập các mạng riêng ảo (VPN) giữa các mạng LAN hoặc giữa các thiết bị đầu cuối và mạng LAN. Ví dụ: kết nối bảo mật giữa chi nhánh của một công ty và trụ sở chính qua Internet.
        - Remote Access: Cho phép người dùng từ xa truy cập vào mạng nội bộ của công ty một cách an toàn.   
  -  <p align="center">
          <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/aa85afc5-07e1-421f-aeda-2dc8c1db07a5" alt="">
  </p>
  <p align="center">
          <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/fea35eb1-bdb4-4e01-9ae2-41bf0b2ba462" alt="">
  </p>
- **Đi sâu hơn vào các thành phần của IPsec:**
  - **Authentication Header (AH):** Là một phần của giao thức IPSec, được sử dụng để cung cấp xác thực và tính toàn vẹn dữ liệu. AH sử dụng thuật toán băm để tạo mã xác thực cho gói tin, đảm bảo rằng gói tin không bị sửa đổi trên đường truyền
  - **Encapsulating Security Payload (ESP):** ESP đóng vai trò cung cấp tính toàn vẹn, xác thực và bảo mật cho dữ liệu được truyền trong mạng. Bằng cách sử dụng thuật toán để mã hóa dữ liệu trong gói tin, đảm bảo rằng thông tin chỉ được giải mã bởi duy nhất người nhận chính xác.
  - **Internet Key Exchange (IKE):** IKE có vai trò thiết lập các SA(security Associations) giữa hai điểm cuối trong mạng. IKE sử dụng các giao thức mã hóa khác nhau để bảo vệ các thông tin định danh và bảo mật trong quá trình thiết lập kết nối IPSec.
      - **Security Associations (SA):** Là các cơ chế định danh và xác thực cho các kết nối được bảo mật trong IPSec. SA bao gồm thông tin về cơ chế mã hóa, thuật toán xác thực, địa chỉ IP của người gửi và người nhận.
<p align="center">
<img src="" alt="">
</p>
<p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/c9e65ba1-8586-4f17-bc76-e83fcaa21f1e" alt="">
</p>
<p align="center">
      <img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/e4826593-e467-4a8f-9a00-04d5256d6028" alt="">
</p>

### **3.1 Cách thức hoạt động của IPsec**

Dưới đây là các bước hoạt động tổng quan của Ipsec: 
- **Giai đoạn 1:** Nhận dạng lưu lượng quan tâm
  - Sau khi một thiết bị mạng đã nhận được một packet, nó sẽ match với IPsec policy đã configured để mà xác định xem packet có cần được truyền qua một đường hầm IPsec hay không. Lưu lượng cần được truyền qua đường hầm IPsec sẽ được gọi là lưu lượng quan tâm.
- **Giai đoạn 2:** Đàm phán Security Association (SA) & Key exchange
  - SA xác định những yếu tố để truyền dữ liệu an toàn giữa 2 site. Nó bao gồm giao thức bảo mật, chế độ đóng gói dữ liệu, thuật toán mã hóa và xác thực và những key được sử dụng để truyền dữ liệu.
  - Sau đó sử dụng giao thức Internet Key Exchange (IKE) để mà thiết lập IKE SA để xác thực danh tính và trao đổi thông tin chính, sau đó là thiết lập IPsec SA để truyền dữ liệu an toàn dựa trên IKE SA
- **Giai đoạn 3:** Truyền dữ liệu
  - Sau khi IPsec SA đã được thiết lập giữa 2 site, chúng có thể truyền dữ liệu qua đường hầm IPsec.
  - Để đảm bảo được tính bảo mật khi truyền dữ liệu, Authentication Header (AH) hoặc Encapsulating Security Payload (ESP) được ứng dụng để mã hóa và xác thực dữ liệu. Cơ chế mã hóa bảo đảm tính bảo mật của dữ liệu và ngăn chặn dữ liệu bị chặn trong quá trình truyền.
  - Cơ chế xác thực bảo đảm tính toàn vẹn và độ tin cậy của dữ liệu và ngăn dữ liệu bị làm giả hoặc giả mạo trong quá trình truyền. IPsec sender sẽ sử dụng thuật toán mã hóa và khóa mã hóa để mã hóa một IP packet, tức là nó sẽ đóng gói dữ liệu gốc.
  - Tiếp đó, sender và receiver sử dụng cùng một thuật toán xác thực và khóa xác thực để xử lý những packet được mã hóa nhằm thu được giá trị kiểm tra tính toàn vẹn (integrity check value – ICV). Nếu như những ICV thu được ở cả hai đầu đều giống nhau, thì gói tin không bị làm giả trong quá trình truyền và receiver sẽ giải mã gói tin đó. Nếu như những ICV khác nhau, receiver sẽ loại bỏ gói tin.
- **Giai đoạn 4:** Kết thúc
  - Đây sẽ là bước cuối cùng và nó liên quan đến việc kết thúc kênh bảo mật IPSec. Việc chấm dứt xảy ra khi mà quá trình trao đổi dữ liệu hoàn tất hoặc phiên đã hết thời gian. Những khóa mật mã cũng sẽ bị loại bỏ.
<p align="center">
<img src="https://github.com/Giaduoc0211/5G-Security/assets/71538455/4f6aad80-6bf6-4db6-961c-1820cca4ba9c" alt="">
</p>




  
  




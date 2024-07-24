# Efficient and Secure Service-oriented Authentication Supporting Network Slicing for 5G-enabled IoT

## I. Mục tiêu 
- Bài báo này thảo luận về các thách thức và giải pháp liên quan đến bảo mật và xác thực trong mạng 5G, đặc biệt là đối với các dịch vụ Internet vạn vật (IoT). 

- Đề xuấ một framwork hộ trợ xác thực trong 5G cho IoT và Network slice:

    - Efficient and Secure Service-Oriented Authentication Framework: Một khung xác thực hiệu quả và an toàn, hỗ trợ network slicing và fog computing cho các dịch vụ IoT trong mạng 5G.
    - User Connections and Anonymous Access: Người dùng có thể thiết lập kết nối hiệu quả với mạng lõi 5G và truy cập ẩn danh các dịch vụ IoT thông qua các network slice phù hợp được các nút fog chọn dựa trên loại slice/dịch vụ của các dịch vụ truy cập.
- Cơ Chế Lựa Chọn Slice Bảo Mật:

    - Privacy-Preserving Slice Selection Mechanism: Cơ chế lựa chọn lát cắt bảo vệ quyền riêng tư, giữ kín cả loại slice cấu hình và loại dịch vụ truy cập của người dùng.
- Thoả thuận khoá Key session:
    - Session Keys Negotiation: Khóa phiên được thoả thuận giữa người dùng, các nút fog và các máy chủ IoT để đảm bảo truy cập an toàn dữ liệu dịch vụ trong bộ nhớ đệm fog và máy chủ từ xa với độ trễ thấp.
- Đánh Giá Hiệu Suất:
    - Performance Evaluation: Đánh giá hiệu xuất, tính hiệu quả và khả thi của nó trong hạ tầng 5G.


## II. Problem statement
### 1. Kiến trúc
![alt text](image-5.png)

- Ở trên hình trên thì chúng ta có thể thấy hệ thống kết hợp core 5G và network slicing, fog computing.


- Mạng 5G hướng tới xử lý lượng lớn dữ liệu, kết nối nhiều thiết bị, giảm độ trễ dịch vụ và mang lại mức độ tin cậy mới để cung cấp các dịch vụ tùy chỉnh dựa trên các yêu cầu chất lượng dịch vụ cụ thể. Bằng cách tích hợp các công nghệ mạng mềm hóa, bao gồm network slicing, SDN và fog computing, 5G dự kiến cung cấp ba loại dịch vụ: giao tiếp loại máy quy mô lớn (mMTC, hay còn gọi là IoT quy mô lớn), băng thông rộng di động nâng cao (eMBB) và giao tiếp độ tin cậy cao và độ trễ thấp (UR-LLC).

- Theo tiêu chuẩn 3GPP TS 23.501, kiến trúc 5G bao gồm bốn lớp: thiết bị người dùng, mạng truy cập, mạng lõi và dịch vụ IoT. Các thiết bị người dùng kết nối với mạng dữ liệu thông qua mạng lõi và mạng truy cập và giao tiếp với các máy chủ IoT.

- Core network tách chức năng mặt phẳng người dùng (UPF) khỏi chức năng mặt phẳng điều khiển (CPF) để cho phép mở rộng độc lập và triển khai linh hoạt.
    - UPF bao gồm chuyển tiếp dữ liệu, báo cáo sử dụng lưu lượng, đánh dấu gói ở tầng vận chuyển trong đường lên và đường xuống,... 
    - CPF kiểm soát xử lý gói trong UPF bằng cách cung cấp một tập hợp các quy tắc trong các phiên, tức là các quy tắc hành động chuyển tiếp để xử lý gói, các quy tắc phát hiện gói để kiểm tra gói.

    - CPF bao gồm nhiều chức năng, bao gồm Chức năng Quản lý Truy cập và Di động (AMF), Chức năng Quản lý Phiên (SMF), Chức năng Kiểm soát Chính sách (PCF), Chức năng Lựa chọn Mạng Slices (NSSF), Quản lý Dữ liệu (UDM), Chức năng Máy chủ Xác thực (AUSF), v.v., mỗi chức năng có các nhiệm vụ riêng. Cụ thể:

        - AMF: Quản lý đăng ký người dùng, kết nối, khả năng truy cập và di động, xác thực và ủy quyền truy cập.
        - SMF: Bao gồm các chức năng quản lý phiên và chuyển vùng.
        - PCF: Hỗ trợ khung chính sách thống nhất để quản lý hành vi mạng.
        - UDM: Chịu trách nhiệm tạo thông tin xác thực xác thực và quản lý đăng ký.
        - AUSF: Hỗ trợ chức năng máy chủ xác thực.
        - NSSF: Chọn tập hợp các phiên bản mạng slices phục vụ người dùng và xác định Thông tin hỗ trợ mạng Slices (NSSAI) tương ứng với các phiên bản mạng slices áp dụng.

- Network Slicing trong Mạng 5G: 
    - Để hỗ trợ các dịch vụ IoT khác nhau trong mạng 5G, network slicing đạt được sự tách biệt và ưu tiên các tài nguyên trên một cơ sở hạ tầng chung, bao gồm khả năng mạng, tài nguyên tính toán, các chức năng mạng ảo và các thiết lập công nghệ truy cập vô tuyến.

    - Mạng 5G trong Hình 1 được chia nhỏ ảo để hỗ trợ các loại dịch vụ IoT khác nhau. Ví dụ, slice 1 được thiết lập cho các giao tiếp loại máy bằng cách thiết lập các chức năng phân phối đầy đủ trên mạng, được tách biệt với các slices dành cho dịch vụ di động và giao tiếp phương tiện. Các điện thoại di động cần một slice end-to-end với băng thông lớn để cho phép các dịch vụ có tốc độ dữ liệu cao và độ trễ thấp, chẳng hạn như phát video và thực tế tăng cường.

    - Các network slices này được quản lý bởi các local control tại biên của mạng truy cập và mặt phẳng điều khiển trong mạng lõi, các bộ điều khiển này chọn các network slices cho các gói sắp tới dựa trên loại slice/dịch vụ và các thông tin phụ trợ khác, và chuyển tiếp các gói tới các máy chủ IoT.

-  Access network: Được nâng cấp để hỗ trợ các dịch vụ IoT có yêu cầu độ trễ thấp hoặc cần biết vị trí chính xác. Điều này được thực hiện bằng cách đưa các tài nguyên tính toán và lưu trữ đến gần rìa của mạng truy cập, tức là gần với các thiết bị đầu cuối hơn.
    - Fog Nodes và C-RAN:
        - Fog Nodes (nút fog) được triển khai trên Cloud-Radio Access Network (C-RAN) để cung cấp giao tiếp baseband tốc độ cao.
        - C-RAN là một kiến trúc mạng ảo hóa trong đó các trạm phát sóng được chia thành các thành phần như BBU (Baseband Unit) và RRH (Remote Radio Head).
            - BBU:Cung cấp lưu trữ tập trung và giao tiếp cho các dịch vụ cục bộ trong Access network. Làm việc để xử lý các tín hiệu cơ sở và quản lý kết nối mạng cho nhiều RRH.
            - RRH: Được trang bị các đơn vị xử lý, tài nguyên lưu trữ, và khả năng tính toán cho các ứng dụng di động yêu cầu nhận diện vị trí và lưu trữ dữ liệu cục bộ. Xử lý tín hiệu radio gần người dùng, giúp giảm độ trễ và cải thiện hiệu suất mạng.
    -Các tài nguyên trong các fog nodes được ảo hóa thành máy ảo (VMs), mỗi VM được kiểm soát bởi một local controller.local controller cung cấp các chức năng như:
        - Xác thực (authentication)
        - Cấp quyền (authorization)
        - Kế toán (accounting)
        - Phân bổ tài nguyên (resource allocation)
        - Quản lý di động (mobility management)
 ### 2. Các mối đe doạ 

- Các Loại Tấn Công:

    - Tấn công nghe lén (eavesdropping attacks): Kẻ tấn công có thể nghe lén và bắt giữ các gói dữ liệu đang được truyền.
    - Tấn công trung gian (man-in-the-middle attacks): Kẻ tấn công có thể chiếm đoạt các khóa phiên (session keys).
    - Tấn công theo dõi (stalking attacks): Kẻ tấn công có thể theo dõi vị trí của người dùng.
- Các tấn công từ bên ngoài này xâm nhập vào bảo mật dịch vụ IoT và quyền riêng tư của người dùng, tạo thành các mối đe dọa chính đối với từng thực thể trong kiến trúc dịch vụ IoT.

### 3. Mục tiêu thiết kế
- Đề xuất khung bảo mật ES3A sẽ có các chức năng sau:

    - Chọn Lựa Slice Bảo Vệ Quyền Riêng Tư: 
        - Để ngăn chặn rò rỉ quyền riêng tư của người dùng, các loại dịch vụ truy cập sẽ được bảo vệ chống lại các fog nodes không đáng tin hoặc các kẻ tấn công bên ngoài.
        - Việc ánh xạ các NSSAIs được phép và các loại slice đã cấu hình, tức là một phần của NSSAIs được phép áp dụng cho các dịch vụ đã đăng ký, cần được các fog nodes học để chọn các slices phù hợp cho việc chuyển tiếp gói.
    - Xác Thực Ẩn Danh Hướng Dịch Vụ:

        - Người dùng sử dụng các thông tin đăng nhập truy cập, được tạo bởi AUSF và một máy chủ IoT, để xác thực bản thân cho việc truy cập dịch vụ IoT.Không có thông tin đăng nhập truy cập hợp lệ, kẻ tấn công sẽ không thể vượt qua được quá trình xác thực của bộ điều khiển hoặc máy chủ IoT.
        - Trong quá trình xác thực dịch vụ, cả local control lẫn máy chủ IoT không thể biết được danh tính của người dùng, có nghĩa là họ không thể phân biệt được nguồn gốc của một thông điệp xác thực từ hai người dùng khác nhau.

    - Thoả Thuận Khoá Hướng Dịch Vụ:

        - Để bảo vệ dữ liệu dịch vụ, một khoá phiên duy nhất được thỏa thuận giữa máy chủ IoT, bộ điều khiển và người dùng.
        - Không có kẻ tấn công nào có thể biết được khoá phiên đã được thoả thuận hoặc phá hoại quá trình thoả thuận này.
        - Khoá phiên này được sử dụng để mã hóa dữ liệu dịch vụ cho người dùng truy cập vào dịch vụ cụ thể được cung cấp bởi máy chủ IoT.
 
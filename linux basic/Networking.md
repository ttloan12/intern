# Networking

### Về ip address

#### Wmnet Infomation có 3 option

- **Bridged**: kết nối lớp mạng VMware ảo với mạng bên ngoài đây là option nếu bạn nào muốn cho đi internet bên ngoài
- **NAT** ( Vitrual Network Translate ). Chia sẽ địa chỉ từ host IP với VMware, nghĩa là nó cũng tương tự card Bridged, nhưng nó đã được dịch chuyển lớp mạng ảo thật thành lớp mạng khác.
- **Host-only**: kết nối Mạng nội bộ trong một mạng riêng, nghĩa là tất cả các card mạng trong VMware được kết nối lại với nhau.

#### Muốn thay đổi NAT thì cần chỉnh sửa trong phần Vitual network editor

-  tắt  tùy chọn Use local DHCP service to distribute IP address to VMs để không cấp IP tự động nữa (hiển nhiên khi đó phải thực hiện Manual Settings). Giờ bạn có thể kiểm tra chi tiết ở DHCP Settings

- DHCP sẽ cung cấp IP tự động trong dải IP **192.168.224.128 – 192.168.224.254**, IP sẽ được gán tự động một trong số 127 IP được cấp này.
- kiểm tra IP tại NAT setting
- ping gg

### Về OSI and TCP/IP

| OSI                                                          | TCP/IP      |
| ------------------------------------------------------------ | ----------- |
| Application                                                  |             |
| presentation :dữ liệu sẽ được đóng gói và mã hoá (Data Encapsulation and Encryption) thành một định dạng chuẩn chung bất kể dữ liệu đầu vào là gì (HTML, Javascript files, image files…) | application |
| session : một kết nối được khởi tạo giữa máy client (máy tính sử dụng trình duyệt để click vào URL) và web server (nơi ứng dụng web được đặt), ngay sau khi mà web server gửi trả lại nội dung web page cho phía client thì kết nối này sẽ được ngắt (terminated), mỗi kết nối như trên được định nghĩa là một phiên (a session) |             |
| transport :lớp này quyết định việc chuyển giao dữ liệu đến đúng process của ứng dụng đang chạy, cũng như điều phối việc một số lượng dữ liệu bao nhiêu sẽ được gửi, ở tốc độ gửi là bao nhiêu. Hai giao thức rất quan trọng trong Transport layer là TCP và UDP | transport   |
| networking :lớp này chịu trách nhiệm giải mã dữ liệu thành các khung dữ liệu chứa các BITS, bao gồm 2 lớp con là MAC và LLC. | internet    |
| data-link : lớp này chịu trách nhiệm giải mã dữ liệu thành các khung dữ liệu chứa các BITS, bao gồm 2 lớp con là MAC và LLC. MAC kiểm soát việc các phần cứng máy tính truy cập dữ liệu và cấp quyền để chuyển giao dữ liệu . Địa chỉ MAC là địa chỉ vật lý và duy nhất đối với 1 thiết bị card mạng.... LLC là interface nằm giữa mac và Network Layer |             |
| physical   bao gồm đường truyền internet (cable, hoặc sóng vô tuyến, sóng không dây), là môi trường để dữ liệu được truyền qua. | networking  |

### Về các lệnh 

1. ipconfig

   ifconfig cung cấp địa chỉ ip, địa chỉ mac, MTU (Maxium Transmission Unit - là kích thước gói dữ liệu lớn nhất, được đo bằng byte, có thể truyền tải qua một mạng lưới). Lệnh này thường được sử dụng để đặt hoặc hiển thị địa chỉ IP và netmask của giao diện mạng. Nó cũng cung cấp các lệnh để bật hoặc tắt một giao diện mạng. Một số cú pháp lệnh `ifconfig`:

   - `ifconfig -a` - Liệt kê tất cả các inteface hiện đang có, kể cả các interface không sử dụng.
   - `ifconfig <interface>` - Thông tin chi tiết của một interface cụ thể.
   - `ifconfig <interface> <address> netmask <address>` - Gán địa chỉ IP và Gateway cho một giao diện. Tuy nhiên, các cấu hình này sẽ được thiết lập lại sau khi hệ thống khởi động lại.
   - `ifup <interface>` hay `ifdown <interface>` - Để bật hay tắt một interface.

   2. ip

      Phiên bản cập nhập của ip config. Gần như trên các hệ thống CentOS systemd mới thì một vài chương trình cũ sẽ bị xoá bỏ mặc định khi cài đặt như ‘route‘, ‘ifconfig‘ hay ‘netstat‘. Bạn nên học cách sử dụng công cụ lệnh ‘ip’ này vì tính tiện dụng của nó.

   Một số cú pháp lệnh `ifconfig`:

   - `ip a` - Lệnh này cung cấp thông tin chi tiết của tất cả các mạng như ifconfig.
   - `ip link` - Cấu hình, thêm và xóa các interface. Sử dụng `ip link show` để hiển thị tất cả các interface trên hệ thống.
   - `ip address` - Hiển thị địa chỉ ip, gắn địa chỉ ip mới hoặc xóa địa chỉ ip chỉ cũ.
   - `ip route` - Được sử dụng để Cấu hình quản lý bảng định tuyến.

   3. hostname

       để xem hoặc thay đổi tên hostname hoặc system’s domain. Nó cũng có thể được dùng kiểm tra địa chỉ IP của máy tính.

      Một số cú pháp lệnh `hostname`:

      - `hostname` - Hiển thị hostname
      - `hostname --all-ip-addresses` - Hiển thị tất cả các địa chỉ IP
      - `sudo hostname <new hostname>` - Thay đổi hostname. Tuy nhiên thay đổi bằng hostname chỉ tạm thời. Sau khi reboot, hostname sẽ bị đưa trở về như cũ.

   4. ping 

      Kết quả ping giữa 2 nút mạng sẽ cho ta những thông tin hữu ích như:

      - Tình trạng của nút đích: nó có kết nối được tới được không
      - Thời gian một vòng di chuyển giữa 2 nút: Host–Computer-Host
      - Phần trăm lượng packet bị mất trong quá trình truyền

      Một số cú pháp lệnh `ping`:

      - `ping <destination>` - Lệnh ping gửi gói tin echo ICMP để kiểm tra kết nối mạng, destination có thể là tên miền hoặc địa chỉ ip trực tiếp
      - `ping -c <number> <destination>` - Bạn có thể giới hạn số lượng gói tin bằng cách thêm " -c " vào lệnh ping.

      

   5. telnet

      `telnet` là lệnh sẽ thực hiện kết nối máy chủ và máy đích thông qua một port bằng cách sử dụng giao thức telnet TCP/IP. Nếu kết nối được thiết lập có nghĩa là kết nối giữa hai máy đang hoạt động tốt.

      Cú pháp của lệnh `telnet`:

      ```none
      telnet <hostname/IP address> <port>  
      ```

      

      Trong trường hợp bạn không xác định một port cụ thể nào thì telnet sẽ sử dụng port mặc định là 23

   6. traceroute

      Nếu như sử dụng `ping` hiển thị cho bạn thấy các gói tin bị mất mát trong kết nối thì `traceroute` cho thấy đường đi được sử dụng, trình tự các cổng mà các gói tin đi qua để có thể đến được đích. `traceroute` chính là một trong những lệnh hữu ích nhất trong khắc phục sự cố mạng qua những thông tin mà lệnh nàu cung cấp gồm:

      - Cung cấp tên và xác định mọi thiết bị trên đường dẫn.
      - Theo dõi lộ trình để đến đích của gói tin.
      - Xác định và chỉ ra vị trí các sự cố trong kết nối mạng, độ trễ trong kết nối mạng đến từ đâu.

      Cú pháp câu lệnh `traceroute`:

      ```none
      traceroute <option> <destination>
      ```

   7. nslookup

      `nslookup` là lệnh được sử dụng để thực hiện các tra cứu liên quan đến DNS. `nslookup` có thể cho chúng ta biết các thông tin quan trọng như MX records và địa chỉ IP liên kết với tên miền.

      Cú pháp lệnh `nslookup`:

      ```none
      nslookup <domainName>
      ```

   8. dig

      `dig` là viết tắt của Domain Information Groper, có nghĩa là công cụ tìm kiếm thông tin tên miền. Nó có tác dụng để kiểm tra và xử lí sự cố DNS Server, tìm kiếm DNS và hiển thị các nội dung được yêu cầu.

      Cú pháp lệnh `dig`:

      - `dig <domainName>` - Đây là lệnh truy vấn DNS cơ bản. Theo mặc định, nó sẽ xuất ra các bản ghi A
      - `dig <domainName> MX` - Truy vấn các bản ghi MX
      - `dig <domainName> NS` - Truy vấn các bản ghi NS
      - `dig <domainName> ANY` - Truy vấn tất cả các loại bản ghi

   9. netstat

      hiển thị các thông tin bảng định tuyến, thông tin kết nối, trạng thái của các cổng, các cài đặt và nhiều các thống kê mạng khác nhau,...

      Một số cú pháp lệnh `netstat`:

      - `netstat -i` - Liệt kê các interface
      - `netstat -r` - Hiển thị bảng định tuyến

   10. Lệnh curl

       Lệnh `curl` là 1 công cụ để truy cập trang web thông qua command, `curl` hỗ trợ những protocol khác nhau như `FILE`, `FTP`, `FTPS`, `Gopher`, `HTTP`, `HTTPS`, `IMAP`, `LDAP`, `POP3`, `RTSP`, `SMTP`, …

       Mặc định `curl` chưa có sẵn trong Linux, để cài đặt `curl` từ Ubuntu repository sử dụng lệnh sau:

       ```
       sudo apt-get install curl
       ```

       Và tiến hành cài đặt những thư viện liên quan:

       ```
       sudo apt-get install libc6 libcurl3 zlib1g
       ```

       Và có thể `curl` với những lệnh thường xuyên sử dụng dưới đây, ví dụ lấy về nội dung của trang web www.google.com.

       ```
       curl http://www.google.com
       ```

       
#### Cách đặt IP, khai báo DNS cho máy linux

**Để cài đặt IP và khai báo DNS cho máy Linux thì chia ra theo hd**h: 

1. **Ubuntu**

**\+ mở file cấu hình interfaces**

\-     `Sudo nano /etc/network/interface`

\-     Sửa file : 

`network:`

`auto ens33`

`iface ens33 inet static`

 `address 192.168.1.100`

 `netmask 255.255.255.0`

 `gateway 192.168.1.1`

 `dns-nameservers 8.8.8.8 8.8.4.4 # Khai báo DNS`

\-     Khởi động lại dịch vụ : `sudo systemctl restart networking`

**\+ mở file cấu hình mạng netplan**

\-     `sudo nano /etc/netplan/00-installer-config.yaml`

ethernets:

  `ens33: # Tên giao diện mạng (có thể thay đổi tùy vào hệ thống)`

   `dhcp4: no # Tắt DHCP để sử dụng IP tĩnh`

   `addresses: [192.168.1.100/24] # Đặt IP tĩnh`

   `gateway4: 192.168.1.1   # Đặt gateway`

   `nameservers:`

​    `addresses: [8.8.8.8, 8.8.4.4] # Khai báo DNS`

 `version: 2`

\-     áp dụng cấu hình : `sudo netplan apply`

2. **centOS** 

\+ mở file cấu hình mạng : `sudo nano /etc/sysconfig/network-scripts/ifcfg-ens33`

\+ cấu hình : 

`BOOTPROTO=static`

`IPADDR=192.168.1.100  # Địa chỉ IP tĩnh`

`NETMASK=255.255.255.0 # Netmask`

`GATEWAY=192.168.1.1  # Gateway`

`DNS1=8.8.8.8      # Khai báo DNS`

`DNS2=8.8.4.4`

\+ khởi động lại dịch vụ : `sudo systemctl restart network`

### regular expression 

  dùng để tìm kiếm, kiểm  tra và xử lý văn bản dựa trên các mẫu quy tắc. 

1. Grep   -       Tìm kiếm văn bản : **Ví dụ**: Tìm các dòng chứa từ  "error" trong file log.txt:  “ grep 'error' log.txt “  

2. ​      Sed  -       cho phép bạn thay thế, chèn, hoặc xóa văn bản : ” sed  's/foo/bar/g' file.txt” - : Thay thế tất cả các từ "foo"  bằng "bar" trong file file.txt:  

3. ​      Awk  -       lọc và thao tác dữ liệu: “awk '/info/ {print}' file.txt  “ - In ra các dòng chứa từ  "info" trong file file.txt:  

4. .      Find  -       tìm kiếm các tập tin theo tên trong hệ thống tệp “find  . -name '*.txt'” - Tìm tất cả các tập tin có phần mở rộng .txt trong thư mục  hiện tại:

     **Cú pháp Regex cơ bản**  ·      

   **.**: Ký tự bất kỳ (ngoại trừ ký tự xuống dòng).  ·     

    *****: 0 hoặc nhiều lần của ký tự trước đó.  ·   

     **+**: 1 hoặc nhiều lần của ký tự trước đó.  ·      

   **?**: 0 hoặc 1 lần của ký tự trước đó.  ·      

   **^**: Bắt đầu của dòng.  ·      

   **$**: Cuối của dòng.  ·     

    **[]**: Tập hợp ký tự (ví dụ: [abc] khớp với a, b hoặc c).  ·  

      **|**: Hoặc (ví dụ: cat|dog khớp với cat hoặc dog).  ·   

      **()**: Nhóm các mẫu.  

   **Tìm tất cả các số có 3 chữ số  trong một file**: grep '[0-9]\{3\}' file.txt  
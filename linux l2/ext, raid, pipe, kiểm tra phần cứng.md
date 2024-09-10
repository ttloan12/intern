### Ext2, ext3, ext4 là gì? cách format ổ cứng, Mount, unmount, fstab?. Kiểm tra dung lượng HDD, file, thư mục

**Ext2**

·     **Khái niệm**: Là hệ thống tập tin cũ hơn và không hỗ trợ tính năng ghi lại (journaling).

·     **Tính năng**:

o  Không có tính năng journaling, nên phục hồi sau sự cố không nhanh như Ext3 hoặc Ext4.

o  Phù hợp cho các ứng dụng nơi tính năng journaling không cần thiết.

·     **Sử dụng**: Thường được dùng trong các hệ thống cũ hoặc thiết bị lưu trữ nhúng.

**Ext3**

·     **Khái niệm**: Là phiên bản mở rộng của Ext2 với tính năng journaling.

·     **Tính năng**:

o  Hỗ trợ journaling, giúp cải thiện tính toàn vẹn dữ liệu và phục hồi sau sự cố.

o  Cải thiện hiệu suất và độ tin cậy so với Ext2.

·     **Sử dụng**: Được sử dụng rộng rãi trong các hệ thống Linux trước khi Ext4 ra đời.

**Ext4**

·     **Khái niệm**: Là phiên bản cải tiến của Ext3 với nhiều tính năng mới và tối ưu hóa.

·     **Tính năng**:

o  Hỗ trợ journaling như Ext3 nhưng với cải tiến về hiệu suất và độ tin cậy.

o  Hỗ trợ các tính năng mới như phân vùng lớn hơn, tệp lớn hơn, và khôi phục nhanh hơn.

o  Cải thiện hiệu suất với các hệ thống tập tin lớn và số lượng lớn các tệp.

·     **Sử dụng**: Là hệ thống tập tin phổ biến nhất cho các hệ thống Linux hiện đại.

**Format ổ cứng** 

\-     **Với ext2: sudo mkfs.ext2 /dev/sdXn**

\-     **Với ext3: sudo mkfs.ext3 /dev/sdXn**

\-     **Với ext4: sudo mkfs.ext4 /dev/sdXn**

Trong đó /dev/sdXn là phân vùng mà bạn muốn format (ví dụ: /dev/sda1).

**Mount và Unmount**

·     **Mount**: Kết nối một phân vùng hoặc thiết bị vào hệ thống tập tin để có thể truy cập dữ liệu của nó.

o  **Lệnh để mount**:

“sudo mount /dev/sdXn /mnt/point”

Trong đó /dev/sdXn là phân vùng và /mnt/point là điểm mount (thư mục mà bạn muốn gắn phân vùng vào).

o  **Tạo điểm mount** (nếu chưa có):

“sudo mkdir /mnt/point”

·     **Unmount**: Ngắt kết nối phân vùng hoặc thiết bị khỏi hệ thống tập tin.

o  **Lệnh để unmount**:

“sudo umount /mnt/point”

**/etc/fstab** là tập tin cấu hình trong Linux chứa thông tin về các phân vùng và điểm mount tự động khi hệ thống khởi động.

·     **Cấu trúc cơ bản của /etc/fstab**:

“<thiết bị> <điểm mount> <hệ thống tập tin> <tùy chọn> <dump> <pass>”

Ví dụ:

“/dev/sda1 /mnt/point ext4 defaults 0 2”

o  /dev/sda1: Thiết bị hoặc phân vùng.

o  /mnt/point: Điểm mount.

o  ext4: Hệ thống tập tin.

o  defaults: Các tùy chọn mount (như read-write).

o  0: Giá trị dump (dùng để sao lưu, thường là 0).

o  2: Giá trị pass (thứ tự kiểm tra hệ thống tập tin).

**Kiểm tra dung lượng**

·     **Kiểm tra dung lượng ổ cứng**:

o  **Sử dụng lệnh df**:

“df -h”

-h hiển thị kết quả với định dạng dễ đọc (ví dụ: GB, MB).

·     **Kiểm tra dung lượng tệp và thư mục**:

o  **Sử dụng lệnh du**:

“du -sh /path/to/file_or_directory”

-s chỉ hiển thị tổng dung lượng, và -h định dạng dễ đọc. 

Ví dụ “du -sh /home/user”

### Tìm hiểu về khái niệm RAID và các loại phổ biến

RAID (Redundant Array of Independent Disks) là một công nghệ kết hợp nhiều ổ cứng vật lý thành một hệ thống lưu trữ duy nhất nhằm tăng cường hiệu suất, khả năng chịu lỗi, hoặc cả hai. Các ổ cứng trong một hệ thống RAID có thể hoạt động như một đơn vị để cải thiện hiệu suất, hoặc dữ liệu có thể được phân chia, sao lưu để đảm bảo tính sẵn sàng cao.

**Các loại RAID phổ biến:**

1. **RAID 0 (Striping)**:

o  **Cách hoạt động**: Dữ liệu được chia thành các phần nhỏ và ghi song song trên nhiều ổ cứng.

o  **Ưu điểm**: Tăng tốc độ truy xuất dữ liệu do có thể đọc/ghi đồng thời trên nhiều ổ.

o  **Nhược điểm**: Không có dự phòng dữ liệu; nếu một ổ hỏng, toàn bộ dữ liệu có thể mất.

o  **Ứng dụng**: Phù hợp cho các ứng dụng cần hiệu suất cao nhưng không cần yêu cầu về an toàn dữ liệu như chỉnh sửa video.

2. **RAID 1 (Mirroring)**:

o  **Cách hoạt động**: Dữ liệu được sao chép lên tất cả các ổ cứng trong hệ thống RAID.

o  **Ưu điểm**: Tăng độ tin cậy vì có bản sao dữ liệu trên mỗi ổ cứng; nếu một ổ hỏng, dữ liệu vẫn còn.

o  **Nhược điểm**: Dung lượng bị giới hạn bởi ổ nhỏ nhất, và tốc độ ghi có thể bị giảm.

o  **Ứng dụng**: Thích hợp cho các ứng dụng yêu cầu tính toàn vẹn và an toàn dữ liệu cao, như lưu trữ cơ sở dữ liệu.

3. **RAID 5 (Striping with Parity)**:

o  **Cách hoạt động**: Dữ liệu và thông tin kiểm tra lỗi (parity) được phân chia và ghi lên nhiều ổ cứng. Parity giúp khôi phục dữ liệu nếu một ổ cứng bị hỏng.

o  **Ưu điểm**: Cân bằng giữa hiệu suất, dung lượng và khả năng chịu lỗi. Có thể tiếp tục hoạt động ngay cả khi một ổ hỏng.

o  **Nhược điểm**: Cần ít nhất 3 ổ cứng và tốc độ ghi không cao như RAID 0 hoặc RAID 1 do phải tính toán parity.

o  **Ứng dụng**: Thường được sử dụng trong các hệ thống lưu trữ doanh nghiệp.

4. **RAID 6 (Striping with Double Parity)**:

o  **Cách hoạt động**: Tương tự RAID 5 nhưng sử dụng 2 khối parity, cho phép chịu được 2 ổ cứng bị hỏng cùng lúc.

o  **Ưu điểm**: Độ tin cậy cao hơn RAID 5 vì có khả năng chịu lỗi cao hơn.

o  **Nhược điểm**: Cần ít nhất 4 ổ cứng và hiệu suất ghi có thể bị giảm.

o  **Ứng dụng**: Thích hợp cho các môi trường yêu cầu tính an toàn dữ liệu cao, nhưng không muốn hy sinh dung lượng lưu trữ nhiều.

5. **RAID 10 (RAID 1 + RAID 0)**:

o  **Cách hoạt động**: Kết hợp giữa RAID 1 (mirroring) và RAID 0 (striping). Dữ liệu được phân chia và sao chép trên các cặp ổ.

o  **Ưu điểm**: Cung cấp cả hiệu suất và khả năng chịu lỗi.

o  **Nhược điểm**: Chi phí cao vì cần ít nhất 4 ổ cứng và dung lượng khả dụng chỉ bằng một nửa tổng dung lượng.

**Ứng dụng**: Sử dụng trong các hệ thống yêu cầu cả hiệu suất và độ an toàn dữ liệu cao

### Kiểm tra phiên bản HĐH, cách update HĐH

Kiểm tra: 

1. Ubuntu

“ lsb_release -a” or “ cat /etc/os-release” or “ uname -r”

2. CentOS

“ cat /etc/redhat-release”

Cách update:

1. Ubuntu

“ sudo apt update” -> “sudo apt upgrade” -> nếu muốn nâng cấp toàn bộ bao gồm các gói đã được thay đổi cấu trúc thì dùng “ sudo apt full-upgarde”

2. centOS

“ sudo yum check-update” -> “ sudo yum update”

### Biến môi trường

**Biến môi trường** (environment variable) là một cặp giá trị (key-value) lưu trữ thông tin cấu hình của hệ điều hành hoặc ứng dụng. Các biến môi trường được sử dụng để lưu trữ các thông tin như đường dẫn hệ thống, cấu hình ứng dụng, thông tin người dùng và nhiều giá trị khác để quá trình hoạt động của hệ thống hoặc chương trình trở nên linh hoạt và tùy chỉnh hơn.

**Một số biến môi trường phổ biến:**

·     **PATH**: Đường dẫn chứa các thư mục nơi hệ điều hành tìm kiếm các tệp thực thi.

·     **HOME**: Thư mục chính của người dùng hiện tại (trên Linux/Unix).

·     **USER**: Tên người dùng hiện tại.

·     **SHELL**: Trình vỏ dòng lệnh được sử dụng (Linux/Unix).

·     **TEMP**: Đường dẫn đến thư mục lưu trữ tạm thời.

·     **LANG**: Thiết lập ngôn ngữ mặc định.

Xem danh sách biến môi trường : env

Xem giá trị của 1 biến môi trường cụ thể: echo $ten-bien

Thiết lập biến môi trường tạm thời trong phiên hiện tại : 

export ten_bien= “gia_tri”

Thiết lập biến môi trường vĩnh viễn: export ten_bien= “gia_tri” sau đó nạp cấu hình shell “ source ~/.bashr

### Tìm hiểu về Pipes (vd: command1 | command 2)

là một cách chuyển output (kết quả đầu ra) của một lệnh này thành input (đầu vào) của một lệnh khác. Điều này giúp kết hợp các lệnh lại với nhau để thực hiện các tác vụ phức tạp mà không cần lưu trữ tạm thời dữ liệu trên đĩa.

\+ “ls | wc -l” (Lấy danh sách các file, sau đó đếm số lượng file trong thư mục)

\+ “cat file.txt | grep "chuoi_tim_kiem" | sort | uniq -c”

 (- cat file.txt: In nội dung file.

\- grep "chuoi_tim_kiem": Lọc các dòng chứa chuỗi cụ thể.

\- sort: Sắp xếp các dòng.

\- uniq -c: Loại bỏ các dòng trùng lặp và đếm số lần xuất hiện.)

### Cách kiểm tra phàn cứng của Server: Main, RAM, HDD, CPU

Mainboard: sudo dmidecode -t baseboard

RAM: free -h, dmidecode -t memory

HDD: lsblk, df -h, fdisk -l

CPU: lscpu, cat /proc/cpuinfo
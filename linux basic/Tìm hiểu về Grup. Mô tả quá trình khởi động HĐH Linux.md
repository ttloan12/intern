#### Tìm hiểu về Grup. Mô tả quá trình khởi động HĐH Linux

1. GRUB (Grand Unified Bootloader) Nó chịu trách nhiệm nạp kernel của hệ điều hành  vào bộ nhớ sau khi máy tính khởi động. Một số tính năng chính của GRUB bao gồm:  Khả năng chọn hệ điều hành: Nếu có nhiều hệ điều hành trên máy tính, GRUB  cho phép người dùng chọn hệ điều hành muốn khởi động.  Hỗ trợ nhiều định dạng tập tin: GRUB có thể đọc được các hệ thống tập tin  phổ biến như ext4, FAT, và NTFS, giúp nó truy cập và nạp kernel từ nhiều loại  hệ thống tập tin khác nhau.  Cấu hình linh hoạt: GRUB cho phép người dùng thay đổi các tùy chọn khởi động  như tham số kernel, chế độ cứu hộ, và nhiều tùy chọn khác.  
2.  Khởi động -> BIOS hoạt động -> POST kiểm tra phần cứng và tìm  thiết bị khởi động-> BIOS chuyển quyền điều khiển cho boot loader, nó thực  hiện tìm kiếm và nạp kernel của hệ điều hành-> kernel được nạp vào bộ nhớ  thực hiện điều khiển phần cứng, lập bộ nhớ ảo, điều khiển các thiết bị, tìm  và nạp tiến trình init -> init quản lý và khởi động các dịch vụ cần thiết  như mạng, các tập tin, dịch vụ đăng nhập  

#### Kernel space, User space

Kerne spacel là vùng bộ nhớ chứa hoạt động của kernel. Kernel có toàn quyền kiểm soát phần cứng và tài nguyên hệ thống, mọi quá trình quản lý bộ nhớ, thiết bị, tài nguyên đều xảy ra trong kernel space. Chỉ các tiến trình đặc quyền mới có thể truy cập được vào kernel space.

User space là vùng bộ nhớ nơi các ứng dụng và chương trình của người dùng hoạt động. các tiến trình trong user space không có quyền truy cập trực tiếp vào phần cứng hoặc tài nguyên hệ thống mà phải gửi yêu cầu tới kernel qua các system calls.
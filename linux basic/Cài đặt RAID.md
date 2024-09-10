RAID là viết tắt của Redundant Array of Independent Disks, được sử dụng ban đầu như một giải pháp bảo vệ dữ liệu bằng cách cho phép ghi dữ liệu lên nhiều đĩa cứng cùng lúc. Sau đó, RAID đã phát triển nhiều biến thể khác nhau để đảm bảo an toàn và tăng tốc độ truy xuất dữ liệu từ đĩa cứng. Dưới đây là năm loại RAID phổ biến mà chúng ta có thể tìm hiểu.

Để hiểu về RAID nhanh chóng, chúng ta có thể tham khảo các thông tin dưới đây:

- RAID nên sử dụng các ổ cứng có dung lượng bằng nhau.

- Việc sử dụng RAID sẽ tốn nhiều ổ cứng hơn so với không sử dụng, nhưng đổi lại dữ liệu sẽ được bảo vệ tốt hơn.

- RAID có thể hoạt động trên nhiều hệ điều hành như Windows 98, Windows 2000, Windows XP, Windows 10, Windows Server 2016, MAC OS X, Linux,...

- RAID 0 sẽ có dung lượng bằng tổng dung lượng của các ổ cứng.

- RAID 1 sẽ duy trì dung lượng của một ổ cứng.

- RAID 5 sẽ có dung lượng nhỏ hơn một ổ cứng (ví dụ: sử dụng 5 ổ cứng RAID 5 sẽ có dung lượng tương đương với 4 ổ cứng).

- RAID 6 sẽ có dung lượng nhỏ hơn hai ổ cứng (ví dụ: sử dụng 5 ổ cứng RAID 6 sẽ có dung lượng tương đương với 3 ổ cứng).

- RAID 10 chỉ có thể được tạo ra khi sử dụng số lượng ổ cứng chẵn và tối thiểu là bốn ổ cứng. Dung lượng sử dụng của RAID 10 bằng một nửa tổng dung lượng của các ổ cứng sử dụng (ví dụ: sử dụng 10 ổ cứng RAID 10 sẽ có dung lượng tương đương với 5 ổ cứng).

Các loại RAID: 

1. RAID0(striping): Yêu cầu tối thiểu hai ổ cứng,

**Cách hoạt động**: Dữ liệu được chia thành các phần nhỏ và ghi song song trên nhiều ổ cứng.

o  **Ưu điểm**: Tăng tốc độ truy xuất dữ liệu do có thể đọc/ghi đồng thời trên nhiều ổ.

o  **Nhược điểm**: Không có dự phòng dữ liệu; nếu một ổ hỏng, toàn bộ dữ liệu có thể mất.

o  **Ứng dụng**: Phù hợp cho các ứng dụng cần hiệu suất cao nhưng không cần yêu cầu về an toàn dữ liệu như chỉnh sửa video.

2. RAID1(mirroring): 

o  **Cách hoạt động**: Dữ liệu được sao chép lên tất cả các ổ cứng trong hệ thống RAID.

o  **Ưu điểm**: Tăng độ tin cậy vì có bản sao dữ liệu trên mỗi ổ cứng; nếu một ổ hỏng, dữ liệu vẫn còn.

o  **Nhược điểm**: Dung lượng bị giới hạn bởi ổ nhỏ nhất, và tốc độ ghi có thể bị giảm.

o  **Ứng dụng**: Thích hợp cho các ứng dụng yêu cầu tính toàn vẹn và an toàn dữ liệu cao, như lưu trữ cơ sở dữ liệu.

3.	RAID 5 (Striping with Parity):
o	**Cách hoạt động**: Dữ liệu và thông tin kiểm tra lỗi (parity) được phân chia và ghi lên nhiều ổ cứng. Parity giúp khôi phục dữ liệu nếu một ổ cứng bị hỏng.
o	**Ưu điểm**: Cân bằng giữa hiệu suất, dung lượng và khả năng chịu lỗi. Có thể tiếp tục hoạt động ngay cả khi một ổ hỏng.
o	**Nhược điểm**: Cần ít nhất 3 ổ cứng và tốc độ ghi không cao như RAID 0 hoặc RAID 1 do phải tính toán parity.
o	**Ứng dụng**: Thường được sử dụng trong các hệ thống lưu trữ doanh nghiệp.
4.	RAID 6 (Striping with Double Parity):
o	**Cách hoạt động**: Tương tự RAID 5 nhưng sử dụng 2 khối parity, cho phép chịu được 2 ổ cứng bị hỏng cùng lúc.
o	**Ưu điểm**: Độ tin cậy cao hơn RAID 5 vì có khả năng chịu lỗi cao hơn.
o	N**hược điểm**: Cần ít nhất 4 ổ cứng và hiệu suất ghi có thể bị giảm.
o	**Ứng dụng**: Thích hợp cho các môi trường yêu cầu tính an toàn dữ liệu cao, nhưng không muốn hy sinh dung lượng lưu trữ nhiều.
5.	RAID 10 (RAID 1 + RAID 0):
o	**Cách hoạt động**: Kết hợp giữa RAID 1 (mirroring) và RAID 0 (striping). Dữ liệu được phân chia và sao chép trên các cặp ổ.
o	**Ưu điểm**: Cung cấp cả hiệu suất và khả năng chịu lỗi.
o	**Nhược điểm**: Chi phí cao vì cần ít nhất 4 ổ cứng và dung lượng khả dụng chỉ bằng một nửa tổng dung lượng.
o	**Ứng dụng**: Sử dụng trong các hệ thống yêu cầu cả hiệu suất và độ an toàn dữ liệu cao.

#### Các Điều Kiện Để Chạy RAID

Để có thể sử dụng **RAID**, cần phải có ít nhất một card điều khiển và hai ổ đĩa cứng có dung lượng giống nhau. Các ổ đĩa có thể sử dụng bất kỳ chuẩn nào như ATA, Serial ATA hoặc SCSI, tuy nhiên tốt nhất là chúng nên hoàn toàn giống nhau để đảm bảo hiệu năng tối ưu khi hoạt động ở chế độ đồng bộ như RAID.

### Cài đặt RAID

Việc cài đặt RAID đơn giản và chủ yếu dựa vào BIOS của mainboard và RAID Controller. Sau khi cắm ổ cứng vào vị trí RAID trên bo mạch bạn chỉ cần vào BIOS của BMC để kích hoạt bộ điều khiển RAID và chỉ định các cổng liên quan (thường trong mục Integrated Peripherals).

Sau khi lưu thông số và khởi động lại máy tính, bạn cần chú ý màn hình thông báo và nhấn đúng tổ hợp phím khi máy tính yêu cầu (ví dụ như Ctrl+F hoặc F4) để vào BIOS RAID.

**Dù mỗi loại RAID có một giao diện khác nhau, nhưng thao tác cơ bản sau đây luôn cần thiết:**

\- Chỉ định ổ cứng tham gia RAID.

\- Lựa chọn kiểu RAID (0/1/0+1/5).
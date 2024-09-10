### Tìm hiểu về Permission của file, directory. SUID, SGID, sticky bit

**Lỗi “ permission denied” là lỗi về phân quyền** 

**Quyền truy cập (Permissions)**

**1. Quyền cơ bản:**

·     **r**: Quyền đọc (read) – cho phép xem nội dung tập tin hoặc liệt kê nội dung thư mục.

·     **w**: Quyền ghi (write) – cho phép thay đổi nội dung tập tin hoặc thêm/xóa tập tin trong thư mục.

·     **x**: Quyền thực thi (execute) – cho phép thực thi tập tin hoặc vào thư mục.

**2. Phân quyền:**

Quyền truy cập được chia thành ba nhóm:

·     **User (u)**: Quyền của người sở hữu tập tin.

·     **Group (g)**: Quyền của nhóm người dùng sở hữu tập tin.

·     **Others (o)**: Quyền của các người dùng khác.

**Ví dụ về quyền truy cập:**

·     -rwxr-xr--:

o  -: Loại tập tin (tập tin thường).

o  rwx: Quyền của người sở hữu (read, write, execute).

o  r-x: Quyền của nhóm (read, execute).

o  r--: Quyền của người khác (read).

**3. Thay đổi quyền truy cập:**

·     **chmod**: Thay đổi quyền truy cập của tập tin hoặc thư mục.

vd: chmod [quyền] tên_tập_tin

**SUID( set user ID)** : khi thuộc tính này được đặt vào 1 tập tin thì tập tin đó sẽ chạy với quyền của người sở hữu tập tin thay vì quyền của người thực thi tập tin. 

  **Cách đặt thuộc tính SUID**:

“ chmod u+s tên_tập_tin”

 **Ví dụ**: Tập tin /usr/bin/passwd có thuộc tính SUID. Khi bạn chạy passwd, tập tin này chạy với quyền của người sở hữu (thường là root) để bạn có thể thay đổi mật khẩu của mình.

 **Xem thuộc tính SUID**: Thuộc tính SUID được hiển thị bằng ký tự s trong phần quyền của chủ sở hữu, thay vì x.

“ls -l /usr/bin/passwd”

Kết quả có thể là:

“-rwsr-xr-x 1 root root 54256 Sep 1 2023 /usr/bin/passwd”

**SGID (Set Group ID)**

Khi thuộc tính SGID được đặt trên một tập tin thực thi, tập tin đó chạy với quyền của nhóm sở hữu tập tin. Đối với thư mục, thuộc tính SGID làm cho các tập tin và thư mục con được tạo ra trong thư mục đó thuộc về nhóm của thư mục, thay vì nhóm của người tạo ra chúng.

·     **Cách đặt thuộc tính SGID**:

“chmod g+s tên_tập_tin”

·     **Ví dụ**: Nếu một thư mục có thuộc tính SGID, các tập tin mới được tạo trong thư mục sẽ có nhóm của thư mục thay vì nhóm của người tạo.

·     **Xem thuộc tính SGID**: Thuộc tính SGID được hiển thị bằng ký tự s trong phần quyền của nhóm, thay vì x.

“ls -l”

Kết quả có thể là:

“drwxrwsr-x 2 root staff 4096 Sep 1 2023 /shared”F

**Sticky Bit**

Khi thuộc tính sticky bit được đặt trên một thư mục, chỉ có người sở hữu tập tin hoặc thư mục con có thể xóa hoặc đổi tên tập tin hoặc thư mục con của mình trong thư mục đó. Điều này bảo vệ các tập tin trong thư mục chung (như /tmp) khỏi việc bị xóa bởi người dùng khác.

·     **Cách đặt thuộc tính sticky bit**:

“chmod +t tên_thư_mục”

·     **Ví dụ**: Thư mục /tmp thường có thuộc tính sticky bit để đảm bảo rằng chỉ người sở hữu tập tin mới có thể xóa hoặc đổi tên tập tin của mình.

·     **Xem thuộc tính sticky bit**: Thuộc tính sticky bit được hiển thị bằng ký tự t trong phần quyền của nhóm, thay vì x.

“ls -ld /tmp”

Kết quả có thể là:

“drwxrwxrwt 10 root root 4096 Sep 1 2023 /tmp”

**Tóm tắt**

·     **SUID**: Tập tin thực thi chạy với quyền của người sở hữu tập tin.

·     **SGID**: Tập tin thực thi chạy với quyền của nhóm sở hữu tập tin, hoặc thư mục có ảnh hưởng đến nhóm của các tập tin con.

·     **Sticky Bit**: Thư mục chỉ cho phép chủ sở hữu của tập tin xóa hoặc đổi tên tập tin của mình.

### Tìm hiểu về Linking file (symbolic, hard link)

**linking** là một phương pháp để tạo liên kết giữa các tập tin.

**1. Hard Link**

·     Hard link là một liên kết trực tiếp đến một tập tin trên hệ thống tập tin. Khi bạn tạo một hard link, bạn tạo một bản sao của tập tin gốc với cùng một inode (định danh duy nhất của tập tin trong hệ thống tập tin). Do đó, cả hai liên kết đều trỏ đến cùng một dữ liệu và thay đổi trong một liên kết sẽ ảnh hưởng đến liên kết khác.

·     **Đặc điểm**:

o  Hard link không thể được tạo ra cho thư mục (ngoại trừ thư mục gốc . và thư mục cha ..).

o  Không thể tạo hard link qua các hệ thống tập tin khác nhau.

o  Xóa một hard link không ảnh hưởng đến các hard link khác hoặc dữ liệu gốc cho đến khi tất cả các liên kết đều bị xóa.

·     **Cú pháp để tạo hard link**:

“ln tên_tập_tin liên_kết”

·     **Ví dụ**: Giả sử bạn có một tập tin file.txt và bạn muốn tạo một hard link đến tập tin đó với tên hardlink.txt:

“ln file.txt hardlink.txt”

Khi bạn kiểm tra inode của cả hai tập tin:

“ls -li file.txt hardlink.txt”

Sẽ thấy rằng cả hai tập tin đều có cùng một số inode, nghĩa là chúng trỏ đến cùng một dữ liệu.

**2. Symbolic Link (Symlink)**

·     Symbolic link là một liên kết đặc biệt (hoặc con trỏ) đến một tập tin hoặc thư mục khác. Symlink không trực tiếp trỏ đến dữ liệu của tập tin, mà thay vào đó trỏ đến đường dẫn của tập tin hoặc thư mục gốc. Nếu tập tin hoặc thư mục gốc bị di chuyển hoặc xóa, symlink sẽ trở thành một liên kết "bị hỏng".

·     **Đặc điểm**:

o  Có thể tạo symlink cho cả tập tin và thư mục.

o  Có thể tạo symlink qua các hệ thống tập tin khác nhau.

o  Nếu bạn xóa tập tin gốc, symlink sẽ trở thành một liên kết bị hỏng và không còn trỏ đến dữ liệu.

·     **Cú pháp để tạo symbolic link**:

“ln -s đường_dẫn_tập_tin_hoặc_thư_mục liên_kết”

·     **Ví dụ**: Giả sử bạn muốn tạo một symbolic link từ file.txt đến symlink.txt:

“ln -s file.txt symlink.txt”

Khi bạn kiểm tra liên kết symbolic:

“ls -l symlink.txt”

Bạn sẽ thấy kết quả như sau:

“lrwxrwxrwx 1 user group 9 Sep 1 12:34 symlink.txt -> file.txt”
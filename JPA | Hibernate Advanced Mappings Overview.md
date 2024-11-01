Trong video này, chúng ta sẽ khám phá các kỹ thuật ánh xạ nâng cao trong Hibernate.

Đến nay, chúng ta chỉ làm quen với ánh xạ cơ bản. Ví dụ như chúng ta đã có lớp `student` và ánh xạ nó tới bảng `student`. Điều này giúp chúng ta bắt đầu làm quen với Hibernate. Nhưng bây giờ, chúng ta sẽ đi sâu hơn vào các tính năng nâng cao.

Với ánh xạ nâng cao trong cơ sở dữ liệu, thông thường bạn sẽ có nhiều bảng và các mối quan hệ giữa chúng. Chúng ta cần mô hình hóa điều này bằng Hibernate.

Chúng ta sẽ khám phá ba loại ánh xạ nâng cao khác nhau: **One-to-One (Một-đối-Một)**, **One-to-Many (Một-đối-Nhiều)** và **Many-to-Many (Nhiều-đối-Nhiều)**.

### 1. Ánh xạ One-to-One
Một giảng viên có thể có một chi tiết về giảng viên như một hồ sơ cá nhân. Ở đây, giảng viên sẽ có các thông tin cơ bản như họ tên và email, trong khi chi tiết giảng viên có các thông tin hồ sơ chi tiết hơn như kênh YouTube, sở thích, LinkedIn, Twitter, và trang Facebook. Dữ liệu này được lưu trong hai bảng riêng biệt.

### 2. Ánh xạ One-to-Many
Giảng viên có thể dạy nhiều khóa học, và mỗi khóa học có một giảng viên duy nhất (trong ví dụ này chúng ta giữ đơn giản). Đây là ánh xạ một-đối-nhiều điển hình.

### 3. Ánh xạ Many-to-One
Đây là mặt ngược lại của ánh xạ một-đối-nhiều. Một khóa học sẽ có một giảng viên, nhưng một giảng viên có thể dạy nhiều khóa học. Đây là mối quan hệ ngược với ánh xạ One-to-Many.

### 4. Ánh xạ Many-to-Many
Khóa học có thể có nhiều học viên, và học viên có thể tham gia nhiều khóa học. Đây là một ví dụ điển hình về ánh xạ nhiều-đối-nhiều.

### Khái niệm về khóa chính, khóa ngoại và cascade
- **Khóa chính**: Dùng để xác định duy nhất một dòng trong bảng.
- **Khóa ngoại**: Dùng để liên kết các bảng, là một trường trong một bảng liên kết đến khóa chính trong bảng khác.
  
Ví dụ: Bảng `instructor` chứa thông tin giảng viên, và `instructor_detail` chứa chi tiết về giảng viên. Một khóa ngoại trong bảng `instructor` sẽ liên kết đến bảng `instructor_detail`, tạo ra mối quan hệ giữa giảng viên và chi tiết của giảng viên.

### Cascade (Chuỗi tác động)
Cascade cho phép áp dụng cùng một hành động lên các thực thể liên quan. Ví dụ, khi lưu một giảng viên thì thông tin chi tiết giảng viên cũng sẽ được lưu theo. Tương tự, khi xóa giảng viên, chi tiết giảng viên cũng sẽ bị xóa (cascade delete). Tuy nhiên, cần cẩn trọng với cascade delete trong quan hệ nhiều-đối-nhiều, ví dụ như với khóa học và học viên, không nên xóa khóa học khi xóa học viên khỏi khóa.

### Eager vs Lazy Loading
- **Eager Loading**: Tải tất cả dữ liệu liên quan ngay khi tải thực thể.
- **Lazy Loading**: Chỉ tải dữ liệu liên quan khi có yêu cầu.

### Quan hệ Unidirectional và Bidirectional
- **Unidirectional (Đơn hướng)**: Một mối quan hệ một chiều, ví dụ từ giảng viên có thể truy cập chi tiết giảng viên.
- **Bidirectional (Hai chiều)**: Mối quan hệ hai chiều, ví dụ từ chi tiết giảng viên có thể truy cập giảng viên và ngược lại.

Chúng ta sẽ đi sâu hơn vào việc mã hóa các loại quan hệ này trong các video tiếp theo.

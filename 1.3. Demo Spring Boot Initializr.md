### Demo Spring Boot Initializr

Trong video này, chúng ta sẽ thực hiện một demo về **Spring Boot Initializr**.

Trước đó, chúng ta đã thảo luận về **Spring Initializr** – một trang web giúp bạn tạo nhanh dự án **Spring** ban đầu. Trang web này nằm tại **start.spring.io**, nơi bạn có thể chọn các dependencies và nó sẽ tạo ra một dự án **Maven** hoặc **Gradle** mà bạn có thể tải xuống và import vào **IDE** của mình như **Eclipse**, **IntelliJ**, **NetBeans**, v.v.

### Maven là gì?

Khi xây dựng các dự án **Java**, bạn có thể cần thêm các **JAR files** như **Spring**, **Hibernate**, **Commons Logging**, **JSON**, và nhiều thứ khác. Một cách là tải thủ công các **JAR** này từ trang web của từng dự án và thêm chúng vào **build/classpath**. Tuy nhiên, **Maven** cung cấp một giải pháp tự động. Bạn chỉ cần chỉ định cho Maven biết dự án và các dependencies mà bạn cần, như **Spring**, **Hibernate**, v.v., Maven sẽ tự động tải về và thêm vào **classpath** của bạn, giúp quá trình phát triển trở nên đơn giản hơn nhiều.

Hãy nghĩ về Maven như một "người trợ lý cá nhân" của bạn. Bạn chỉ cần cung cấp danh sách những thứ cần mua sắm (dependencies), và Maven sẽ tự động làm tất cả cho bạn.

### Quy trình phát triển cơ bản

1. **Cấu hình dự án** tại trang **Spring Initializr** (start.spring.io).
2. **Tải xuống** file ZIP chứa dự án đã tạo.
3. **Giải nén** file ZIP đó.
4. **Import dự án Maven** vào IDE của bạn.

### Bắt đầu demo

1. Mở trình duyệt và truy cập vào **start.spring.io**.
2. Chọn **Maven** và **Java** làm ngôn ngữ phát triển.
3. Chọn phiên bản **Spring Boot** mới nhất (tránh phiên bản snapshot).
4. Thiết lập thông tin metadata cho dự án:
   - **Group ID**: com.luv2code.springboot.demo
   - **Artifact ID**: mycoolapp
5. Chọn dependencies cần thiết cho dự án. Ở đây, chúng ta chọn **Web** để có khả năng phát triển ứng dụng web toàn diện với **Tomcat** và **Spring MVC**.
6. Nhấn nút **Generate Project** để tải xuống file ZIP của dự án.

### Giải nén dự án

1. Vào thư mục **Downloads** trên máy tính và tìm file ZIP vừa tải xuống, ví dụ: **mycoolapp.zip**.
2. Giải nén file và di chuyển thư mục giải nén vào thư mục làm việc, ví dụ: **dev-spring-boot**.
3. Bên trong thư mục này sẽ có file **POM.xml**, các file cấu hình khác, và thư mục **src** chứa mã nguồn.

### Import dự án vào IDE

1. Mở IDE yêu thích của bạn (trong demo này, sử dụng **IntelliJ**).
2. Import dự án **Maven** từ thư mục đã giải nén (ví dụ: **dev-spring-boot/mycoolapp**).
3. IDE sẽ tải về tất cả các dependencies mà dự án cần thông qua **Maven**.

### Cấu trúc dự án Spring Boot

Dự án bao gồm các file chính:
- **pom.xml**: Tập tin quản lý dependencies của **Maven**.
- **MycoolappApplication.java**: Đây là file chính chứa hàm `main` của ứng dụng Spring Boot.
- **resources** và **test**: Các thư mục chứa tài nguyên và mã kiểm thử.

### Chạy ứng dụng Spring Boot

1. Mở file **MycoolappApplication.java**.
2. Chạy ứng dụng dưới dạng **Java Application** (không cần chạy trên server, vì Spring Boot đã bao gồm server nhúng).
3. Sau khi chạy, kiểm tra log. Bạn sẽ thấy **Tomcat** đã được khởi tạo trên **port 8080**.
4. Mở trình duyệt và truy cập vào **localhost:8080**. Bạn sẽ thấy một trang lỗi vì chưa có mã điều khiển hay trang web nào được tạo ra, nhưng server đã hoạt động bình thường.

### Kết luận

Bây giờ bạn đã có một ứng dụng **Spring Boot** cơ bản chạy với **Tomcat nhúng**. Trong các video tiếp theo, chúng ta sẽ xây dựng thêm chức năng cho ứng dụng này. Hãy sẵn sàng khám phá sâu hơn trong những video tiếp theo!

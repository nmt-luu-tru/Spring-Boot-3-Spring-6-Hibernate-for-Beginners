### Giới thiệu về Spring Boot

Trong video này, chúng ta sẽ tìm hiểu về **Spring Boot**.

### Spring là gì?
**Spring** là một framework rất phổ biến để phát triển các ứng dụng **Java**, cung cấp nhiều lớp trợ giúp và các annotation để làm cho việc phát triển dễ dàng hơn. Tuy nhiên, việc xây dựng một ứng dụng Spring truyền thống có nhiều thách thức, chẳng hạn như:
- Xác định **JAR dependencies** cần thiết cho dự án Spring.
- Cấu hình hệ thống và quyết định sử dụng **cấu hình XML** hay **cấu hình Java**.
- Cài đặt và cấu hình server (**Tomcat**, **JBoss**, **WebSphere**, v.v.).

Những phức tạp này xuất hiện trước khi bạn thực sự bắt đầu xây dựng ứng dụng của mình, và đó là nơi **Spring Boot** hỗ trợ.

### Spring Boot là gì?
**Spring Boot** giúp đơn giản hóa quá trình phát triển các ứng dụng **Spring** bằng cách tự động hóa nhiều công đoạn cấu hình. Nó giảm thiểu việc cấu hình thủ công, tự động cấu hình dựa trên **properties file** và **classpath**, và giúp giải quyết các xung đột phụ thuộc (**dependency conflicts**). Nó cũng cung cấp một **HTTP server nhúng** sẵn, chẳng hạn như **Tomcat**, **Jetty**, hoặc **Undertow**, giúp bạn có thể bắt đầu phát triển nhanh chóng mà không cần cài đặt server riêng biệt.

### Mối quan hệ giữa Spring Boot và Spring
**Spring Boot** không thay thế **Spring**; thay vào đó, nó làm cho Spring dễ sử dụng hơn. **Spring Boot** sử dụng **Spring** ở phía sau, vì vậy khi bạn sử dụng **Spring Boot**, thực chất bạn vẫn đang chạy mã của **Spring**. Trong khóa học này, chúng ta sẽ học cả **Spring Boot** và **Spring**.

### Các tính năng của Spring Boot:
- **Embedded server**: Spring Boot bao gồm một server nhúng (ví dụ: **Tomcat**) trong ứng dụng của bạn. Khi bạn tạo ra một file JAR cho ứng dụng (ví dụ: `mycoolapp.jar`), nó sẽ bao gồm cả mã ứng dụng và server nhúng. Điều này có nghĩa là bạn không cần cài đặt server riêng biệt.
- **Standalone apps**: Vì ứng dụng của bạn bao gồm cả server, bạn có thể chạy nó độc lập. Ví dụ, từ dòng lệnh, bạn có thể nhập `java -jar mycoolapp.jar`, và ứng dụng cùng với server nhúng sẽ được chạy độc lập.
- **Triển khai file WAR**: Nếu tổ chức của bạn yêu cầu triển khai truyền thống (như sử dụng file **WAR** trên các server **Tomcat**, **JBoss**, hoặc **WebSphere**), **Spring Boot** cũng hỗ trợ việc này. Bạn có thể đóng gói ứng dụng **Spring Boot** của mình dưới dạng file **WAR** và triển khai nó lên server bên ngoài nếu cần.

### Spring Boot và các công nghệ Spring truyền thống
**Spring Boot** không thay thế các công nghệ như **Spring MVC**, **Spring REST**. Thay vào đó, nó làm việc với chúng, cung cấp cách cấu hình đơn giản và nhanh chóng hơn. Bạn vẫn có thể sử dụng toàn bộ các tính năng của **Spring Core**, **Spring AOP**, **Spring MVC**, và **Spring REST** khi làm việc với Spring Boot.

### Các câu hỏi thường gặp về Spring Boot
1. **Spring Boot có thay thế Spring MVC hay Spring REST không?**
   - Không, **Spring Boot** sử dụng các công nghệ này ở phía sau. Nó chỉ giúp đơn giản hóa việc cấu hình, nhưng không thay thế các công nghệ Spring.
   
2. **Mã của Spring Boot có chạy nhanh hơn mã Spring truyền thống không?**
   - Không, vì **Spring Boot** vẫn sử dụng mã của Spring. Mục đích chính của **Spring Boot** là giúp bắt đầu nhanh chóng và giảm thiểu việc cấu hình.

3. **Tôi có cần IDE đặc biệt để phát triển Spring Boot không?**
   - Không, bạn có thể sử dụng bất kỳ **IDE** nào để phát triển ứng dụng Spring Boot. Bạn cũng có thể sử dụng **Spring Tool Suite (STS)**, một bộ plugin miễn phí dành cho Spring, nhưng không bắt buộc. Thậm chí bạn có thể chỉ dùng trình soạn thảo văn bản và **Maven** trên dòng lệnh.

### Spring Initializer
**Spring Boot** cung cấp công cụ **Spring Initializer**, một trang web tại **start.spring.io** giúp bạn nhanh chóng tạo một dự án Spring Boot. Bạn chỉ cần chọn các dependency cần thiết, và nó sẽ tạo ra một dự án **Maven** hoặc **Gradle** để bạn tải về và import vào IDE của mình (như **IntelliJ**, **Eclipse**, **NetBeans**). Chúng ta sẽ sử dụng **Spring Initializer** nhiều lần trong khóa học này để thiết lập các dự án.

### Kết luận
Đây là phần giới thiệu ngắn về **Spring Boot**. Trong các video tiếp theo, chúng ta sẽ đi sâu hơn vào các chi tiết của Spring Boot và thực hành với các ví dụ. Hẹn gặp lại bạn trong các bài học tiếp theo!

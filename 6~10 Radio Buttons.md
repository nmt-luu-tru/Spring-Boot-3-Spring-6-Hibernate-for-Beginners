### Tìm Hiểu Spring MVC Forms với Radio Buttons

Trong video này, chúng ta sẽ khám phá cách sử dụng radio buttons trong các form Spring MVC với Thymeleaf. Radio buttons là một phần quan trọng trong các form HTML, cho phép người dùng chọn một tùy chọn duy nhất từ danh sách các lựa chọn có sẵn. Chúng ta sẽ xây dựng một form cho phép người dùng chọn ngôn ngữ lập trình yêu thích của họ.

### Tổng Quan về Radio Buttons trong HTML

Radio buttons trong HTML được sử dụng để cho phép người dùng chọn một tùy chọn duy nhất từ một nhóm các tùy chọn. Dưới đây là một ví dụ cơ bản về cách sử dụng radio buttons:

```html
<label for="favLanguage">Favorite Programming Language:</label><br/>
<input type="radio" name="favLanguage" value="Go"> Go<br/>
<input type="radio" name="favLanguage" value="Java"> Java<br/>
<input type="radio" name="favLanguage" value="Python"> Python<br/>
```

- **`name="favLanguage"`**: Tên của nhóm radio buttons, đảm bảo rằng chỉ một tùy chọn có thể được chọn trong nhóm này.
- **`value="Go"`**: Giá trị được gửi khi form được submit nếu tùy chọn này được chọn.
- **`Go`**: Văn bản hiển thị cho người dùng.

### Sử Dụng Thymeleaf với Radio Buttons

Khi sử dụng Thymeleaf cùng với Spring MVC, chúng ta có thể dễ dàng tạo radio buttons bằng cách liên kết chúng với các thuộc tính của đối tượng Java. Điều này giúp việc quản lý dữ liệu nhập liệu trở nên hiệu quả và tự động.

### Các Bước Phát Triển Ứng Dụng với Radio Buttons

Chúng ta sẽ đi qua các bước sau:
1. **Cập nhật lớp `Student` để thêm thuộc tính `favoriteLanguage`.**
2. **Thêm danh sách ngôn ngữ lập trình vào `application.properties`.**
3. **Cập nhật controller để xử lý dữ liệu từ radio buttons và inject danh sách ngôn ngữ lập trình.**
4. **Cập nhật form HTML để thêm radio buttons sử dụng danh sách từ model.**
5. **Cập nhật trang xác nhận để hiển thị ngôn ngữ lập trình yêu thích.**
6. **Thử nghiệm ứng dụng.**

#### Bước 1: Cập Nhật Lớp `Student` để Thêm Thuộc Tính `favoriteLanguage`

Mở file `Student.java` trong package `model` và thêm thuộc tính `favoriteLanguage` cùng với getter và setter.

```java
package com.luv2code.springboot.thymeleafdemo.model;

public class Student {
    
    private String firstName;
    private String lastName;
    private String country; // Thuộc tính đã có
    private String favoriteLanguage; // Thuộc tính mới

    // Constructor không tham số
    public Student() {
    }

    // Getter và Setter cho firstName
    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    // Getter và Setter cho lastName
    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    // Getter và Setter cho country
    public String getCountry() {
        return country;
    }

    public void setCountry(String country) {
        this.country = country;
    }

    // Getter và Setter cho favoriteLanguage
    public String getFavoriteLanguage() {
        return favoriteLanguage;
    }

    public void setFavoriteLanguage(String favoriteLanguage) {
        this.favoriteLanguage = favoriteLanguage;
    }
}
```

**Giải thích:**
- **`private String favoriteLanguage;`**: Khai báo thuộc tính để lưu trữ ngôn ngữ lập trình yêu thích.
- **Getter và Setter**: Các phương thức `getFavoriteLanguage` và `setFavoriteLanguage` để truy cập và cập nhật giá trị.

#### Bước 2: Thêm Danh Sách Ngôn Ngữ Lập Trình vào `application.properties`

Mở file `application.properties` và thêm danh sách các ngôn ngữ lập trình.

```properties
countries=Brazil,France,Germany,India,Mexico,Spain,United States
languages=Go,Java,Python,Rust,TypeScript
```

**Giải thích:**
- **`countries`**: Danh sách các quốc gia được sử dụng trong dropdown list.
- **`languages`**: Danh sách các ngôn ngữ lập trình được sử dụng trong radio buttons.

#### Bước 3: Cập Nhật Controller để Xử Lý Dữ Liệu từ Radio Buttons và Inject Danh Sách Ngôn Ngữ Lập Trình

Mở file `StudentController.java` trong package `controller` và cập nhật như sau:

```java
package com.luv2code.springboot.thymeleafdemo.controller;

import com.luv2code.springboot.thymeleafdemo.model.Student;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.GetMapping;

import java.util.List;

@Controller
public class StudentController {

    // Inject danh sách các quốc gia từ application.properties
    @Value("#{'${countries}'.split(',')}")
    private List<String> countries;

    // Inject danh sách các ngôn ngữ lập trình từ application.properties
    @Value("#{'${languages}'.split(',')}")
    private List<String> languages;

    // Phương thức để hiển thị form
    @GetMapping("/showForm")
    public String showForm(Model theModel) {
        // Tạo một đối tượng Student mới
        Student theStudent = new Student();
        
        // Thêm đối tượng Student vào model
        theModel.addAttribute("student", theStudent);
        
        // Thêm danh sách các quốc gia và ngôn ngữ vào model
        theModel.addAttribute("countries", countries);
        theModel.addAttribute("languages", languages);
        
        return "student-form";
    }

    // Phương thức để xử lý khi người dùng gửi form
    @PostMapping("/processForm")
    public String processForm(@ModelAttribute("student") Student theStudent) {
        
        // Hiển thị thông tin student để kiểm tra
        System.out.println("Student First Name: " + theStudent.getFirstName());
        System.out.println("Student Last Name: " + theStudent.getLastName());
        System.out.println("Student Country: " + theStudent.getCountry());
        System.out.println("Favorite Language: " + theStudent.getFavoriteLanguage());
        
        return "student-confirmation";
    }
}
```

**Giải thích chi tiết:**
- **`@Value("#{'${languages}'.split(',')}")`**: Inject danh sách các ngôn ngữ lập trình từ `application.properties`, tách chuỗi bằng dấu phẩy và lưu vào danh sách `languages`.
- **`theModel.addAttribute("languages", languages);`**: Thêm danh sách ngôn ngữ vào model để Thymeleaf có thể truy cập và sử dụng trong form.

#### Bước 4: Cập Nhật Form HTML để Thêm Radio Buttons Sử Dụng Danh Sách Từ Model

Mở lại file `student-form.html` trong thư mục `templates` và thay thế phần radio buttons hardcoded bằng việc tạo radio buttons động từ danh sách ngôn ngữ trong model.

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Student Registration Form</title>
</head>
<body>

<h2>Student Registration Form</h2>

<form th:action="@{/processForm}" th:object="${student}" method="post">
    First Name: <input type="text" th:field="*{firstName}" /><br/><br/>
    Last Name: <input type="text" th:field="*{lastName}" /><br/><br/>
    
    <!-- Dropdown List Cho Quốc Gia -->
    <label for="country">Country:</label>
    <select th:field="*{country}">
        <option value="" disabled selected>Select your country</option>
        <option th:each="country : ${countries}"
                th:value="${country}"
                th:text="${country}">Country</option>
    </select><br/><br/>
    
    <!-- Radio Buttons Cho Ngôn Ngữ Lập Trình Yêu Thích -->
    <label>Favorite Programming Language:</label><br/>
    <div th:each="language : ${languages}">
        <input type="radio" th:field="*{favoriteLanguage}" th:value="${language}" /> <span th:text="${language}"></span><br/>
    </div><br/>
    
    <button type="submit">Submit</button>
</form>

</body>
</html>
```

**Giải thích chi tiết:**
- **`<div th:each="language : ${languages}">`**: Lặp qua danh sách `languages` từ model để tạo các radio buttons.
- **`th:field="*{favoriteLanguage}"`**: Liên kết radio button với thuộc tính `favoriteLanguage` trong đối tượng `Student`. Khi bạn sử dụng thuộc tính `th:field` trong Thymeleaf, nó không chỉ liên kết trường nhập liệu với thuộc tính `favoriteLanguage` của đối tượng **Student** mà còn **tự động tạo thuộc tính name** cho các thẻ `<input>`. Điều này đảm bảo rằng người dùng chỉ có thể chọn một tùy chọn trong nhóm.
- **`th:value="${language}"`**: Thiết lập giá trị của radio button là tên ngôn ngữ lập trình.
- **`<span th:text="${language}"></span>`**: Hiển thị văn bản của ngôn ngữ lập trình cho người dùng.

#### Bước 5: Cập Nhật Trang Xác Nhận `student-confirmation.html`

Mở file `student-confirmation.html` trong thư mục `templates` và thêm phần hiển thị ngôn ngữ lập trình yêu thích.

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Student Confirmation</title>
</head>
<body>

<h2>Student is confirmed</h2>

<p>First Name: <span th:text="${student.firstName}"></span></p>
<p>Last Name: <span th:text="${student.lastName}"></span></p>
<p>Country: <span th:text="${student.country}"></span></p>
<p>Favorite Programming Language: <span th:text="${student.favoriteLanguage}"></span></p> <!-- Thêm dòng này -->

</body>
</html>
```

**Giải thích:**
- **`<p>Favorite Programming Language: <span th:text="${student.favoriteLanguage}"></span></p>`**: Hiển thị ngôn ngữ lập trình yêu thích mà người dùng đã chọn.

#### Bước 6: Thử Nghiệm Ứng Dụng

1. **Khởi chạy ứng dụng**: Chạy ứng dụng Spring Boot của bạn.
2. **Truy cập form**: Mở trình duyệt và truy cập `http://localhost:8080/showForm`.
3. **Nhập dữ liệu**:
    - Nhập `First Name` và `Last Name`.
    - Chọn quốc gia từ dropdown list.
    - Chọn ngôn ngữ lập trình yêu thích từ các radio buttons.
4. **Submit form**: Nhấn nút "Submit".
5. **Xem kết quả**: Trang `student-confirmation.html` sẽ hiển thị thông tin đã nhập từ người dùng, bao gồm cả ngôn ngữ lập trình yêu thích.

**Ví dụ Kết Quả:**

```
Student is confirmed

First Name: John
Last Name: Doe
Country: Germany
Favorite Programming Language: Java
```

### Tổng Kết Các Bước Phát Triển

1. **Cập Nhật Lớp `Student`**: Thêm thuộc tính `favoriteLanguage` và các phương thức getter, setter.
2. **Thêm Danh Sách Ngôn Ngữ Lập Trình vào `application.properties`**: Định nghĩa các ngôn ngữ lập trình trong file cấu hình.
3. **Cập Nhật Controller**: Inject danh sách ngôn ngữ lập trình từ `application.properties` và thêm chúng vào model để sử dụng trong form.
4. **Cập Nhật Form HTML**: Thêm radio buttons vào form sử dụng Thymeleaf để liên kết với thuộc tính `favoriteLanguage` của đối tượng `Student`.
5. **Cập Nhật Trang Xác Nhận**: Hiển thị ngôn ngữ lập trình yêu thích mà người dùng đã chọn.
6. **Thử Nghiệm Ứng Dụng**: Đảm bảo rằng radio buttons hoạt động đúng và dữ liệu được xử lý chính xác.

### Lợi Ích của Việc Sử Dụng Radio Buttons và Data Binding trong Spring MVC

- **Tính Tự Động**: Data binding giúp tự động liên kết dữ liệu từ form với các thuộc tính của đối tượng Java, giảm thiểu việc xử lý thủ công và giảm lỗi.
- **Dễ Dàng Bảo Trì**: Sử dụng Thymeleaf để tạo radio buttons động từ danh sách ngôn ngữ lập trình giúp mã nguồn trở nên sạch sẽ và dễ hiểu.
- **Linh Hoạt**: Danh sách ngôn ngữ lập trình được quản lý từ `application.properties` giúp dễ dàng cập nhật và mở rộng danh sách mà không cần sửa mã nguồn.
- **Tăng Tính Hiệu Quả**: Việc tạo các form phức tạp với nhiều loại trường nhập liệu như text fields, dropdown lists, và radio buttons trở nên đơn giản và hiệu quả hơn.

### Kết Luận

Bằng cách sử dụng Spring MVC cùng với Thymeleaf, chúng ta có thể xây dựng các form nhập liệu mạnh mẽ và linh hoạt, hỗ trợ nhiều loại trường dữ liệu khác nhau như text fields, dropdown lists, và radio buttons. Data binding giúp tự động liên kết dữ liệu từ form với các đối tượng Java, giảm thiểu công sức và tăng tính chính xác trong việc xử lý dữ liệu. Việc quản lý danh sách các tùy chọn từ `application.properties` giúp ứng dụng trở nên dễ dàng mở rộng và bảo trì.

Chúc bạn thành công trong việc xây dựng các form Spring MVC với các loại trường dữ liệu đa dạng và hiệu quả!

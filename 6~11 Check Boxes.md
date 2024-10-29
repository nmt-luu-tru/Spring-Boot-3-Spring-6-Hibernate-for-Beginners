### Tìm Hiểu Spring MVC Forms với Check Boxes

Trong video này, chúng ta sẽ tìm hiểu cách sử dụng check boxes trong các form Spring MVC với Thymeleaf. Check boxes cho phép người dùng lựa chọn nhiều tùy chọn cùng một lúc, khác biệt so với radio buttons chỉ cho phép chọn một tùy chọn duy nhất. Chúng ta sẽ xây dựng một form để người dùng có thể chọn nhiều hệ điều hành yêu thích.

### Tổng Quan về Check Boxes trong HTML

Check boxes trong HTML được sử dụng để cho phép người dùng chọn nhiều tùy chọn từ một nhóm các lựa chọn có sẵn. Dưới đây là một ví dụ cơ bản về cách sử dụng check boxes:

```html
<label for="favOS">Favorite Operating Systems:</label><br/>
<input type="checkbox" name="favOS" value="Linux"> Linux<br/>
<input type="checkbox" name="favOS" value="Mac OS"> Mac OS<br/>
<input type="checkbox" name="favOS" value="Microsoft Windows"> Microsoft Windows<br/>
```

- **`name="favOS"`**: Tên của nhóm check boxes, cho phép người dùng chọn nhiều tùy chọn cùng lúc.
- **`value="Linux"`**: Giá trị được gửi khi check box này được chọn.
- **`Linux`**: Văn bản hiển thị cho người dùng.

### Sử Dụng Thymeleaf với Check Boxes

Khi sử dụng Thymeleaf cùng với Spring MVC, chúng ta có thể dễ dàng tạo check boxes bằng cách liên kết chúng với các thuộc tính của đối tượng Java. Điều này giúp quản lý dữ liệu nhập liệu trở nên hiệu quả và tự động.

### Các Bước Phát Triển Ứng Dụng với Check Boxes

Chúng ta sẽ thực hiện theo quy trình sau:
1. **Thêm danh sách các hệ điều hành vào `application.properties`.**
2. **Cập nhật lớp `Student` để thêm thuộc tính `favoriteSystems`.**
3. **Cập nhật controller để xử lý dữ liệu từ check boxes và inject danh sách các hệ điều hành.**
4. **Cập nhật form HTML để thêm check boxes sử dụng danh sách từ model.**
5. **Cập nhật trang xác nhận để hiển thị các hệ điều hành được chọn.**
6. **Thử nghiệm ứng dụng.**

#### Bước 1: Thêm Danh Sách Các Hệ Điều Hành vào `application.properties`

Mở file `application.properties` và thêm danh sách các hệ điều hành dưới dạng một chuỗi được phân tách bằng dấu phẩy.

```properties
countries=Brazil,France,Germany,India,Mexico,Spain,United States
languages=Go,Java,Python,Rust,TypeScript
systems=Linux,Mac OS,Microsoft Windows,Android,iOS
```

**Giải thích:**
- **`countries`**: Danh sách các quốc gia được sử dụng trong dropdown list.
- **`languages`**: Danh sách các ngôn ngữ lập trình được sử dụng trong radio buttons.
- **`systems`**: Danh sách các hệ điều hành được sử dụng trong check boxes.

#### Bước 2: Cập Nhật Lớp `Student` để Thêm Thuộc Tính `favoriteSystems`

Mở file `Student.java` trong package `model` và thêm thuộc tính `favoriteSystems` cùng với getter và setter.

```java
package com.luv2code.springboot.thymeleafdemo.model;

import java.util.List;

public class Student {
    
    private String firstName;
    private String lastName;
    private String country; // Thuộc tính đã có
    private String favoriteLanguage; // Thuộc tính đã có
    private List<String> favoriteSystems; // Thuộc tính mới

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

    // Getter và Setter cho favoriteSystems
    public List<String> getFavoriteSystems() {
        return favoriteSystems;
    }

    public void setFavoriteSystems(List<String> favoriteSystems) {
        this.favoriteSystems = favoriteSystems;
    }
}
```

**Giải thích:**
- **`private List<String> favoriteSystems;`**: Khai báo thuộc tính `favoriteSystems` để lưu trữ các hệ điều hành được chọn.
- **Getter và Setter**: Phương thức `getFavoriteSystems` và `setFavoriteSystems` để truy cập và cập nhật giá trị của thuộc tính `favoriteSystems`.

#### Bước 3: Cập Nhật Controller để Xử Lý Dữ Liệu từ Check Boxes và Inject Danh Sách Các Hệ Điều Hành

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

    // Inject danh sách các hệ điều hành từ application.properties
    @Value("#{'${systems}'.split(',')}")
    private List<String> systems;

    // Phương thức để hiển thị form
    @GetMapping("/showForm")
    public String showForm(Model theModel) {
        // Tạo một đối tượng Student mới
        Student theStudent = new Student();
        
        // Thêm đối tượng Student vào model
        theModel.addAttribute("student", theStudent);
        
        // Thêm danh sách các quốc gia, ngôn ngữ và hệ điều hành vào model
        theModel.addAttribute("countries", countries);
        theModel.addAttribute("languages", languages);
        theModel.addAttribute("systems", systems);
        
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
        System.out.println("Favorite Operating Systems: " + theStudent.getFavoriteSystems());
        
        return "student-confirmation";
    }
}
```

**Giải thích chi tiết:**
- **`@Value("#{'${systems}'.split(',')}")`**: Sử dụng annotation `@Value` để inject danh sách các hệ điều hành từ tệp `application.properties`. Dữ liệu sẽ được tách bằng dấu phẩy và lưu vào danh sách `systems`.
- **`theModel.addAttribute("systems", systems);`**: Thêm danh sách hệ điều hành vào model để Thymeleaf có thể truy cập và sử dụng trong form.
- **Phương thức `processForm`**: Nhận đối tượng `Student` đã được bind từ form thông qua `@ModelAttribute("student")`, và in ra thông tin để kiểm tra, bao gồm cả các hệ điều hành được chọn.

#### Bước 4: Cập Nhật Form HTML để Thêm Check Boxes Sử Dụng Danh Sách Từ Model

Mở lại file `student-form.html` trong thư mục `templates` và thay thế phần check boxes hardcoded bằng việc tạo check boxes động từ danh sách hệ điều hành trong model.

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
    
    <!-- Check Boxes Cho Hệ Điều Hành Yêu Thích -->
    <label>Favorite Operating Systems:</label><br/>
    <div th:each="system : ${systems}">
        <input type="checkbox" th:field="*{favoriteSystems}" th:value="${system}" /> <span th:text="${system}"></span><br/>
    </div><br/>
    
    <button type="submit">Submit</button>
</form>

</body>
</html>
```

**Giải thích chi tiết:**
- **`<div th:each="system : ${systems}">`**: Lặp qua danh sách `systems` từ model để tạo các check boxes động.
- **`th:field="*{favoriteSystems}"`**: Liên kết check box với thuộc tính `favoriteSystems` trong đối tượng `Student`.
- **`th:value="${system}"`**: Thiết lập giá trị của check box là tên hệ điều hành.
- **`<span th:text="${system}"></span>`**: Hiển thị tên hệ điều hành cho người dùng.

#### Bước 5: Cập Nhật Trang Xác Nhận `student-confirmation.html`

Mở file `student-confirmation.html` trong thư mục `templates` và thêm phần hiển thị các hệ điều hành được chọn.

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
<p>Favorite Programming Language: <span th:text="${student.favoriteLanguage}"></span></p>
<p>Favorite Operating Systems:</p>
<ul>
    <li th:each="system : ${student.favoriteSystems}" th:text="${system}"></li>
</ul>

</body>
</html>
```

**Giải thích:**
- **`<ul>` và `<li>`**: Sử dụng danh sách không thứ tự để hiển thị các hệ điều hành được chọn dưới dạng các mục riêng biệt.
- **`th:each="system : ${student.favoriteSystems}"`**: Lặp qua danh sách `favoriteSystems` từ đối tượng `Student` để tạo các mục trong danh sách.
- **`th:text="${system}"`**: Hiển thị tên hệ điều hành cho từng mục trong danh sách.

#### Bước 6: Thử Nghiệm Ứng Dụng

1. **Khởi chạy ứng dụng**: Chạy ứng dụng Spring Boot của bạn.
2. **Truy cập form**: Mở trình duyệt và truy cập `http://localhost:8080/showForm`.
3. **Nhập dữ liệu**:
    - Nhập `First Name` và `Last Name`.
    - Chọn quốc gia từ dropdown list.
    - Chọn ngôn ngữ lập trình yêu thích từ radio buttons.
    - Chọn một hoặc nhiều hệ điều hành yêu thích từ các check boxes.
4. **Submit form**: Nhấn nút "Submit".
5. **Xem kết quả**: Trang `student-confirmation.html` sẽ hiển thị thông tin đã nhập từ người dùng, bao gồm cả các hệ điều hành được chọn.

**Ví dụ Kết Quả:**

```
Student is confirmed

First Name: John
Last Name: Doe
Country: Germany
Favorite Programming Language: Java
Favorite Operating Systems:
- Linux
- Mac OS
```

### Phân Tích Kỹ Thuật và Lợi Ích của Check Boxes và Data Binding

- **Data Binding với Spring MVC**: Tự động liên kết dữ liệu từ form với các thuộc tính của đối tượng `Student` trong model, giúp giảm thiểu việc xử lý thủ công từng tham số từ form.
- **Thymeleaf hỗ trợ Data Binding**: Với cú pháp `th:field` và `th:object`, Thymeleaf giúp việc kết nối dữ liệu từ model vào form trở nên dễ dàng và trực quan.
- **Đa Lựa Chọn với Check Boxes**: Người dùng có thể chọn nhiều tùy chọn cùng lúc, phù hợp với các trường hợp yêu cầu lựa chọn đa dạng như hệ điều hành yêu thích.
- **Linh Hoạt trong Quản Lý Dữ Liệu**: Việc quản lý danh sách các tùy chọn như quốc gia, ngôn ngữ lập trình và hệ điều hành thông qua `application.properties` giúp dễ dàng cập nhật và mở rộng danh sách mà không cần sửa mã nguồn.
- **Tăng Tính Hiệu Quả**: Việc tạo các form phức tạp với nhiều loại trường nhập liệu như text fields, dropdown lists, radio buttons và check boxes trở nên đơn giản và hiệu quả hơn.

### Kết Luận

Bằng cách sử dụng Spring MVC với Thymeleaf, chúng ta có thể dễ dàng xây dựng các form nhập liệu mạnh mẽ hỗ trợ nhiều loại trường dữ liệu khác nhau như text fields, dropdown lists, radio buttons và check boxes. Data binding giúp tự động liên kết dữ liệu từ form với các đối tượng Java, giảm thiểu công sức và tăng tính chính xác trong việc xử lý dữ liệu. Việc quản lý danh sách các tùy chọn từ `application.properties` giúp ứng dụng trở nên dễ dàng mở rộng và bảo trì.

Chúc bạn thành công trong việc xây dựng các form Spring MVC với các loại trường dữ liệu đa dạng và hiệu quả!

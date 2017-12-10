# Composite Partern
Composite pattern được sử dụng khá nhiều. Composite Pattern nó là Structural Design Pattern, là mẫu thiết kế liên quan đến cấu trúc, kết cấu của các đối tượng. Nó được áp dụng để cấu trúc một class theo tiêu chuẩn hoặc điều chỉnh cấu trúc một class đang tồn tại.  
Trong thực tế, một form HTML có thể chứa một hoặc nhiều các thành phần form, mỗi thành phần này sẽ có cùng các hành vi như hiển thị, kiểm tra dữ liệu, hiển thị lỗi… Nếu không áp dụng các mẫu thì chúng ta sẽ lặp đi lặp lại code rất nhiều và giải pháp cho vấn đề này là ứng dụng Composite pattern. Chúng ta tạo ra một abstract class:

```
abstract class FormComponent {
	abstract function add (FormComponent $obj);.  
 	abstract function remove (FormComponent $obj);  
 	abstract function display();  
	abstract function validate();  
	abstract function showError();  
}
```
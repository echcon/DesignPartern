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
Lớp trừu tượng ở trên có sử dụng type hinting (cách xác định dạng dữ liệu cho tham số), hai phương thức đầu chính là cách mà Composite pattern sử dụng. Mỗi lớp con sẽ kế thừa từ lớp cha và nó cần phải định nghĩa các phương thức trìu tượng được implement từ lớp cha trìu tượng. Ví dụ:  

```
class Form extends FormComponent {
  private $_elements = array();
  function add(FormComponent $obj) {
    $this->_elements[] = $obj;
  }
  function display() {
    // Display the entire form.
  }
}
class FormElement extends FormComponent {
  function add(FormComponent $obj) {
    return $obj; // Or false.
  }
  function display() {
    // Display the element.
  }
}
```
**Class Form** định nghĩa phương thức **add()** được implement từ **FormConponent**, nó cho phép bạn thêm thành phần vào form:  

```
$form = new Form();
$email = new FormElement();
$form->add($email);
```
Chú ý là **FormElement** cũng định nghĩa phương thức **add()**, nhưng phương thức này không làm gì cả, vì chúng ta không cần thêm thành phần form vào một thành phần form. Thay vào đó, phương thức **add()** này trả về đối tượng được thêm vào hoặc trả về một giá trị hoặc bung ra một lỗi.

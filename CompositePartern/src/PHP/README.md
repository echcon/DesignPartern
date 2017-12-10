# PHP
## Ví dụ áp dụng Composite Pattern
Với ví dụ ở dạng mẫu trên, chúng ta vẫn chưa thật sự hiểu rõ về Composite pattern. Một ví dụ cụ thể tiếp theo sẽ giúp bạn hiểu chi tiết. Ví dụ dưới đây về một ứng dụng quản lý các công việc cần làm của một nhóm và của từng thành viên trong nhóm.  

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Ví dụ về Composite pattern</title>
</head>
<body>
    <h2>Ví dụ về Composite pattern</h2>
    <?php
    #------------ ĐỊNH NGHĨA CLASS ----------------------#
    /* Định nghĩa class WorkUnit sử dụng Composite pattern
     * Lớp có 2 thuộc tính: tasks, name.
     * Lớp có 5 phương thức: __construct(), getName(), add(), remove(), assignTask(), completeTask().
     */
    abstract class WorkUnit {
        // Các tác vụ cần làm
        protected $tasks = array();
        // Lưu tên nhân viên hoặc tên nhóm
        protected $name = NULL;

        function __construct($name) {
            $this->name = $name;
        }
        function getName() {
            return $this->name;
        }
        // Các phương thức trìu tượng cần thực hiện
        abstract function add(Employee $e);
        abstract function remove(Employee $e);
        abstract function assignTask($task);
        abstract function completeTask($task);
    }
    
    /* Lớp Team mở rộng từ lớp WorkUnit.
     * Lớp có 1 thuộc tính: _employees.
     * Lớp có 1 phương thức: getCount().
     */
    class Team extends WorkUnit {
        // Lưu các thành viên của nhóm
        private $_employees = array();
    
        // Thực hiện các phương thức trìu tượng
        function add(Employee $e) {
            $this->_employees[] = $e;
            echo "<p>{$e->getName()} gia nhập nhóm {$this->getName()}.</p>";
        }
        function remove(Employee $e) {
            $index = array_search($e, $this->_employees);
            unset($this->_employees[$index]);
            echo "<p>{$e->getName()} bị đuổi khỏi nhóm {$this->getName()}.</p>";
        }
        function assignTask($task) {
            $this->tasks[] = $task;
            echo "<p>Một tác vụ được gán cho nhóm {$this->getName()}. Nó có thể hoàn thành dễ dàng với {$this->getCount()} thành viên.</p>";
        }
        function completeTask($task) {
            $index = array_search($task, $this->tasks);
            unset($this->tasks[$index]);
            echo "<p>Nhiệm vụ '$task' đã hoàn thành bởi nhóm {$this->getName()}.</p>";
        }
        // Phương thức trả về số thành viên trong nhóm
        function getCount() {
            return count($this->_employees);
        }
    }
    
    /* Lớp Employee mở rộng từ lớp WorkUnit
     * Lớp không có thuộc tính và phương thức nào
     */
    class Employee extends WorkUnit {
        // Empty functions
        function add(Employee $e) {
            return false;
        }
        function remove(Employee $e) {
            return false;
        }

        // Thực hiện phương thức trìu tượng
        function assignTask($task) {
            $this->tasks[] = $task;
            echo "<p>Một tác vụ được gán cho {$this->getName()}. Tác vụ này phải được hoàn thành bởi một mình {$this->getName()}.</p>";
        }
        function completeTask($task) {
            $index = array_search($task, $this->tasks);
            unset($this->tasks[$index]);
            echo "<p>Nhiệm vụ '$task' được hoàn thành bởi {$this->getName()}. </p>";
        }
    
    }
    #------------ KẾT THÚC ĐỊNH NGHĨA CLASS ----------------------#

    // Tạo đối tượng
    $frontend = new Team('Frontend');
    $thong = new Employee('ThongNC');
    $chien = new Employee('ChienVM');
    $thao = new Employee('ThaoDV');

    // Gán nhân viên vào nhóm frontend
    $frontend->add($thong);
    $frontend->add($chien);
    $frontend->add($thao);

    // Gán các tác vụ cho nhóm và nhân viên
    $frontend->assignTask('Xây dựng website');
    $evan->assignTask('Xây dựng frontend');
    // Hoàn thành một tác vụ
    $frontend->completeTask('Xây dựng website');

    // Chuyển Taylor Otwell sang nhóm backend
    $frontend->remove($thao);

    // Xóa các đối tượng
    unset($frontend, $thong, $chien, $thao);
    ?>
</body>
</html>
```

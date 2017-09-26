# LisException class

#### 简介

``` php
final LisContainer {
	protected static string $_instance;
	protected string $message; 
	protected int $code;
	protected string $previous;
	
	public function __construct();
	public static function setExceptionHandler([$class => $action]);
}
```

#### 案例

``` php
定义ErrorController类
<?php 
class ErrorController {
	public static function handleAction($e) {
		var_dump($e);
	}
}
?>


<?php
class test {
    public $name;

    public function __construct() {
        echo "test \n";
    }
}
$test = new test();

\Lis\Application::setAppDirectory(dirname(__FILE__));
\Lis\Exception::setExceptionHandler(array("ErrorController", "handleAction"));
throw new Exception("Catch me twice", 1);

$app = new \Lis\Application();
var_dump(\Lis\Container::get());
var_dump(\Lis\Container::add("test", $test));
var_dump(\Lis\Container::get("test"));

?>

```

#### 输出



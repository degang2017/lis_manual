# LisContainer class

#### 简介

负责类的注入

``` php
final LisContainer {
	protected static string $_instance;
	protected static array $_container; 
	
	public function __construct($container = NULL);
	public static function get($name = NULL);
	public static function add($name, $obj);
}
```

#### 案例

``` php
<?php
class test {
    public $name;

    public function __construct() {
        echo "test \n";
    }
}
$test = new test();

\Lis\Application::setAppDirectory(dirname(__FILE__));
$app = new \Lis\Application();
var_dump(\Lis\Container::get());
var_dump(\Lis\Container::add("test", $test));
var_dump(\Lis\Container::get("test"));
$app->run();

?>

```

#### 输出

``` c

test
array(3) {
  ["config"]=>
  object(Lis_Config)#4 (0) {
  }
  ["exception"]=>
  object(Lis_Exception)#5 (8) {
    ["string":"Exception":private]=>
    string(0) ""
    ["file":protected]=>
    string(31) "/root/php-7.1.7/ext/lis/t/t.php"
    ["line":protected]=>
    int(13)
    ["trace":"Exception":private]=>
    array(2) {
      [0]=>
      array(4) {
        ["function"]=>
        string(11) "__construct"
        ["class"]=>
        string(13) "Lis\Container"
        ["type"]=>
        string(2) "->"
        ["args"]=>
        array(0) {
        }
      }
      [1]=>
      array(6) {
        ["file"]=>
        string(31) "/root/php-7.1.7/ext/lis/t/t.php"
        ["line"]=>
        int(13)
        ["function"]=>
        string(11) "__construct"
        ["class"]=>
        string(15) "Lis\Application"
        ["type"]=>
        string(2) "->"
        ["args"]=>
        array(1) {
          [0]=>
          string(25) "/root/php-7.1.7/ext/lis/t"
        }
      }
    }
    ["message":protected]=>
    NULL
    ["code":protected]=>
    int(0)
    ["previous":protected]=>
    NULL
    ["previous":"Exception":private]=>
    NULL
  }
  ["router"]=>
  object(Lis_Router)#6 (0) {
  }
}
bool(true)
object(test)#1 (1) {
  ["name"]=>
  NULL
}

```


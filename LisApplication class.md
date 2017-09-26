# LisApplication class

#### 简介

LisApplication 它负责请求、路由、执行、输出等。

``` php
final LisApplication {
	protected static string $_environ;
	protected bool $_running; 
	
	public function __construct([, $container = NULL ]);
	public function __get();
	public static function getEnviron([$name = NULL]);
	public static function setAppDirectory($path);
	public static function getAppDirectory();
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
$app = new \Lis\Application(['test' => $test]);
var_dump($app);
$environ = \Lis\Application::getEnviron();
$appDirectory = \Lis\Application::getAppDirectory();
echo LIS_VERSION."\n";
var_dump($environ, $test);

?>

```

#### 输出
``` c

test
object(Lis\Application)#2 (2) {
  ["_running":protected]=>
  bool(true)
  ["_environ":protected]=>
  string(7) "develop"
}
object(test)#1 (1) {
  ["name"]=>
  NULL
}
1.0.0
string(7) "develop"
object(test)#1 (1) {
  ["name"]=>
  NULL
}

```



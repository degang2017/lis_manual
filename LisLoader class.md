# LisLoader class

#### 简介

``` php
final LisLoader {
	protected static string $_instance;
	public static function import($path);
}
```

#### 案例

``` php
<?php
class Hello{
	public static function test(){
		echo "test";
	}
}
?>

<?php
\Lis\Application::setAppDirectory(dirname(__FILE__));
$app = new \Lis\Application();
\Lis\Loader::import(dirname(__FILE__)."/util/Hello.php");
Hello::test();
?>

```

#### 输出
``` c
test
```



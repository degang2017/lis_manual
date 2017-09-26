# LisConfig class

#### 简介

``` php
final LisConfig {
	protected static string $_instance;
	protected static array $_config; 
	
	public static function set($key, $val);
	public static function get($key); //db.slave.port
}
```

#### 案例

``` php
<?php
\Lis\Application::setAppDirectory(dirname(__FILE__));
$app = new \Lis\Application();
var_dump(\Lis\Config::set('db', [ 'user' => 'db1', 'passport' => '123']));
var_dump(\lis\Config::get('db'));
?>

```

#### 输出
``` c
bool(true)
array(2) {
	["user"]=>
		string(3) "db1"
	["passport"]=>
   string(3) "123"
}
```



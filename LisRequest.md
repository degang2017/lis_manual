# LisRequest class

#### 简介

``` php
final LisRequest {
	protected static string $_instance;
	public static function getMethod();
	public static function getBaseUri();
	public static function setBaseUri(string $baseUri); 
	public static function getQuery(string $name = NULL);
	public static function getPost(string $name = NULL);
	public static function getCookie(string $name = NULL);
	public static function getFiles(string $name = NULL);
	public static function getControllerName();
	public static function getActionName();
}
```

#### 案例

``` php
class HomeController {
	public static function indexAction() {
		echo "home_index";
		var_dump(\Lis\Request::getMethod());
		var_dump(\Lis\Request::getQuery());
		var_dump(\Lis\Request::getControllerName());
		var_dump(\Lis\Request::getActionName());
		}
}

\Lis\Application::setAppDirectory(dirname(__FILE__));
$app = new \Lis\Application();

\Lis\Request::setBaseUri('/user/33333/sex3333/33333/ewfwefre/name1/dsdssdds/reset-password');

var_dump(\Lis\Request::getMethod());

\Lis\Route::group('/user/{id_3-3:[0-9]+}/sex3333/{sex:[0-9]+}/ewfwefre',function(){
	\Lis\Route::cli('/name1/{name:[a-zA-Z]+}/reset-password', 'HomeController:indexAction');
});

$app->run();

```

#### 输出
``` c
string(3) "Cli"
home_indexstring(3) "Cli"
array(3) {
  ["id_3-3"]=>
  string(5) "33333"
  ["sex"]=>
  string(5) "33333"
  ["name"]=>
  string(8) "dsdssdds"
}
string(14) "HomeController"
string(11) "indexAction"
```







# LisRoute class

#### 简介

``` php
final LisRoute {
	protected static string $_instance;
	public static function group($rule, function(){});
	public static function get($rule, $action); 
	public static function post($rule, $action);
	public static function put($rule, $action);
	public static function patch($rule, $action);
	public static function delete($rule, $action);
	public static function options($rule, $action);
	public static function cli($rule, $action);
}
```

#### 案例

``` php
//library目录下
<?php
class Middle {
     public function test() {
 		    echo "middle test()";
 	   }
}

?>

<?php
\Lis\Application::setAppDirectory(dirname(__FILE__));
$app = new \Lis\Application();
\Lis\Route::get('/name2/{name:[a-zA-Z]+}/reset-password', 'HomeController:home');

\Lis\Route::group('/user/{id_3-3:[0-9]+}/age/{age:[0-9]+}/', function(){
	\Lis\Route::get('/name/{name:[a-zA-Z]+}/reset-password','HomeController:home');
}))->middleware('Middle:test');
$app->run();
?>

```






# LisView class

#### 简介

``` php
final LisView {
    protected static string $_instance;
    public static function assign($name, $val);
    public static function render(string $tpl, array $vars = NULL); 
}
```

#### 案例

```php
LisView::assign("var1", "hello test111");
LisView::render("index", ["var2" => "test2222"]);
```

#### 输出
``` c
 <html>
 <?php echo $var1; ?>
 <?php echo $var2; ?>
 <html>
```


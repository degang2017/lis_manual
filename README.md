# Lis 框架手册

Lis是一个C语言编写的PHP轻量级框架

# PHP版本

PHP 7.1.10 +

# 文件布局

``` 
+ public
  | - index.php
  | + css
  | + js
  | + img
+ conf
  | - application.php 
- application/
  + controller
     - IndexController.php 
  + view 
     |+ index   
        - index.php
  - library
  - model
  - plugin
```

## 目录
- [LisApplication](./LisApplication.md)
- [LisConfig](./LisConfig.md)
- [LisContainer](./LisContainer.md)
- [LisException](./LisException.md)
- [LisLoader](./LisLoader.md)
- [LisRequest](./LisRequest.md)
- [LisRoute](./LisRoute.md)
- [LisView](./LisView.md)



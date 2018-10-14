---
layout:     post
title:      "Ecshop二次开发：升级至5.6"
subtitle:   " \"修改ecshop使之可以使用php5.6\""
date:       2018-10-11 20:34:00
author:     "Bin"
header-img: "img/post/bg/ecshop.jpg"
catalog: true
tags:
    - Ecshop
---

> “I like coding. ”


### 1. perg_replace()

####错误
```php
Deprecated: preg_replace(): The /e modifier is deprecated, use preg_replace_callback instead in cls_template.php
```
出现以上问题是preg_replace()函数中用到的修饰符/e在PHP5.5.x中已经被弃用了。在PHP5.5以上的版本用preg_replace_callback函数替换了preg_replace函数。

####解决方法

```php
return preg_replace("/{([^\}\{\n]*)}/e", "\$this->select('\\1');", $source); 
```
替换为
```php
return preg_replace_callback("/{([^\}\{\n]*)}/", function($r) { return $this->select($r[1]); }, $source);
```

####位置
```bash
cls_template.php 300
cls_template.php 493
cls_template.php 552
cls_template.php 1090
```

### 2. array_shift()

####错误
```php
Strict Standards: Only variables should be passed by reference 
```
出现这个问题的原因，貌似在php5.4中array_shift只能为变量，不能是函数返回值。

####解决方法

```php
$tag_sel = array_shift(explode(‘ ‘, $tag));
```
替换为
```php
$tag_arr = explode(‘ ‘, $tag);
$tag_sel = array_shift($tag_arr);
```

####位置
```bash
cls_template.php 423
cls_template.php 1090
lib_main.php 1330
lib_base.php 1229
admin/flashplay.php 131
admin/flashplay.php 183
```

### 3. cls_image::gd_version()

####错误
```php
Strict Standards: Non-static method cls_image::gd_version() should not be called statically  
```
如问题中提示的一样，因为 cls_image.php 中 gd_version() 不是 static 函数

####解决方法

```php
return cls_image::gd_version();
```
替换为
```php
$cls_image = new cls_image();
return $cls_image->gd_version();
```
####位置
```bash
lib_base.php 346
```

### 4. =&

####错误
```php
Deprecated: Assigning the return value of new by reference is deprecated 
```
PHP5.3+废除了”=&”符号，对象复制用”=”

####解决方法

=& 替换为 =


### 5. mktime()

####错误
```php
Strict Standards: mktime(): You should be using the time() function instead
```
mktime()方法不带参数被调用时，会被抛出一个报错提示。

####解决方法

```php
$auth = mktime();
```
替换为
```php
$auth = time();
```

####位置
```bash
admin\shop_config.php 32
sms_uri.php 31
```

### 6. __construct()

####错误

```php
Strict Standards: Redefining already defined constructor for class cls_sql_dump
```
PHP早期版本是使用跟类同名的函数作为构造函数，后来又出现了使用 __construct()作为构造函数

####解决方法

把__construct()函数放在，同名函数上面就行了。


### 7. vbb::set_cookie()

####错误
```php
Strict Standards: Declaration of vbb::set_cookie() should be compatible with integrate::set_cookie($username = '', $remember = NULL)
```
vbb继承了integrate类并且重写了 set_cookie() 函数，但vbb重写set_cookie函数的参数 与 其父类set_cookie 的参数不符所以出现以上问题

####解决方法

```php
function set_cookie ($username="");
```
替换为
```php
function set_cookie ($username="", $remember = NULL);
```

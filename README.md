# YT - Yaf Thinkphp Framework 
[![Build Status](https://secure.travis-ci.org/laruence/yaf.png)](https://github.com/laruence/yaf)

YT 框架是用c扩展构建的php框架，基于[Laruence的yaf框架](https://github.com/laruence/yaf)修改版，主要适配了thinkphp框架的一些目录结构和使用习惯。
与yaf框架的主要不同之处：
* 框架目录结构与thinkphp基本相同
* 去除控制器和行为的Controller和Action后缀，name_suffix配置无效;
* 默认开启use_namespace，use_spl_autoload;
* 应用目录下所有类的命名空间必须 `app\` 开头;
* 默认模块控制器命名空间为`app\controllers`，自定义模块控制器命名空间为 `app\[Module]\controllers` ;

默认模块控制器示例：
```php
<?php

namespace app\controllers;     

use think\Controller;
class Index extends Controller
{
    public function index()    
    { 
        echo 'hello';          
    }
}
```

自定义api模块控制器示例：

```php
<?php

namespace app\api\controllers;

use think\Controller;
class Api extends Controller
{
    public function index()
    {   
        echo 'hello';
    }
}
```

## Requirement
- PHP 7.0+  (master branch))

### Rewrite rules

#### Apache

```conf
#.htaccess
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule .* index.php
```

#### Nginx

```
server {
  listen ****;
  server_name  domain.com;
  root   document_root;
  index  index.php index.html index.htm;
 
  if (!-e $request_filename) {
    rewrite ^/(.*)  /index.php/$1 last;
  }
}
```

#### Lighttpd

```
$HTTP["host"] =~ "(www.)?domain.com$" {
  url.rewrite = (
     "^/(.+)/?$"  => "/index.php/$1",
  )
}
```

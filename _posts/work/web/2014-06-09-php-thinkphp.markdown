---
layout:     post
title:      "thinkphp"
subtitle:   " \"thinkphp\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
---

# thinkphp

```
git clone https://github.com/top-think/think tp5
cd tp5
git clone https://github.com/top-think/framework thinkphp
cd public
php -S localhost:8888 router.php
```


```
D('User')
M('User')
A(ction)
L(anguage)
C(onfig)
S(session)
F(ast)
I(nput)
U(rl)

开启页面调试功能
'SHOW_PAGE_TRACE' => true,

// 定义公共错误模板，View/Public/error.html
'TMPL_EXCEPTION_FILE' => 'Public:error', 
// 默认错误跳转对应的模板文件
'TMPL_ACTION_ERROR' => 'Public:error', 
//成功页面
'TMPL_ACTION_SUCCESS' => 'Public:success', 



```
# examples

- [framework](https://github.com/top-think)
- [wstmall](https://github.com/wstmall/wstmall)


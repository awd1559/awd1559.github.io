---
layout:     post
title:      "javascript"
subtitle:   " \"javascript\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: lang
permalink: /lang/javascript
tags:
    - lang
---
> - [web front目录](/web/front)





# javascript

#### var/const/let

> - ES6 add let
> - 作用域只在所在块中有效，没有变量提升，声明后才可使用，相同作用域中不可重复声明
> - 尽量使用let，不使用var
> - 
> - 立即执行函数(IIFE)(function () { var tmp = ...;  ... }()); 不再使用
> - { let tmp = ...; ... } 可代替IIFE
> - 
> - const 常量


> - ES6 解构(Destructuring)

```
var [a, b, c] = [1, 2, 3];  //let will ERROR
var [,,third] = ["foo", "bar", "baz"];  //third = "baz"
var [head, ...tail] = [1, 2, 3, 4];     //head = 1, tail = [2, 3, 4]

let { foo, bar } = { foo: "aaa", bar: "bbb" };
```

#### string 
> - ES6 support codepoing > 0xFFFF

```
//when codepoing > 0xFFFF, use fromCodePoint
String.fromCharCode(0x20BB7)    // => return 0x0BB7
String.fromCodePoint(0x20BB7)   

\uxxxx shows unicode, ranged between \u0000——\uFFFF
\u{20BB7}   //Unicode 0x20BB7, since ES6


//RE
/\u{61}/.test('a') // false
/\u{61}/u.test('a') // true
/^.$/.test('𠮷') // false
/\u{20BB7}/u.test('𠮷') // true , codepoint = 0x20BB7
```


#### binary

```
0b111110111 === 503 // true,
0o767 === 503 // true
```

> - Number

```
isFinite(25) // true
isFinite("25") // true
Number.isFinite(25) // true
Number.isFinite("25") // false

isNaN(NaN) // true
isNaN("NaN") // true
Number.isNaN(NaN) // true
Number.isNaN("NaN") // false

// ES5
parseInt("12.34") // 12
parseFloat('123.45#') // 123.45

// ES6
Number.parseInt("12.34") // 12
Number.parseFloat('123.45#') // 123.45
```

#### Array

```
//from()函数转换两类对象到数组：类似数组的对象（array-like object）和可遍历（iterable）的对象
let ps = document.querySelectorAll('p');

Array.from(ps).forEach(function (p) {
  console.log(p);
});


Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);



//Array.of()方法用于将一组值，转换为数组
Array.of(3, 11, 8) // [3,11,8]
Array.of(3).length // 1



//find
[1, 5, 10, 15].find(function(value, index, arr) {
    return value > 9;
}) // 10

//findIndex
[1, 5, 10, 15].findIndex(function(value, index, arr) {
    return value > 9;
}) // 2






//entries()，keys()和values()
for (let key of ['a', 'b'].keys()) {}

for (let value of ['a', 'b'].values()) {console.log(elem);}

for (let [key, value] of ['a', 'b'].entries()) {}


///
var a1 = [1, 2, 3, 4];
var a2 = [for (i of a1) i * 2];

a2 // [2, 4, 6, 8]
```







#### function

> - argument default value

```
//ES6
function log(x, y = 'World') {}

//ES5
function log(x, y) {
  y = y || 'World';
}
```


> - rest arguments

```
function push(array, ...items) { 
  items.forEach(function(item) {
    array.push(item);
    console.log(item);
  });
}

var a = [];
push(a, 1, 2, 3)            //将1,2,3打包到items Array中


function f(a, ...b, c){}   //ERROR
```




> - spread
> - 与rest正好相反

```
function add(x, y) {
  return x + y;
}
var numbers = [4, 38];
add(...numbers)         //将Array numbers拆包到[x,y]中
```

> - 只要具有Iterator接口的对象，比如Map，都可以使用spread

```
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let arr = [...map.keys()]; // [1, 2, 3]

//Generator
var go = function*(){
  yield 1;
  yield 2;
  yield 3;
};

[...go()] 
```



> - => function

```
var f = () = > {}       //基本语法
var f = (v) => {return v+1}    //可省略：var f = v => v + 1 

//如果返回对象，使用()，否则有歧义
var getTempItem = id => ({ id: id, name: "Temp" });
```







#### Set/Map

```
var items = new Set([1, 2, 3, 4, 5]);

var s = new Set();

for (i of s) {console.log(i)}

s.foreach((v,k) => v*2)
```

> - size
> - add(value)
> - delete(value)
> - has(value)
> - clear()



```
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
```

> - size
> - has(key)
> - get(key)
> - set(key, value)
> - delete(key)
> - clear





#### Generator/Promise
> - callback hell

```
fs.readFile(fileA, function (err, data) {
  fs.readFile(fileB, function (err, data) {
    // ...
  });
});
```

> - Promise
> - change the way to write callbacks
> - too much thens

```
var readFile = require('fs-readfile-promise');

readFile(fileA)
.then(function(data){
  console.log(data.toString());
})
.then(function(){
  return readFile(fileB);
})
.then(function(data){
  console.log(data.toString());
})
.catch(function(err) {
  console.log(err);
});
```



> - Generator
> - 异步任务的容器，用yield标明要暂停执行的地方

```
function* gen(x){
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }
```








#### Object

```
// ES6
class Lecture {
  constructor(name, teacher) {
    this.name = name;
    this.teacher = teacher;
  }
  display() {
    ...
  }
}
var l = new Lecture("cs", "wang");
l.display();

//继承
class ColorPoint extends Point {}
```






```
// ES5
function Lecture(name, teacher){
	this.name = name;
	this.teacher = teacher;
}
Lecture.prototype.display = function(){};

//继承
User.property = new Person();




//literal object
var myobj = {
  id:"",
  name: {
    firstName: 'Brendan',
    lastName: 'Eich'
  },
  init:function(){},
  doSomething: function(){}
};




//1
var obj = new Object();
obj.val = 5;

//2
function User(name){ this.name = name;}
var me = new User(“awd”);

//3
function User(){}
var me = new User();
var you = new me.constructor();
```



#### Module


> - ES6

```
//profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};

//main.js
import {firstName, lastName, year} from './profile';


//2
export default const str = 'message'
import str from './message'
```


> - CommonJS
> - Server Node.js, Browserify use CommonJS

```
//1
//profile.js
exports.firstName = 'Michael';
exports.lastName = 'Jackson';
exports.year = 1958;

//2
//prifile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958; 
module.exports = {firstName, lastName, year}

//main.js
var profile = require('./profile')
console.log(profile.year)

let {firstName, lastName, year} = require('./profile')
console.log(year)
```






> - AMD
> - [RequireJS](http://requirejs.org/) use AMD

```
define(['./MyModule.js'], function (MyModule) { });

```






#### 命名空间

```
//创建默认全局命名空间
var YAHOO = {};
//设置子命名空间
YAHOO.util = {};

//创建最终命名空间
YAHOO.util.Event = {
	addEventListener: function() {}
};

//调用函数
YAHOO.util.Event.addEventListener();
```



#### map/reduce, filter, sort

```
var arr = [1, 3, 5, 7, 9];

let result = arr.map(x => x*x); //[1, 9, 25, 49, 81]

let result = arr.reduce((x,y) => {return x+y}); //25

arr.filter((x) => {return x % 2 !== 0})
```


#### call/apply/bind

```
function changeColor(color){
  this.style.color = color;
}
changeColor(“white”); //= window.changeColor;  this == window

const main = document.getElementById(“main”);
changeColor.call(main, “black”);    //=main.changeColor(); this == main
```




# jquery

#### basic

```
$(document).ready(function() {});
//简写
$().ready(function() {});
$(function(){});



(function(wp, $){
  … ...
})(wp, jQuery);
```

#### extensions

```
jQuery.extend = jQuery.fn.extend = function(){};
jQuery.extend($.extend) 和jQuery.fn.extend($.fn.extend)是同一个函数 
jQuery库中，有些方法是通过调用jQuery.extend，有些是通过jQuery.fn.extend

jQuery.extend中，typeof jQuery = "function"
jQuery.extend相当于为function类添加静态方法extend
jQuery被赋值给$，所以可以使用$.extend()
```

```
使用$.extend,  扩展自定义的对象
var myself = {name: "jack"};
$.extend(myself, {
  setName:function(n){this.name = n;}
});
myself.setName("tom");  //使用
```

//扩展全局函数

```
//jQuery扩展全局函数
jQuery.foo = function(){};
$.foo();  //使用

//全局函数
$.extend({
  foo:function(){},
  bar:function(){}
});
$.foo(); $.bar()  //使用

//封装到awd对象中
$.awd = {
foo:function() {},
bar:function() {}
};
$.awd.foo();
$.awd.bar();



//添加jQuery对象方法
$.fn.xyz = function(){
  this.text("sss");
};
$('div').xyz();
$('#message').xyz();
```


```
1类级别的插件开发
1.1定义一个全局函数
jQuery.foo = function(){}
1.2使用extend定义全局函数 
jQuery.extend({
  foo:function(){},
  bar:function(){}
});


1.3使用命名空间定义函数
jQuery.plugin = {
  foo:function(){}
}

$(function(){
  $.foo();
});


2对象级别的插件开发
(function($){
  $.fn.extend({
    foo3:function() {
      alert('对象级别插件extend方式1');
    },
    bar3:function() {
      alert('对象级别插件extend方式2');
    }
  })
})(jQuery);

(function($){
  $.fn.foo4 = function() {
    alert('对象级别插件fn方式');
  }
})(jQuery);



//接收参数来控制插件的行为
(function($){
$.fn.bar4 = function(options) {
var defaults = {aaa:'1',bbb:'2'};
var opts = $.extend(defaults, options);
alert('参数值:aaa:'+opts.aaa+';bbb:'+opts.bbb);
}
})(jQuery);

//提供公有方法访问插件的配置项值
(function($){
$.fn.foo5 = function(options) {    
var opts = $.extend({}, $.fn.foo5.defaults, options);
alert('参数值:aaa:'+opts.aaa+';bbb:'+opts.bbb);
}
$.fn.foo5.defaults = {aaa:'1',bbb:'2'};
})(jQuery);

//提供公有方法来访问插件中其他的方法
(function($){
$.fn.bar5 = function(options) {
$.fn.bar5.alert(options);
}
$.fn.bar5.alert = function(params) {
alert(params);
}
})(jQuery);
```




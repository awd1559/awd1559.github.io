---
layout:     post
title:      "javascript"
subtitle:   " \"javascript\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - js
---

# framework

#### [angularjs](https://angularjs.org/)
[source code on github](https://github.com/angular/angular.js)
[angular.io](https://github.com/angular/angular.io) site for Angular 2 documentation
[doc](http://docs.angularjs.cn/api)

#### [backbone](http://backbonejs.org/)
[source code on github](https://github.com/jashkenas/backbone)

#### [emberjs](http://emberjs.com/)
[source code on github](https://github.com/emberjs/ember.js)

#### [jquery](https://jquery.com/)
[source code on github](https://github.com/jquery/jquery)

#### [meteor](https://www.meteor.com/)
[source code on github](https://github.com/meteor/meteor/)

	//install
	curl https://install.meteor.com | /bin/sh
	//create project
	meteor create <name>
	meteor add tabs:bootstrap

#### [ionic2](http://ionicframework.com)
[github](https://github.com/driftyco/ionic)

	Apache cordova: javascript api to access device's camera, mic, etc
	Angularjs
	support html5, iOS 8, Android 4.1, Windows 10

```
#install 
npm install -g cordova ionic

#创建项目
ionic start myApp
ionic start myApp blank
ionic start myApp tabs
ionic start myApp sidemenu

cd myApp
ionic platform add ios
ionic build ios
ionic emulate ios

ionic platform add android
ionic build android
ionic emulate android
```


#### [react](https://facebook.github.io/react/)
[source code on github](https://github.com/facebook/react)

#### [spine](http://spinejs.com/)
[source code on github](https://github.com/spine)

	Lightweight MVC library


#### [egret](http://www.egret.com/)
[source code on github](https://github.com/egret-labs)
html5 game engine
创建项目
egret create HelloWorld
创建HelloWorld目录到当前目录

编译项目
egret build HelloWorld
编译HelloWorld目录中的项目

运行项目
egret startserver HelloWorld
自动打开http://localhost:3000/HelloWorld/launcher/index.html

将bin-debug、launcher、resources文件夹HTTP服务器的根目录下即可运行

使用WebStore作为IDE，打开目录即可编辑TypeScript

# library

#### [moment](http://momentjs.com/)
[source code on github](https://github.com/moment/moment/)
	Parse, validate, manipulate, and display dates in JavaScript

#### [PhotoSwipe](http://photoswipe.com/)
[source code on github](https://github.com/dimsemenov/PhotoSwipe)

#### [raphael](http://raphaeljs.com/)
[source code on github](https://github.com/DmitryBaranovskiy/raphael)

	Vector Library

#### [threejs](http://threejs.org/)
[source code on github](https://github.com/mrdoob/three.js/)

	javascript 3d library

#### [video-js](http://videojs.com/)
[source code on github](https://github.com/videojs/video.js)
	the html5 player framework

#### [d3](https://d3js.org/)
[source code on github](https://github.com/mbostock/d3)

	data chart

#### [DataTables](https://datatables.net/)



# 浏览器对象

#### web函数
window
history
	history.go(-2)
	history.go(3)
location
	location.replace(“http://www.baidu.com”);
	location.href=“myPage.html"
navigator
screen
document
var time = new Date();
time.toUTCString();
time.toLocaleString();
time.getTimezoneOffset();
time.toLocaleTimeString();
time.toTimeString();
time.toLocaleDateString();
time.toDAteString();

#### Dom函数



#### lambda函数、匿名函数
$(document).ready(function() {   …   });





#### call方式
function changeColor(color){
	this.style.color = color;
}
changeColor(“white”);	//= window.changeColor;  this == window

var main = document.getElementById(“main”);
changeColor.call(main, “black”);		//=main.changeColor(); this == main


#### 面向对象
function Lecture(name, teacher){
	this.name = name;
	this.teacher = teacher;
}
Lecture.prototype.display = function(){};





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



#### 继承
User.property = new Person();


#### 命名空间
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

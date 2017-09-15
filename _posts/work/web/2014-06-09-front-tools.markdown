---
layout:     post
title:      "front tools"
subtitle:   " \"front tools\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: web
permalink: /web/tools
tags:
    - web
---
> - [web front目录](/web/front)

# tools

##### [Bower](http://bower.io/)
> - package manager for web frontend module
> - [packages](http://bower.io/search/)

> - install 
```
npm install -g bower 
```

> - usage

```
bower install bootstrap #download bootstrap to directory: bower_components

bower search [package]
bower install [package]
bower uninstall [package]
bower update [package]
bower list        //list package hierarchy in directory: bower_components

bower help
bower init        //create a simple bower.json
```


> - bower.json
```
bower init #create a simple bower.json
bower install #install dependencies in bower.json
```







#### [yeoman](http://yeoman.io)
> - framework tool for web dev

> - install
```
npm install -g yo
#yo depends on bower, grunt, gulp
npm install -g bower grunt-cli gulp
```

> - generators
```
#install generator
npm install -g generator-webapp
npm install -g generator-angular
npm install -g generator-gulp-webapp
```

[generators](http://yeoman.io/generators/)

- gulp-angular
- gulp-webapp
- mobile
- webapp
- angular
- angular-fullstack
- react-fullstack


> - usage

```
//bootstrap, sass, modernizr
yo webapp  #use grunt
yo gulp-webapp  #use gulp

//sass, bootstrap, grunt
yo angular
yo angular —coffee
yo angular:controller myController
yo angular:directive myDirective
yo angular:filter myFilter
yo angular:service myService
```






















#### [gulp](http://gulpjs.com/)
> - [中文](http://www.gulpjs.com.cn/)

> - install

```
npm -g install gulp
npm -g install gulp-cli
#install to directory: node_modules/gulp
npm install gulp

npm init
npm install --save-dev gulp #save "devDependencies" in file package.json
```

> - gulpfile.js

```
var gulp = require('gulp');

gulp.task('default', function() {
  // place code for your default task here
});
gulp.task('styles', ['default'], function() {  
  return gulp.src('src/styles/main.scss')
    .pipe(sass({ style: 'expanded' }))
    .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
    .pipe(gulp.dest('dist/assets/css'))
    .pipe(rename({suffix: '.min'}))
    .pipe(minifycss())
    .pipe(gulp.dest('dist/assets/css'))
    .pipe(notify({ message: 'Styles task complete' }));
});

```

run the task

>gulp           #run default task
>gulp --task    #list task hierarchy


> - [plugin](http://gulpjs.com/plugins/)

- 编译sass  gulp-ruby-sass
- Autoprefix: gulp-autoprefixer
- 压缩css gulp-minify-css
- JSHint    gulp-jshint
- 拼接    gulp-concat
- 丑化    gulp-uglify
- 图片压缩  gulp-imagemin
- live reload gulp-livereload
    gulp-cache    只有修改过的图片会进行压缩
    gulp-notify
    gulp-sourcemaps
























#### [grunt](http://www.gruntjs.net)

> - install

```
npm install -g grunt-cli
npm install -g grunt

npm install --save-dev grunt 
```

> - scripts

```
var gulp = require('gulp');
var sass =  require('gulp-ruby-sass');

gulp.task('sass', function(){
  return sass('source/file.scss').on('error', sass.logError)
    .pipe(gulp.dest())
});
```


> - Gruntfile
Gruntfile.js or Gruntfile.coffee

```
'use strict';
module.exports = function(grunt) {
  grunt.initConfig({
    clean: {
      src: ['dist']
    },
    uglify: {
      options: {
        banner: '<%= banner %>'
      },
      dist: {
        src: '<%= concat.dist.dest %>',dest: 'dist/ba-<%= pkg.name %>.min.js'
      },
    }
  })
}
```

```
//到项目grunt项目的根目录：
npm install  //安装依赖项目， 根据package.json(必须有内容)
grunt
grunt serve
```




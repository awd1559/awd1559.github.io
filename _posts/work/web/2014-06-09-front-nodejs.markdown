---
layout:     post
title:      "Node.js"
subtitle:   " \"Node.js\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: web
permalink: /web/nodejs
tags:
    - web
---
> - [web front目录](/web/front)


# [Node.js](https://nodejs.org/)
> - brew install nodejs
> - download installer from [Node.js](https://nodejs.org/)
> - [npm](https://www.npmjs.com) included
> - [awesome-nodejs](https://github.com/sindresorhus/awesome-nodejs)


#### working in webstorm

- Edit Configration -> Node.js
- Node interpreter: usr/local/bin/node
- JavaScript file:  bin/www

```
npm install -g supervisor #monitor node code changes
supervisor app.js

//better use yomen
//and now we have dva

change jade template files will refresh on browser
```

#### usage
```
npm init #init package.json file
npm -l #display the npm command full usage
npm <cmd> -h #display the npm <cmd> help info

npm install [package] #install package to directory<node_modules>
npm update [package]
npm uninstall [package]<version>
npm view [package]

npm publish <tagball>
npm publish <folder>

npm start
npm stop

npm list #list package in directory: node_modules
npm version

npm install #install packages in package.json 
```


```
//yarn is good
//yarn use package.json as npm
yarn init         #init package.json file
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
yarn remove [package]
yarn update [package]
yarn install
```




# packages


#### babel    
> - translation

```
npm i -g babel-cli
npm i --save-dev babel-core
npm i --save-dev babel-eslint
npm i --save-dev babel-loader
npm i --save-dev babel-preset-react
npm i --save-dev babel-preset-es2015
npm i --save-dev babel-preset-stage-0 
```

```
//.babelrc
{
  "presets": ["react", "es2015", "state-0"],
  "plugins": []
}
```

```
babel index.js   //output to std output
```











##### webpack
> - user Loaders to extract resources, package to one or multi-part static resources
> - yard add webpack


```
//use default config file
//package entry.js and all its used resources into build/bundle.js
//webpack.config.js
var path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'entry.js'),
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
    }
};
```



```
//webpack.config.js
var webpack = require('webpack');

module.exports = {
    entry: __dirname + "/app/main.js",
    output: {
      path: __dirname + "/build",
      filename: "bundle.js"
    },
    resolve: {
      extensions: ["", ".js", ".jsx", ".jade"]
    },

    module: {
      loaders: [
        { 
          test: /\.jade$/, 
          loader: "jade" 
        }
      ]
    },
    plugins: [
      new webpack.BannerPlugin('This file is created by awd')
    ]
};
```

```
//see progress with colors
webpack --progress --colors
//and watch files changes   
webpack --progress --colors --watch
npm i -g webpack-dev-server
webpack-dev-server --progress --colors
```


#### webpack-loaders

> - css-loader

```
yarn add style-loader css-loader --dev
{
  test:/\.css$/,
  loaders:['style','css'],    //loader: 'style!css'
  exclude:'node_modules'
}
```

> - less-loader

```
yarn add less-loader --dev
{
  test: /\.less$/,
  loader: 'style!css!less'
}
```

> - sass-loader

```
yarn add sass-loader --dev
{
  test: /\.scss$/,
  loader: 'style!css!sass'
}
```



> - url-loader

```
yarn add url-loader --dev
{
  test: /\.(png|jpg)$/,
  loader: 'url?limit=25000'
}
//小于25000的png|jpg文件，转为BASE64，存储在css中
```



> - reactjs jsx loader

```
yarn add react react-dom --dev
yarn add babel-loader --dev
yarn add babel-preset-es2015 --dev
yarn add babel-preset-react --dev

//webpack.config.js
resolve: {
    extensions: ['.js', '.jsx']
},
module: {
  loaders: [{
    test:/\.js|jsx$/,
    loaders:['babel-loader?presets[]=es2015&presets[]=react'],
    exclude:"/node_modules/"
  }]
}
```



> - Plugins

```
npm install html-webpack-plugin

new HtmlWebpackPlugin()

new HtmlWebpackPlugin({//根据模板插入css/js等生成最终HTML
  favicon:'./src/img/favicon.ico', //favicon路径
  filename:'/view/index.html',    //生成的html存放路径，相对于 path
  template:'./src/view/index.html',    //html模板路径
  inject:true,    //允许插件修改哪些内容，包括head与body
  hash:true,    //为静态资源生成hash值
  minify:{    //压缩HTML文件
    removeComments:true,    //移除HTML中的注释
    collapseWhitespace:true    //删除空白符与换行符
  }
})
```

```
new webpack.optimize.UglifyJsPlugin({    //压缩代码
    compress: {
        warnings: false
    },
    except: ['$super', '$', 'exports', 'require']    //排除关键字
}),
```

> - webpack-dev-server

```
npm install webpack-dev-server --save-dev

//package.json
"dev": "webpack-dev-server --devtool eval --progress --colors --hot --content-base build"

npm run dev   //localhost:8080

```


















#### express

```
npm i -g express
npm i -g express-generator
express test_express               //create project
cd test_express
npm install
npm start
```

```
var app = express();

//设置模版引擎
app.set('views', path.join(__dirname, 'views'))
app.set(‘view engine’, ‘html’);
app.set(‘view engine’, ‘ejs’);
app.set(‘view engine’, ‘jade’);


//路由 
app.get(‘/’, routes.index);
app.get(‘/login’, routes.login);
app.post(‘/login’, routes.doLogout);

/ab?cd    匹配abcd, acd，0个或1个b字符
/ab+cd    至少一个b
/ab*cd    0个或多个各种字符


//使用名称
var index = require('./routes/index');
app.use('/', index);

//routes/index.js
var express = require('express');
var router = express.Router();
router.get('/', function(req, res, next){
  res.render('index', {title:'传过去值'});
});


//res方法
res.download()
res.end()
res.jsoin()
res.jsonp()
res.redirect()
res.send()
res.sendFile()
res.sendStatus()
```






#### koa

//supervisor
- nodejs 代码修改后必须重新启动才可以看到修改结果
- supervisor可以在修改代码后自动重启
- npm install -g supervisor
- 使用supervisor app.js 启动服务器
- 会遇到supervisor不停重启的错误问题





# Component
> - see [awesome-nodejs](https://github.com/sindresorhus/awesome-nodejs)


#### dialog

[vodal](https://github.com/chenjiahan/vodal)

```
npm i -S vodal

App.vue
@import "../../node_modules/vodal/common.css";
@import "../../node_modules/vodal/door.css";
@import "../../node_modules/vodal/flip.css";
@import "../../node_modules/vodal/rotate.css";
@import "../../node_modules/vodal/slide-down.css";
@import "../../node_modules/vodal/slide-left.css";
@import "../../node_modules/vodal/slide-right.css";
@import "../../node_modules/vodal/slide-up.css";
@import "../../node_modules/vodal/zoom.css";
```








#### markdown

> - [vue-markdown](https://github.com/miaolz123/vue-markdown)

```
npm install --save vue-markdown

import VueMarkdown from 'vue-markdown'

new Vue({
  components: {
    VueMarkdown
  }
})
```


> - [mavonEditor](https://github.com/hinesboy/mavonEditor)

```
npm install mavon-editor --save

import Vue from 'vue'
import mavonEditor from 'mavon-editor'
import 'mavon-editor/dist/css/index.css'

Vue.use(mavonEditor)
```







# DataBase

#### ORM
> - [mongoose](https://github.com/Automattic/mongoose)
MongoDB

> - [sequelize](https://github.com/sequelize/sequelize)
PostgreSQL, SQLite, MySQL, MSSQL

```
npm install --save sequelize
npm install --save sqlite3
```




#### Query

> -[Knex](http://knexjs.org/)
MySQL
PostgreSQL
SQLite3
Oracle
MSSQL

just query

```
npm install knex --save
npm install sqlite3
```

#### Other

> - [NeDB](https://github.com/louischatriot/nedb)

```
npm install nedb --save 
```


> - [Lowdb](https://github.com/typicode/lowdb)
json file database

```
npm install lowdb --save
```





# HTTP
> - [axios](https://github.com/mzabriskie/axios)
promise Http client

```
npm install axios --save
```



> - [request](https://github.com/request/request)
Simplified HTTP request client




# spider
> - [node-crawler](https://github.com/bda-research/node-crawler)

```
npm install crawler
```






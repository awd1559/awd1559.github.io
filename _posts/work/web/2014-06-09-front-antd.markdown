---
layout:     post
title:      "antd"
subtitle:   " \"web front antd\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: web
permalink: /web/antd
tags:
    - web
---
> - [web front目录](/web/front)



- [antd](http://ant.design/)
- [github](https://github.com/ant-design/ant-design)

```
//dva
npm install dva-cli
dva new myapp
cd myapp
npm i antd --save
npm i antd-mobile --save
npm i babel-plugin-import --save-dev
npm start
```

```
//antd-init, not a good idea
npm install -g antd
npm install -g antd-init
mkdir example && cd example
antd-init
npm start
npm run build
```

自定义主题
```
//dva
//.roadhogrc
"extraBabelPlugins":
["dva-hmr","transform-runtime", 
  ["import", { "libraryName": "antd", "style": "css" }]
]

"theme": {
  "primary-color": "#1DA57A",
},

"theme": "./theme.js",


//antd-int
//package.json
"theme": {
  "primary-color": "#1DA57A",
},
"theme": "./theme.js",

//theme.js
module.exports = () => {
  return {
    'primary-color': '#1DA57A',
    'link-color': '#1DA57A',
    'border-radius-base': '2px',
  };
};
```





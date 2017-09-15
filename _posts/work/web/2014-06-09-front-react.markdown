---
layout:     post
title:      "react"
subtitle:   " \"web front react\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: web
permalink: /web/react
tags:
    - web
---
> - [web front目录](/web/front)




# [react](https://facebook.github.io/react/)
- [source code on github](https://github.com/facebook/react)

#### start kit

> - [dva](https://github.com/dvajs/dva)
> - redux + react-router + redux-saga 
> - is the best way to start a react+redux application
> - auto load
> - support TypeScript
```
npm install dva-cli
dva new myapp
cd myapp
npm start
```


> - [create-react-app](https://github.com/facebookincubator/create-react-app)
> - used in intellij IDEA

```
npm install -g create-react-app
create-react-app hello-world
npm start
npm run build
```

> - webpack 

```
//reactjs jsx loader
yarn add react react-dom
yarn add babel-core babel-loader --dev
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

```
//app.js
import React, { Component } from 'react'
import { render } from 'react-dom'
import HelloMessage from './hello.js'

render(<HelloMessage name="John" />, document.getElementById('root'));

//hello.js
import React, { Component } from 'react';
class HelloMessage extends Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

module.exports = HelloMessage  //ok
export default HelloMessage    //ok
```

```
//html
<html>
<head>
  <title>webpack+react</title>
</head>
<body>
  <div id="root"></div>
<script type="text/javascript" src="bundle.js"></script>
</body>
</html>
```

> - ~~and the obsoleted~~
> - [~~react-starter-kit~~](https://github.com/kriasoft/react-starter-kit)
```
git clone -o react-starter-kit -b master --single-branch https://github.com/kriasoft/react-starter-kit.git MyApp
cd MyApp
npm install
npm start
```

> - ~~and the obsoleted~~
> - [~~react-aspnet-boilerplate~~](https://github.com/pauldotknopf/react-aspnet-boilerplate)
```
npm install -g generator-react-aspnet-boilerplate
yo react-aspnet-boilerplate
yo react-aspnet-boilerplate:empty-template
cd src/React
npm install
gulp
dotnet restore
dotnet ef database update
dotnet run
```


#### React
> - React四大概念：
> - Component
> - JSX：
    实现了Component，封装了HTML
    JSX最终被编译为js内容，如：
    <a href="http://facebook.github.io/react/">Hello!</a>
    直接使用js就是：
    React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello!')

> - VDOM：提升操作DOM的性能
> - Data Flow：单项数据绑定



> - Redux:事件流
> - component -> action -> reducer -> state -> component

#### IDEA

```
npm install create-react-app

newproject -> React App
create-react-app:C:\Users\awd\AppData\Roaming\npm\node_modules\create-react-app
run config -> npm 
command:run
script: start
```











#### basic useage 

```
// 1. 传统写法
const App = React.createClass({});

// 2. es6 的写法
import React, { Component } from 'antd'
class App extends Component{
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

// 3. stateless 的写法（antd推荐的写法）
const App = (props) => ({});
```



```
<script src="react.js"></script>
<script src="react-dom.js"></script>
<script src="browser.min.js"></script>
<script type="text/babel">
  var App = React.createClass({
    getInitialState: function () {
      return { count: 0 };
    },
    getDefaultProps: function() {

    },
    componentWillMount: function() {

    },
    componentDidMount: function() {

    },
    handleClick: function () {
      this.setState({
        count: this.state.count + 1,
      });
    },
    render: function () {
      return (
        <button onClick={this.handleClick}>
          clicks: {this.state.count}
        </button>
      );
    }
  });
  ReactDOM.render(
    <App />, document.getElementById('container')
  );
</script>
```

#### harmony usage
```
<script src="react.js"></script>
<script src="react-dom.js"></script>
<script src="browser.min.js"></script>
<script type="text/babel">
  class ExampleApplication extends React.Component {
    constructor(props) {
      super(props);
      this.state = { count: props.initialCount };
    }

    render() {
      var elapsed = Math.round(this.props.elapsed  / 100);
      var seconds = elapsed / 10 + (elapsed % 10 ? '' : '.0' );
      var message = `React has been successfully running for ${seconds} seconds.`;

      return <p>{message}</p>;
    }
  }
  var start = new Date().getTime();
  setInterval(() => {
    ReactDOM.render(
      <ExampleApplication elapsed={new Date().getTime() - start} />,
      document.getElementById('container')
    );
  }, 50);
</script>
```


#### precompile
```
npm install -g babel-cli
npm install babel-preset-react
babel index.js --presets react --out-dir=build
```

```
//index.js

var App = React.createClass({
  getInitialState: function() {
    return { count: 0 };
  },
  handleClick: function() {
    this.setState({count: this.state.count + 1});
  },
  render: function() {
    return <button onClick={this.handleClick}>
            clicks: {this.state.count} 
            </button>;
  }
});

ReactDOM.render(<App />, document.getElementById('container'));

```

```
<script src="build/react.js"></script>
<script src="build/react-dom.js"></script>
<script src="build/index.js"></script>
```



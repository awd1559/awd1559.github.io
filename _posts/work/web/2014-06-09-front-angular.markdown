---
layout:     post
title:      "angular"
subtitle:   " \"web front angular\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: web
permalink: /web/angular
tags:
    - web
---
> - [web front目录](/web/front)






# [angularjs](https://angularjs.org/)
[source code on github](https://github.com/angular/angular.js)<br>
[angular.io](https://github.com/angular/angular.io) site for Angular 2 documentation<br>
[doc](http://docs.angularjs.cn/api)<br>

# Angularjs in IDEA

```
newproject -> static web -> AngularJS
run config -> npm 
command:run
script: start
说明：
npm start -> package.json中的start, 启动http-server
依赖:
bower -> bower.json
    angular: 1.5
    angular-route
    angular-loader
    angular-mocks
    html5-boilerplate: 5.3
http-server
karma
```







# Angular CLI

```
npm install angular-cli
newproject -> static web -> AngularCLI
AngularCLI: C:\Users\awd\AppData\Roaming\npm\node_modules\angular-cli

open localhost:4200
```







#### basic

```
var app = angular.module('app', ['ngRoute']);
var app = angular.module('app', []).run(function($rootScope) {$rootScope.name = "wwww";});
<div ng-app="app">
  <h1>name: {{ name }}</h1>
</div>

app.controller("HelloController", ['$scope', '$http', function($scope, $http){
    $http.get('http://rest-service.guides.spring.io/greeting')
        .success(function(data) {
            $scope.greeting = data;
        });
    $scope.counter = 0;
    $scope.add = function(amount) { $scrope.conter += amount; };
}]);

```


```
<html ng-app="app">
  <body>
    <div ng-controller="HelloController">
      <p>The ID is {{ greeting.id }}</p>
      <p>The content is {{ greeting.content }}</p>
      <button ng-click="add(1)" class="button">Add</button>
    </div>
    <div>
        <input ng-model="person.name" type="text" placeholder="name">
        <h1>Hello, {{ person.name }}</h1>
    </div>
    <script src="angular.js"></script>
    <script src="app.js"></script>
  </body>
</html>
```



```
<div ng-controller="MyController">
  <input ng-model="expr" type="text" placeholder="enter an expression" />
  <h2>{{ parseValue }}</h2>
</div>
```

```
app.controller('MyController', function($scope, $parse){
    $scope.$watch('expr', function(newVal, oldVal, scope){
      if (newValue !== oldValue) {
        var parseFun = $parse(newVal);
        $scope.parsedValue = parseFun(scope);
      }
    });
});
```




#### factory

```
angular.module('app.services')
.factory('User', function($http) { // injectables go here
  var backendUrl = "http://localhost:3000";  var service = {    // our factory definition
    user: {},
    setName: function(newName) { 
      service.user['name'] = newName; 
    },
    setEmail: function(newEmail) {
      service.user['email'] = newEmail;
    },
    save: function() {
      return $http.post(backendUrl + '/users', {
        user: service.user
      });
    }
  };  return service;
});
```

#### service

```
angular.module('app.services')
.service('User', function($http) { // injectables go here
  var self = this; // Save reference
  this.user = {};
  this.backendUrl = "http://localhost:3000";
  this.setName = function(newName) {
    self.user['name'] = newName;
  }
  this.setEmail = function(newEmail) {
    self.user['email'] = newEmail;
  }
  this.save = function() {
    return $http.post(self.backendUrl + '/users', {
      user: self.user
    })
  }
});

angular.module('app')
.controller('MainCtrl', function($scope, User) {
  $scope.saveUser = User.save;
});
```



##### provider

```
angular.module('app.services')
.provider('User', function() {
  this.backendUrl = "http://localhost:3000";
  this.setBackendUrl = function(newUrl) {
    if (url) this.backendUrl = newUrl;
  }
  this.$get = function($http) { // injectables go here
    var self = this;
    var service = {
      user: {},
      setName: function(newName) {
        service.user['name'] = newName;
      },
      setEmail: function(newEmail) {
        service.user['email'] = newEmail;
      },
      save: function() {
        return $http.post(self.backendUrl + '/users', {
          user: service.user
        })
      }
    };
    return service;
  }
});

angular.module('myApp')
.config(function(UserProvider) {
  UserProvider.setBackendUrl("http://myApiBackend.com/api");
})
```


# Component

- [ngmodules](https://ngmodules.org/)
- [angular-ui](https://github.com/angular-ui)



#### [angular-material](https://github.com/angular/material)

```
//install
bower install angular-material
//build
npm install
gulp build
//view the doc
gulp docs
cd dist/docs
php -S 
```






#### [lumX](https://github.com/lumapps/lumX)
- [demo&doc](http://ui.lumapps.com/) 

  AngularJS, Google Material Design
  
  demo code included in github(express+angularjs)
  to use the demo
 
```
    npm install & bower install
    gulp serve
    http://localhost:8080
  
  angular.module('myModule', ['lumx']);
```





# Project

- [ng-admin](https://github.com/marmelab/ng-admin)
- [taigaio](https://github.com/taigaio)




# examples
- [angularmvctutorial](https://github.com/bumblebeeman/angularmvctutorial)      angularjs in asp.netmvc




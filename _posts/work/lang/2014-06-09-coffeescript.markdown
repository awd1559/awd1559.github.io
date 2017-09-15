---
layout:     post
title:      "coffeescript"
subtitle:   " \"coffeescript\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: lang
permalink: /lang/coffeescript
tags:
    - lang
---
> - [web front目录](/web/front)



＃ coffeescript

#### 函数

```
//js
var square = function(x) {
  return x * x;
};

//coffee 
square = (x) -> x * x
change = -> "ok"

//js
var cube = function(x) {
  return square(x) * x;
};

//coffee
cube   = (x) -> square(x) * x

//js
var fill = function(container, liquid= "coffee") {
	return "Filling the " + container + " with " + liquid + "...";
};

//coffee
fill = (container, liquid = "coffee") ->
  "Filling the #{container} with #{liquid}..."

```

#### object array

```
//js
var song = ["do", "re", "mi", "fa", "so"];

var singers = {
  Jagger: "Rock",
  Elvis: "Roll"
};


var kids = {
  brother: {
    name: "Max",
    age: 11
  },
  sister: {
    name: "Ida",
    age: 9
  }
};

//coffee
//do not need var 
kids =
  brother:
    name: "Max"
    age:  11
  sister:
    name: "Ida"
    age:  9
```

#### if, else, unless

```
//js
if (happy && sad)
if (happy || sad)

//coffee
if happty and sad
if happy or sad
```


#### 循环与推导

```
//js
var foods = ['toast', 'cheese', 'wine']
for (var i = 0, var len = foods.length; i < len; i++) {
  food = foods[i];
  eat(food);
}

//coffee
eat food for food in ['toast', 'cheese', 'wine']

//js
var courses = ['greens', 'caviar', 'truffles', 'roast', 'cake'];
var i,j,len
for (i = j = 0, len = courses.length; j < len; i = ++j) {
  dish = courses[i];
  menu(i + 1, dish);
}

//coffee
courses = ['greens', 'caviar', 'truffles', 'roast', 'cake']
menu i + 1, dish for dish, i in courses

//coffee
foods = ['broccoli', 'spinach', 'chocolate']
eat food for food in foods when food isnt 'chocolate'

//coffee
evens = (x for x in [0..10] by 2)

yearsOld = max: 10, ida: 9, tim: 11

ages = for child, age of yearsOld
  "#{child} is #{age}"


//js
if (this.studyingEconomics) {
  while (supply > demand)    { buy(); }
  while (!(supply > demand)) { sell();}
}

//coffee
if this.studyingEconomics
  buy()  while supply > demand
  sell() until supply > demand


//js 
var num = 6;
result = (function() {
  var _results;
  _results = [];
  while(num -= 1) {_result.push(""+ num + "littile monkeys");}
  return _results;
})();

//coffee
num = 6
result = while num -= 1
  "#{num} little monkeys, jumping on the bed. One fell out and bumped his head."

```

#### Range

```
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9] #var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];

start = numbers[0..2] #var start = numbers.slice(0,3);

middle = numbers[3...-2] #var middle = numbers.slice(3,-2);

end = numbers[-2..]  #var end = numbers.slice(-2);

copy = numbers[..]   #var copy = numbers.slice(0);
```






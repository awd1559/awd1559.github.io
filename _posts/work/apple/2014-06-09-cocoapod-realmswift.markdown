---
layout:     post
title:      "RealmSwift"
subtitle:   " \"RealmSwift\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
>[RealmSwift](https://github.com/realm/realm-cocoa)
><small>目录:[cocoapod](/2014/06/09/cocoapod-cocoapod)</small>

# install

```
pod 'RealmSwift'
```


# doc

```
https://realm.io/docs/swift/latest/
```

# usage 

```
// Define your models like regular Swift classes
class Dog: Object {
  dynamic var name = ""
  dynamic var age = 0
}
class Person: Object {
  dynamic var name = ""
  dynamic var picture: NSData? = nil // optionals supported
  let dogs = List<Dog>()
}

// Use them like regular Swift objects
let myDog = Dog()
myDog.name = "Rex"
myDog.age = 1
print("name of dog: \(myDog.name)")

// Get the default Realm
let realm = try! Realm()

// Query Realm for all dogs less than 2 years old
let puppies = realm.objects(Dog).filter("age < 2")
puppies.count // => 0 because no dogs have been added to the Realm yet

// Persist your data easily
try! realm.write {
  realm.add(myDog)
}

// Queries are updated in real-time
puppies.count // => 1

// Query and update from any thread
dispatch_async(dispatch_queue_create("background", nil)) {
  let realm = try! Realm()
  let theDog = realm.objects(Dog).filter("age == 1").first
  try! realm.write {
    theDog!.age = 3
  }
}
```


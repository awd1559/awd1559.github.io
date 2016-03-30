---
layout:     post
title:      "ObjectMapper"
subtitle:   " \"ObjectMapper\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
ObjectMapper
https://github.com/Hearst-DD/ObjectMapper


//install
pod 'ObjectMapper', '~> 1.1’



class User: Mappable {
    var username: String?
    var age: Int?
    var weight: Double!
    var array: [AnyObject]?
    var dictionary: [String : AnyObject] = [:]
    var bestFriend: User?                       // Nested User object
    var friends: [User]?                        // Array of Users
    var birthday: NSDate?

    required init?(_ map: Map) {

    }

    // Mappable
    func mapping(map: Map) {
        username    	<- map["username"]
        age         		<- map["age"]
        weight      	<- map["weight"]
        array       		<- map["arr"]
        dictionary  	<- map["dict"]
        bestFriend  	<- map["best_friend"]
        friends     	<- map["friends"]
        birthday    	<- (map["birthday"], DateTransform())
    }
}


//JSONString -> model
let user = Mapper<User>().map(JSONString)
//Model -> JSONString
let JSONString = Mapper().toJSONString(user, prettyPrint: true)



//嵌套
"distance" : {
     "text" : "102 ft",
     "value" : 31
}

func mapping(map: Map) {
    distance <- map["distance.value"]
}
distance <- map["distances.0.value"]



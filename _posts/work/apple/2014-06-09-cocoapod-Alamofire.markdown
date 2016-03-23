---
layout:     post
title:      "Alamofire"
subtitle:   " \"Alamofire\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
Alamofire
https://github.com/Alamofire/Alamofire

pod 'Alamofire', '~> 3.0’
import Alamofire

Making a Request
Alamofire.request(.GET, “https://httpbin.org/get”)
.responseString{response in 
	self.label.text = response.result.value
}

Response Handling
response(
resonseData
responseString
responseJSON
responsePropertyList

request: NSURLRequest
response: NSHTTPURLResponse
data: NSData
error: NSError

Alamofire.request(.GET, "https://httpbin.org/get", parameters: ["foo": "bar"])
         .responseJSON { response in
             print(response.request)  // original URL request
             print(response.response) // URL response
             print(response.data)     // server data
             print(response.result)   // result of response serialization

             if let JSON = response.result.value {
                 print("JSON: \(JSON)")
             }
         }


response handler
Alamofire.request(.GET, "https://httpbin.org/get", parameters: ["foo": "bar"])
         .response { request, response, data, error in
             print(request)
             print(response)
             print(data)
             print(error)
          }
response data handler
Alamofire.request(.GET, "https://httpbin.org/get", parameters: ["foo": "bar"])
         .responseData { response in
             print(response.request)
             print(response.response)
             print(response.result)
          }
response string handler
Alamofire.request(.GET, "https://httpbin.org/get")
         .responseString { response in
             print("Success: \(response.result.isSuccess)")
             print("Response String: \(response.result.value)")
         } response json handler
Alamofire.request(.GET, "https://httpbin.org/get")
         .responseJSON { response in
             debugPrint(response)
         }
chained response handlers
Alamofire.request(.GET, "https://httpbin.org/get")
         .responseString { response in
             print("Response String: \(response.result.value)")
         }
         .responseJSON { response in
             print("Response JSON: \(response.result.value)")
         }

HTTP methods

Parameters

HTTP Headers
let headers = [
    "Authorization": "Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==",
    "Content-Type": "application/x-www-form-urlencoded"
]

Alamofire.request(.GET, "https://httpbin.org/get", headers: headers)
         .responseJSON { response in
             debugPrint(response)
         }



response serialization
use Ono




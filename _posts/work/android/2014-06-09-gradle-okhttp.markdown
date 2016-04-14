---
layout:     post
title:      "okhttp"
subtitle:   " \"Android okhttp by square\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[okhttp](http://square.github.io/okhttp)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


# install

```
compile 'com.squareup.okhttp3:okhttp:3.2.0'
```

# get 

```
String url = "https://raw.github.com/square/okhttp/master/README.md";

OkHttpClient client = new OkHttpClient();

String run(String url) throws IOException {
  Request request = new Request.Builder().url(url).build();
  Response response = client.newCall(request).execute();
  return response.body().string();
}
```

# post json string

```
public static final MediaType JSON = MediaType.parse("application/json; charset=utf-8");

OkHttpClient client = new OkHttpClient();

String post(String url, String json) throws IOException {
  RequestBody body = RequestBody.create(JSON, json);
  Request request = new Request.Builder()
      .url(url)
      .post(body)
      .build();
  Response response = client.newCall(request).execute();
  return response.body().string();
}
```

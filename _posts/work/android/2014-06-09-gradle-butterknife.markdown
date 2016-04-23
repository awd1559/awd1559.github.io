---
layout:     post
title:      "butterknife"
subtitle:   " \"Android butterknife\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[butterknife](https://github.com/JakeWharton/butterknife)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>

Bind Android views and callbacks

# install 

```
compile 'com.jakewharton:butterknife:7.0.1'
```

# usage

```
@Bind(R.id.user) EditText username;
@Bind(R.id.pass) EditText password;

@BindString(R.string.login_error)
String loginErrorMessage;

@OnClick(R.id.submit) 
void submit(View view) {
  // TODO call server...
}

@Override public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.simple_activity);
  ButterKnife.bind(this);
}

```
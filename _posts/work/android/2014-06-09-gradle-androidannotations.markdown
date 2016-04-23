---
layout:     post
title:      "AndroidAnnotations"
subtitle:   " \"AndroidAnnotations: Dependency Injection<50K\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[AndroidAnnotations](https://github.com/excilys/androidannotations)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


@EActivity(R.layout.main)  

@ViewById(R.id.myTextView)  

@Click


@Click({R.id.button1,R.id.button2,R.id.button3})  
void buttonClicked(Button bt){  
    switch(bt.getId()){  
    case R.id.button1:  //  
        break;  
        ...  
    }  
} 


@EBean,@RootContext,@UiThread
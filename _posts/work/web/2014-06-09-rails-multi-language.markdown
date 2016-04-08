---
layout:     post
title:      "多语言"
subtitle:   " \"rails多语言\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - ruby
---
使用多语言
config/application.rb
config.i18n.default_locale = :cn
新建文件config/locales/cn.*.yml
cn:
  helpers:
    actions: “文字”

使用方法：t('.cancel', :default => t(“helpers.actions"))


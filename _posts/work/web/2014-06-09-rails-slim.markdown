---
layout:     post
title:      "rails-slim"
subtitle:   " \"slim\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - ruby
---
gem ‘slim’		会遇到:slim [not found]
使用gem ‘slim-rails’
修改config/application.rb
class Application < Rails::Application
  config.sass.preferred_syntax= :sass
    config.generators do |g|
      g.template_engine :slim
    end
end
之后，rails g controller home 将创建controler.sass 和action.html.slim

erb2slim
sass-convert进行文件迁移, 可以吗？？







开头
doctype html
html
  head 
    title slim template
     meta name=‘name’ content=‘content’
  body
    h1 here to go



#content 
  p this is p
===><div id=‘content’><p>thhis is p</p></div>


img src=“/image/image.jpg”
===> <img src=‘/image/image.jpg’ >


== yield                          <%= yield%>
== render ‘footer’             <%= render ‘footer’ %>






post














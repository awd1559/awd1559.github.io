---
layout:     post
title:      "分页"
subtitle:   " \"rails分页\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - ruby
---
paging
Gemfile
  gem ‘will_paginate’
book_controller.rb
 def index
   @books = Book.paginate :page => params[:page], :per_page => 10
 end
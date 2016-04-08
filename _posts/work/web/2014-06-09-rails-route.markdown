---
layout:     post
title:      "rails"
subtitle:   " \"ruby-rails\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - ruby
---

# route
使用member和collection
resources :photos do 				resources :photos do
  member do					  get ‘preview’,  on:  :member
     get ‘preview’				end
  end
end
==> get /photos/1/preview    => photos#preview  params[:id]
==> preview_photo_url、preview_photo_path



resources :photos do                                resource :photos do
  collection do					get ‘search’, on:  :collection
    get ‘search’ 				      end
  end
end
==> get /photos/search   => photos#seach
==>search_photos_url search_photos_path


使用has_many :through， 不使用has_and_belongs_to_many

为多次使用的验证创建validator
class EmailValidator <ActiveModal::EachValidator


使用named_scope
clas User < ActiveRecord::Base
  scope :active, -> {where(active: true)}
  scope :inactive, ->{ where(active: false) }
end

触发检查
@book.valid?

往errors中添加
@book.errors.add :price, “价格有误”

没有错误
@book.errors.empty?

有错误
@book.errors.any?


密码确认
if !(params[:password_confirm].eql? @publisher.password) then
      @publisher.errors.add :password, "两次密码输入不一致"
end
最好写在modal里:





html: <input name=‘myname’ />
服务端获取: params[:myname]

get :参数在url中
post:参数不在url中


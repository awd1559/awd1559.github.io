---
layout:     post
title:      "rails ajax"
subtitle:   " \"rails ajax\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - ruby
---
paylog.coffee

$ ->
  $('#btnAdd').click (event) ->
    event.preventDefault() # 最开始的时候忘记加这句了，导致默认的提交动作也被执行了
    $.ajax(
      type: "POST"
      url: "/paylogs/add"
      success: ->
        alert "success"
    )

为form中的btnAdd按钮添加ajax



或者使用 remote, Rails中自带ajax
<%= form_for(@book, remote:true) do |f| %>

在控制器中
format.js { render :layout => false, :status => 406  }
paylog/new.js.erb中
<% if @reply.errors.empty? %>
  $('<%= escape_javascript(render :partial => 'reply', :object => @reply) %>').hide().appendTo($('#replies table > tbody')).fadeIn('fast').css('display', 'table-row');
<% else %>
  $('<span class="error-message"><%= escape_javascript(@reply.errors.full_messages.join(',')) %></span>').appendTo($('#new_reply_form'))
<% end %>
返回jquery代码，由客户端执行


或者
客户端ajax提交
$('new_reply_form').on('submit', function(event){
    $.ajax({
	url: $(this).prop('action'), 
	dataType: 'json', /* more option */
	onsuccess: } 
    )
})
服务端控制器中返回json数据
 format.json { render :json => {:errors => @reply.errors.full_messages.join(',')} } 
json数据交由客户端js代码渲染
{“comments”:[
	{“content”:"很不错嘛","id":1,"nickname":"纳尼"},
	{"content":"哟西哟西","id":2,"nickname":"小强"}
]}
$.each()方法接受两个参数，第一个是需要遍历的对象集合（JSON对象集合），第二个是用来遍历的方法，这个方法又接受两个参数，第一个是遍历的index，第二个是当前遍历的值。
$.each(data.comments, function(i, item) {
            $("#info").append(
                    "<div>" + item.id + "</div>" + 
                    "<div>" + item.nickname    + "</div>" +
                    "<div>" + item.content + "</div><hr/>");
        });

可直接使用parseJson函数
var json_str = '{"a":1, "b":2}';
 var data = $.parsejson(json_str);
 alert(data.a)

或者使用spine.js框架

gem spine-rails
gem json2-rails
gem jquery-rails
rails g spine:new
	生成以下目录文件
	app/assets/javscripts/app/models/
	app/assets/javscripts/app/views/
	app/assets/javscripts/app/controllers/
	app/assets/javscripts/app/index.js.coffeescript
rails g spine:new -app for_bar	#使用不同的namespace


example usage:
rails new blog
gem “spine-rails"
bundle install

rails g scaffold Post title:string content:string
rake db:migrate

rails g spine:new
rails g spine:model Post title content
rails g spine:controller Posts

use spine
// Sends an AJAX POST to the server
var post = App.Post.create({
  title: 'Hello World!',
  content: 'Spine & Rails, sitting in a tree!'
});

// => ID returned from Rails
post.id;

// Sends AJAX PUT to the server
post.updateAttributes({title: 'Goodbye'});






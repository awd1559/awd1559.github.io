---
layout:     post
title:      "rails-view"
subtitle:   " \"ruby\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - ruby
---
模版*.html.erb
<% %> 执行Ruby代码，没有返回值
<%= %> 用来输出结果



url 
<%= link_to 'show',  @book %>  			//books#show/:id
<%= link_to 'Back', books_path %>		//books#index



循环
<% @people.each do |person| %>
  Name: <%= person.name %><br>
<% end %>


builder模版,扩展名为.builder
xml.em("emphasized")
xml.em { xml.b("emph & bold") }
xml.a("A Link", "href" => "http://rubyonrails.org")
xml.target("name" => "compile", "option" => "fast")
输出结果：
<em>emphasized</em>
<em><b>emph &amp; bold</b></em>
<a href="http://rubyonrails.org">A link</a>
<target option="fast" name="compile" />

<%= render “menu” %>	输出_menu.html.erb
<%= render “shared/menu” %> 输出app/views/shared/_menu.html.erb
<%= render partial: “product” %>
<%= render partial: “product”, collection: @products %>




局部布局
box布局中渲染 _post局部视图
<%= render partial: ‘post’, layout: ‘box’, locals: {post: @post} %>


RecordTagHelper
content_tag_for
<%= content_tag_for(:tr, @post, class: "frontpage") do %>
  <td><%= @post.title %></td>
<% end %>
生成的 HTML 如下：
<tr id="post_1234" class="post frontpage">
  <td>Hello World!</td>
</tr>

<%= content_tag_for(:tr, @posts) do |post| %>
  <td><%= post.title %></td>
<% end %>
生成的 HTML 如下：
<tr id="post_1234" class="post">
  <td>Hello World!</td>
</tr>
<tr id="post_1235" class="post">
  <td>Ruby on Rails Rocks!</td>
</tr>




div_for
<%= div_for(@post, class: "frontpage") do %>
  <td><%= @post.title %></td>
<% end %>
生成的 HTML 如下：
<div id="post_1234" class="post frontpage">
  <td>Hello World!</td>
</div>

AssetTagHelper
stylesheet_link_tag
javascript_include_tag

CaptureHelper
<%= yield :special %>
<%= content_for :special %>
  ………………
<% end %>

DateHelper

DebugHelper
debug(my_hash)

FormHelper
<%= form_for @person, url: {action: "create"} do |f| %>
  <%= f.text_field :first_name %>
  <%= f.text_field :last_name %>
  <%= submit_tag 'Create' %>
<% end %>
生成的 HTML 如下：
<form action="/people/create" method="post">
  <input id="person_first_name" name="person[first_name]" type="text" />
  <input id="person_last_name" name="person[last_name]" type="text" />
  <input name="commit" type="submit" value="Create" />
</form>
表单提交后创建的 params 对象如下：
{"action" => "create", "controller" => "people", "person" => {"first_name" => "William", "last_name" => "Smith"}}

f.check_box
# Let's say that @post.validated? is 1:
check_box("post", "validated")
# => <input type="checkbox" id="post_validated" name="post[validated]" value="1" />
#    <input name="post[validated]" type="hidden" value="0" />
f.file_field
file_field(:user, :avatar)
# => <input type="file" id="user_avatar" name="user[avatar]" />
f.hidden_field
hidden_field(:user, :token)
# => <input type="hidden" id="user_token" name="user[token]" value="#{@user.token}" />
f.label
label(:post, :title)
# => <label for="post_title">Title</label>
f.password_field
password_field(:login, :pass)
# => <input type="text" id="login_pass" name="login[pass]" value="#{@login.pass}" />
f.radio_button
# Let's say that @post.category returns "rails":
radio_button("post", "category", "rails")
radio_button("post", "category", "java")
# => <input type="radio" id="post_category_rails" name="post[category]" value="rails" checked="checked" />
#    <input type="radio" id="post_category_java" name="post[category]" value="java" />
f.text_area
text_area(:comment, :text, size: "20x30")
# => <textarea cols="20" rows="30" id="comment_text" name="comment[text]">
#      #{@comment.text}
#    </textarea>
f.text_field
text_field(:post, :title)
# => <input type="text" id="post_title" name="post[title]" value="#{@post.title}" />
f.email_field
email_field(:user, :email)
# => <input type="email" id="user_email" name="user[email]" value="#{@user.email}" />
f.url_field
url_field(:user, :url)
# => <input type="url" id="user_url" name="user[url]" value="#{@user.url}" />

FormOptionsHelper
这个模块提供很多方法用来把不同类型的集合转换成一组 option 标签。
6.10.1 collection_select
为 object 类的 method 方法返回的集合创建 select 和 option 标签。
使用此方法的模型示例：
class Post < ActiveRecord::Base
  belongs_to :author
end

class Author < ActiveRecord::Base
  has_many :posts
  def name_with_initial
    "#{first_name.first}. #{last_name}"
  end
end

使用举例，为文章实例（@post）选择作者（Author）：
collection_select(:post, :author_id, Author.all, :id, :name_with_initial, {prompt: true})

如果 @post.author_id 的值是 1，上述代码生成的 HTML 如下：
<select name="post[author_id]">
  <option value="">Please select</option>
  <option value="1" selected="selected">D. Heinemeier Hansson</option>
  <option value="2">D. Thomas</option>
  <option value="3">M. Clark</option>
</select>

6.10.2 collection_radio_buttons
为 object 类的 method 方法返回的集合创建 radio_button 标签。
使用此方法的模型示例：
class Post < ActiveRecord::Base
  belongs_to :author
end

class Author < ActiveRecord::Base
  has_many :posts
  def name_with_initial
    "#{first_name.first}. #{last_name}"
  end
end

使用举例，为文章实例（@post）选择作者（Author）：
collection_radio_buttons(:post, :author_id, Author.all, :id, :name_with_initial)

如果 @post.author_id 的值是 1，上述代码生成的 HTML 如下：
<input id="post_author_id_1" name="post[author_id]" type="radio" value="1" checked="checked" />
<label for="post_author_id_1">D. Heinemeier Hansson</label>
<input id="post_author_id_2" name="post[author_id]" type="radio" value="2" />
<label for="post_author_id_2">D. Thomas</label>
<input id="post_author_id_3" name="post[author_id]" type="radio" value="3" />
<label for="post_author_id_3">M. Clark</label>

6.10.3 collection_check_boxes
为 object 类的 method 方法返回的集合创建复选框标签。
使用此方法的模型示例：
class Post < ActiveRecord::Base
  has_and_belongs_to_many :authors
end

class Author < ActiveRecord::Base
  has_and_belongs_to_many :posts
  def name_with_initial
    "#{first_name.first}. #{last_name}"
  end
end

使用举例，为文章实例（@post）选择作者（Author）：
collection_check_boxes(:post, :author_ids, Author.all, :id, :name_with_initial)

如果 @post.author_ids 的值是 [1]，上述代码生成的 HTML 如下：
<input id="post_author_ids_1" name="post[author_ids][]" type="checkbox" value="1" checked="checked" />
<label for="post_author_ids_1">D. Heinemeier Hansson</label>
<input id="post_author_ids_2" name="post[author_ids][]" type="checkbox" value="2" />
<label for="post_author_ids_2">D. Thomas</label>
<input id="post_author_ids_3" name="post[author_ids][]" type="checkbox" value="3" />
<label for="post_author_ids_3">M. Clark</label>
<input name="post[author_ids][]" type="hidden" value="" />

6.10.4 country_options_for_select
返回一组 option 标签，几乎包含世界上所有国家。
6.10.5 country_select
返回指定对象和方法的 select 和 option 标签。使用 country_options_for_select 方法生成各个 option 标签。
6.10.6 option_groups_from_collection_for_select
返回一个字符串，由多个 option 标签组成。和 options_from_collection_for_select 方法类似，但会根据对象之间的关系使用 optgroup 标签分组。
使用此方法的模型示例：
class Continent < ActiveRecord::Base
  has_many :countries
  # attribs: id, name
end

class Country < ActiveRecord::Base
  belongs_to :continent
  # attribs: id, name, continent_id
end

使用举例：
option_groups_from_collection_for_select(@continents, :countries, :name, :id, :name, 3)

可能得到的输出如下：
<optgroup label="Africa">
  <option value="1">Egypt</option>
  <option value="4">Rwanda</option>
  ...
</optgroup>
<optgroup label="Asia">
  <option value="3" selected="selected">China</option>
  <option value="12">India</option>
  <option value="5">Japan</option>
  ...
</optgroup>

注意，这个方法只会返回 optgroup 和 option 标签，所以你要把输出放入 select 标签中。
6.10.7 options_for_select
接受一个集合（Hash，数组，可枚举的对象等），返回一个由 option 标签组成的字符串。
options_for_select([ "VISA", "MasterCard" ])
# => <option>VISA</option> <option>MasterCard</option>

注意，这个方法只返回 option 标签，所以你要把输出放入 select 标签中。
6.10.8 options_from_collection_for_select
遍历 collection，返回一组 option 标签。每个 option 标签的值是在 collection 元素上调用 value_method 方法得到的结果，option 标签的显示文本是在 collection 元素上调用 text_method 方法得到的结果
# options_from_collection_for_select(collection, value_method, text_method, selected = nil)

例如，下面的代码遍历 @project.people，生成一组 option 标签：
options_from_collection_for_select(@project.people, "id", "name")
# => <option value="#{person.id}">#{person.name}</option>

注意：options_from_collection_for_select 方法只返回 option 标签，你应该将其放在 select 标签中。
6.10.9 select
创建一个 select 元素以及根据指定对象和方法得到的一系列 option 标签。
例如：
select("post", "person_id", Person.all.collect {|p| [ p.name, p.id ] }, {include_blank: true})

如果 @post.person_id 的值为 1，返回的结果是：
<select name="post[person_id]">
  <option value=""></option>
  <option value="1" selected="selected">David</option>
  <option value="2">Sam</option>
  <option value="3">Tobias</option>
</select>

6.10.10 time_zone_options_for_select
返回一组 option 标签，包含几乎世界上所有的时区。
6.10.11 time_zone_select
为指定的对象和方法返回 select 标签和 option 标签，option 标签使用 time_zone_options_for_select 方法生成。
time_zone_select( "user", "time_zone")

6.10.12 date_field
返回一个 date 类型的 input 标签，用于访问指定的属性。
date_field("user", "dob")

6.11 FormTagHelper
这个模块提供一系列方法用于创建表单标签。FormHelper 依赖于传入模板的 Active Record 对象，但 FormTagHelper 需要手动指定标签的 name 属性和 value 属性。
6.11.1 check_box_tag
为表单创建一个复选框标签。
check_box_tag 'accept'
# => <input id="accept" name="accept" type="checkbox" value="1" />

6.11.2 field_set_tag
创建 fieldset 标签，用于分组 HTML 表单元素。
<%= field_set_tag do %>
  <p><%= text_field_tag 'name' %></p>
<% end %>
# => <fieldset><p><input id="name" name="name" type="text" /></p></fieldset>

6.11.3 file_field_tag
创建一个文件上传输入框。
<%= form_tag({action:"post"}, multipart: true) do %>
  <label for="file">File to Upload</label> <%= file_field_tag "file" %>
  <%= submit_tag %>
<% end %>

结果示例：
file_field_tag 'attachment'
# => <input id="attachment" name="attachment" type="file" />

6.11.4 form_tag
创建 form 标签，指向的地址由 url_for_options 选项指定，和 ActionController::Base#url_for 方法类似。
<%= form_tag '/posts' do %>
  <div><%= submit_tag 'Save' %></div>
<% end %>
# => <form action="/posts" method="post"><div><input type="submit" name="submit" value="Save" /></div></form>

6.11.5 hidden_field_tag
为表单创建一个隐藏的 input 标签，用于传递由于 HTTP 无状态的特性而丢失的数据，或者隐藏不想让用户看到的数据。
hidden_field_tag 'token', 'VUBJKB23UIVI1UU1VOBVI@'
# => <input id="token" name="token" type="hidden" value="VUBJKB23UIVI1UU1VOBVI@" />

6.11.6 image_submit_tag
显示一个图片，点击后提交表单。
image_submit_tag("login.png")
# => <input src="/images/login.png" type="image" />

6.11.7 label_tag
创建一个 label 标签。
label_tag 'name'
# => <label for="name">Name</label>

6.11.8 password_field_tag
创建一个密码输入框，用户输入的值会被遮盖。
password_field_tag 'pass'
# => <input id="pass" name="pass" type="password" />

6.11.9 radio_button_tag
创建一个单选框。如果希望用户从一组选项中选择，可以使用多个单选框，name 属性的值都设为一样的。
radio_button_tag 'gender', 'male'
# => <input id="gender_male" name="gender" type="radio" value="male" />

6.11.10 select_tag
创建一个下拉选择框。
select_tag "people", "<option>David</option>"
# => <select id="people" name="people"><option>David</option></select>

6.11.11 submit_tag
创建一个提交按钮，按钮上显示指定的文本。
submit_tag "Publish this post"
# => <input name="commit" type="submit" value="Publish this post" />

6.11.12 text_area_tag
创建一个多行文本输入框，用于输入大段文本，例如博客和描述信息。
text_area_tag 'post'
# => <textarea id="post" name="post"></textarea>

6.11.13 text_field_tag
创建一个标准文本输入框，用于输入小段文本，例如用户名和搜索关键字。
text_field_tag 'name'
# => <input id="name" name="name" type="text" />

6.11.14 email_field_tag
创建一个标准文本输入框，用于输入 Email 地址。
email_field_tag 'email'
# => <input id="email" name="email" type="email" />

6.11.15 url_field_tag
创建一个标准文本输入框，用于输入 URL 地址。
url_field_tag 'url'
# => <input id="url" name="url" type="url" />

6.11.16 date_field_tag
创建一个标准文本输入框，用于输入日期。
date_field_tag "dob"
# => <input id="dob" name="dob" type="date" />

6.12 JavaScriptHelper
这个模块提供在视图中使用 JavaScript 的相关方法。
6.12.1 button_to_function
返回一个按钮，点击后触发一个 JavaScript 函数。例如：
button_to_function "Greeting", "alert('Hello world!')"
button_to_function "Delete", "if (confirm('Really?')) do_delete()"
button_to_function "Details" do |page|
  page[:details].visual_effect :toggle_slide
end

6.12.2 define_javascript_functions
在一个 script 标签中引入 Action Pack JavaScript 代码库。
6.12.3 escape_javascript
转义 JavaScript 中的回车符、单引号和双引号。
6.12.4 javascript_tag
返回一个 script 标签，把指定的代码放入其中。
javascript_tag "alert('All is good')"

<script>
//<![CDATA[
alert('All is good')
//]]>
</script>

6.12.5 link_to_function
返回一个链接，点击后触发指定的 JavaScript 函数并返回 false。
link_to_function "Greeting", "alert('Hello world!')"
# => <a onclick="alert('Hello world!'); return false;" href="#">Greeting</a>

6.13 NumberHelper
这个模块提供用于把数字转换成格式化字符串所需的方法。包括用于格式化电话号码、货币、百分比、精度、进位制和文件大小的方法。
6.13.1 number_to_currency
把数字格式化成货币字符串，例如 $13.65。
number_to_currency(1234567890.50) # => $1,234,567,890.50

6.13.2 number_to_human_size
把字节数格式化成更易理解的形式，显示文件大小时特别有用。
number_to_human_size(1234)          # => 1.2 KB
number_to_human_size(1234567)       # => 1.2 MB

6.13.3 number_to_percentage
把数字格式化成百分数形式。
number_to_percentage(100, precision: 0)        # => 100%

6.13.4 number_to_phone
把数字格式化成美国使用的电话号码形式。
number_to_phone(1235551234) # => 123-555-1234

6.13.5 number_with_delimiter
格式化数字，使用分隔符隔开每三位数字。
number_with_delimiter(12345678) # => 12,345,678

6.13.6 number_with_precision
使用指定的精度格式化数字，精度默认值为 3。
number_with_precision(111.2345)     # => 111.235
number_with_precision(111.2345, 2)  # => 111.23

6.14 SanitizeHelper
SanitizeHelper 模块提供一系列方法，用于剔除不想要的 HTML 元素。
6.14.1 sanitize
sanitize 方法会编码所有标签，并删除所有不允许使用的属性。
sanitize @article.body

如果指定了 :attributes 或 :tags 选项，只允许使用指定的标签和属性。
sanitize @article.body, tags: %w(table tr td), attributes: %w(id class style)

要想修改默认值，例如允许使用 table 标签，可以这么设置：
class Application < Rails::Application
  config.action_view.sanitized_allowed_tags = 'table', 'tr', 'td'
end

6.14.2 sanitize_css(style)
过滤一段 CSS 代码。
6.14.3 strip_links(html)
删除文本中的所有链接标签，但保留链接文本。
strip_links("<a href="http://rubyonrails.org">Ruby on Rails</a>")
# => Ruby on Rails

strip_links("emails to <a href="mailto:me@email.com">me@email.com</a>.")
# => emails to me@email.com.

strip_links('Blog: <a href="http://myblog.com/">Visit</a>.')
# => Blog: Visit.

6.14.4 strip_tags(html)
过滤 html 中的所有 HTML 标签，以及注释。
这个方法使用 html-scanner 解析 HTML，所以解析能力受 html-scanner 的限制。
strip_tags("Strip <i>these</i> tags!")
# => Strip these tags!

strip_tags("<b>Bold</b> no more!  <a href='more.html'>See more</a>")
# => Bold no more!  See more

注意，得到的结果中可能仍然有字符 <、> 和 &，会导致浏览器显示异常。
7 视图本地化
Action View 可以根据当前的本地化设置渲染不同的模板。
例如，假设有个 PostsController，在其中定义了 show 动作。默认情况下，执行这个动作时渲染的是 app/views/posts/show.html.erb。如果设置了 I18n.locale = :de，渲染的则是 app/views/posts/show.de.html.erb。如果本地化对应的模板不存在就使用默认模板。也就是说，没必要为所有动作编写本地化视图，但如果有本地化对应的模板就会使用。
相同的技术还可用在 public 文件夹中的错误文件上。例如，设置了 I18n.locale = :de，并创建了 public/500.de.html 和 public/404.de.html，就能显示本地化的错误页面。
Rails 并不限制 I18n.locale 选项的值，因此可以根据任意需求显示不同的内容。假设想让专业用户看到不同于普通用户的页面，可以在 app/controllers/application_controller.rb 中这么设置：
before_action :set_expert_locale

def set_expert_locale
  I18n.locale = :expert if current_user.expert?
end

然后创建只显示给专业用户的 app/views/posts/show.expert.html.erb 视图。


布局和视图渲染
redirect_to(@book)		#=> show.html.erb
render :edit     		#=> edit.html.erb
render plain: “OK”
render html: "<strong>Not Found</strong>".html_safe
render json: @product

表单帮助方法




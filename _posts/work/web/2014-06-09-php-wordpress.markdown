---
layout:     post
title:      "wordpress"
subtitle:   " \"web:wordpress\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
---
## wordpress

#### basic

```
admin url: localhost/wp-admin
```

```
//wp-content/themes/----/screenshot.jpg 300*225
//wp-content/themes/----/style.css

/*
Theme Name: Tutorial
Theme URI: https://wordpress.org/themes/----
Author: Book2
Author URI: https://wordpress.org/
Description: *****
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Tags: black, blue, gray, pink, purple
*/	
```

#### orders

```
//首页
	static html render by front-page.php
	home.php
	index.php
	
//文章页
	single-{posttype}.php
	single.php
	index.php
	
//page
	page-{slug}.php
	page-{id}.php
	page.php
	index.php
	
//category
	category-{slug}.php
	category-{id}.php
	category.php
	archive.php
	index.php
	
//tag
	tag-{slug}.php
	tag-{id}.php
	tag.php
	archive.php
	index.php
	
//自定义分类法taxonomy
	taxonomy-{taxonomy}-{term}.php
	taxonomy-{taxonomy}.php
	archive.php
	index.php
	
//自定义文章类型
	archive-{posttype}.php
	archive.php
	index.php
	
//author
	author-{nickname}.php
	author-{id}.php
	author.php
	archive.php
	index.php
	
//date
	date.php
	archive.php
	index.php
	
//search
	search.php
	index.php
	
//attach
	MIME-TYPE: image.php, video.php, application.php, text.php, plain.php, text_plain.php
	attachment.php
	single-attachment.php
	single.php
	index.php
	
```


#### index.php

```
<?php get_header(); ?>
<div id='container'>
	if(have_posts()) : while(have_posts()) : the_post();
		<a href="<?php the_permalink(); ?>"><?php the_title();?></a>
		the_tags();
		the_time('Y年n月j日');
		the_author();
		the_category();			        输出ul   li
		comments_popup_link('0 条评论'， '1 条评论', '% 条评论', '评论已关闭');//评论链接，输出a
		edit_post_link();				编辑文章链接,输出a
		the_excerpt();		                        内容提要
		endwhile;
		<?php previous_posts_link('&lt;&lt;新文章', 0); ?>   导航
		<?php next_posts_link('旧文章 &gt;&gt;', 0); ?>
	else:
		<p>没有找到任何文章</p>
	endif;
</div>

	<?php get_sidebar();?>

	<?php get_footer();?>
	
</body>
</html>
````

```
get_header()  => call header.php, or wp-includes/theme-compat/header.php
get_sidebar() => call sidebar.php
get_footer()  => call footer.php
```



#### functions.php

```
register_sidebar(array('name'=>'First_sidebar'));   主题定义中出现小工具栏
register_nav_menus($location,  $description);	//description将出现在后台menu设置中
register_post_type
register_taxonomy
```


#### header.php

```
<!DOCTYPE >
<html>
<head>
<title><?php if( is_home() ){
	bloginfo('name'); echo " - "; bloginfo('description');
} elseif ( is_category() ){
	single_cat_title(); echo " - "; bloginfo('name');
} elseif ( is_single() || is_page() ){
	single_post_title();
} elseif ( is_search() ){
	echo "搜索结果"; echo " - "; bloginfo('name');
} elseif ( is_404() ){
	echo '页面未找到！';
} else {
	wp_title('', true);
}?>
</title>
<link rel="stylesheet" href="<?php get_template_directory_uri();?>/css/bootstrap.min.css">
<link rel="stylesheet" href="<?php bloginfo('stylesheet_url'); ?>" type="text/css" media="screen" />
<link rel="alternate" type="application/rss+xml" title="RSS 2.0 - 所有文章" href="<?php echo $feed; ?>" />
<link rel="alternate" type="application/rss+xml" title="RSS 2.0 - 所有评论" href="<?php bloginfo('comments_rss2_url')?>" />
<link rel="pingback" href="<?php bloginfo('pingback_url'); ?>" />
<?php wp_head(); ?>
</head>
```


#### sidebar.php

```
if(!function_exists('dynamic_sidebar') || dynamic_slidebar('Frist_sidebar'))
```



#### single.php

```
comments_template(); 	//call comments.php
```



#### category.php

```
single_cat_title('', false)		当前category_name
$cat = get_the_category($post->ID);
$cat_name = $cat[0]->cat_name;
$cat_id = $cat[0]->term_id;

get_category_link($cat_id)
```


#### comments.php

```
if(!empty($post->post_password) && $_COOKIE['wp-postpass_' . COOKIEHASH] != $post->post_password){

} else if( !commens_open() ){

} else if( !have_comments() ) {

} else {
	wp_list_comments('type=comment&callback=');
}
do_action('comment_form', $post->ID);
```

#### search.php

```
get_search_form()			->require search form.php

get_search_query()			->获得搜索词

if(have_posts()){
	while(have_posts()){
		the_post();
		get_template_part('part/content', get_post_format());
	}
}
```

#### searchform.php

```
<form action="<?php echo esc_url( home_url('/' ) );?>">
</form>
```



# api

#### blog info Tag
```
bloginfo
bloginfo_rss
get_bloginfo
get_bloginfo_rss

//Lists & Dropdown tags
wp_lsit_authors
wp_list_categories
wp_list_pages
wp_list_bookmarks
wp_list_comments
wp_get_archives
wp_page_menu
wp_dropdown_pages
wp_dropdown_categories
wp_dropdown_users
```

---------- | ---------------------------------------------------------------------------------------------- |
name       | table > wp_options > blogname, 设置 > 常规 > 站点标题       										|
description| table > wp_options > blogdescription, 设置 > 常规 > 副标题  										|
wpurl	   | table > wp_options siteurl,可以使用site_url()函数代替bloginfo('wpurl')  							|
		   | #bloginfo(wpurl) 返回根站点的URL																	|
		   | #site_url()函数返回子站点的URL                             										|
siteurl	   | #table wp_options home,  设置 > 常规 中设置的 "站点地址（URL）")",可以使用 home_url()   				|
admin_email| #table wp_options admin_email, 设置 > 常规 中设置的 "电子邮件地址         							|
charset	   | #table wp_options blog_charset, 设置 > 常规 中设置的"页面和feed的编码"    							|
version	   | # wp-includes/version.php 中 $wp_version                              							|
html_type  | #table wp_options html_type, 内容类型（默认:"text/html"）,使用 pre_option_html_type 过滤器覆盖默认值 |
text_direction | #文本方向。可以使用 is_rtl() 代替。                                  							|
language       | #显示语言                                                         							|
stylesheet_url | #当前主题style.css路径，可使用get_stylesheet_uri()                  							|
stylesheet_directory | #显示当前主题的样式表路径，可使用get_stylesheet_directory_uri() 							|
template_url	     | #当前主题URL路径																		|
	                 |  #在子主题中， get_bloginfo('template_url')和get_template()都将返回父主题的目录			|
	                 |  #get_template_directory_uri()用于父主题目录											|
	                 |  #get_stylesheet_directory_uri()用于子主题目录 										|
pingback_url      | #显示通告文件 XML-RPC 的URL (xmlrpc.php)  	|
atom_url	      | #显示 Atom feed URL (/feed/atom)        		|
rdf_url		      | #显示 RDF/RSS 1.0 feed URL (/feed/rfd).  	|
rss_url		      | #显示rss feed URL (/feed/rss)             	|
rss2_url	      | #显示rss2 feed URL (/feed)                	|
comments_atom_url |	#显示评论的Atom feed URL(/comments/feed)   	|
comments_rss2_url |	#显示评论的rss2 feed URL(/comments/feed)   	|

#### filter
```
has_filter
add_filter
apply_filters
marge_filters
remove_filter
remove_all_filters
```

#### actions
```
has_action
add_action
do_action
do_action_ref_array
did_action
remove_action
remove_all_actions


register_activation_hook
register_deactivation_hook


add_action($action_name, $myfunction);
do_action($action_name, $args_to_myfunction);
plugins_loaded
sanitize_comment_cookies
setup_theme
auth_cookie_malformed
auth_cookie_valid
set_current_user
init
widgets_init
parse_request
send_headers
pre_get_posts
posts_selection
wp
template_redirect
get_header
wp_print_styles
wp_print_scripts
loop_start
loop_end
get_sidebar
wp_meta
get_footer
wp_footer
```

```
#header.php	
get_header()		#call header.php		
get_header('home')	#call header-home.php

#sidebar.php
get_sideabar()		#call sidebar.php
get_sidebar('home')	#call sidebar-home.php

#search.php
get_search_form()		#call search.php

#comments.php
comments_template()		#call comments.php

#footer.php
get_footer()			# call footer.php
get_footer('home')		# call footer-home.php


add_theme_support
add_theme_support('post-formats');	
add_theme_support('post-thumbnails');
add_theme_support('custom-background');
add_theme_support('custom-header');
add_theme_support('menus');	 打开后台菜单项功能
add_theme_support('automatic-feed-links')
add_theme_support('html5')

#script/css
wp_register_script($handle, $src, )
wp_enqueue_script($handle)
```




```
__('####');
_e('####'); 多语言翻译

- http://codex.wordpress.org/zh-cn:函数参考
- http://codex.wordpress.org/zh-cn:模板标签Theme


//admin菜单
add_action('admin_menu', 'cat_menu');	//增加admin左侧菜单
function cat_menu(){
	add_menu_page($page_title, $menu_title, $capability, $menu_slug, $function, $icon_url, $position);		
	add_submenu_page($parent_slug, $page_title, $menu_title, $capability, $menu_slug, $function)
}




admin->post->edit->post_format
add_theme_support('post-format', array('', '', ''));
add_theme_support('post-thumbnails');
add_action('after_setup_theme', FunctionName);


//admin-> Appearance ->widget
register_sidebar(array('name'=>'First_sidebar'));   主题定义中出现小工具栏
register_sidebar(array(
	"name" => "",
	"id"      => "sidebar-1",
	"description" => ""
));
add_action('widgets_init', FunctionName);
在admin->Appearance->widget中向自己的sidebar中添加widget
在sidebar.php中调用
	dynamic_sidebar('sidebar-id')


register_nav_menus($location,  $description);	//description将出现在后台menu设置中
register_post_type
register_taxonomy

//js、css资源
wp_enqueue_style
wp_enqueue_scripts
add_action('init',   FunctionName)

//数据库查询
$wpdb->get_var(
	$wpdb->prepare("SELECT COUNT(ID) FROM {$wpdb->posts} WHERE post_status='publish' AND post_type='post' ")
);
$wpdb->get_results();
$wpdb->get_col();

//google代码
add_action('wp_footer', 'add_googleanalytics');
<?php function add_googleanalytics() {?>
	//放入google html/js代码
<?php } ?>

//favicon图标添加到header.php
或者添加到funcitons.php
function blog_favicon(){
	echo '<link rel="Shortcut Icon" type="image/x-icon" href=".get_bloginfo('wpurl').'/favicon.ico" />';
}
add_action('wp_header', 'blog_favicon');



//移除版本信息
function wpbeginner_remove_version(){
	return "";
}
add_filter('the_generator', 'wpbeginner_remove_version');
```







# 函数

#### wp_title
```
wp_title(string $sep='$raquo;', bool $display=true, string $seplocation='')
$sep
	how to separate the various items within the page title
$display
	whether to display or retrieve title
$seplocation
	direction to display title, 'right'
```

#### the_content
```
the_content(string $more_link_text=null, bool $strip_teaser = false)
$more_link_text
	content for when there is more text
$strip_teaser
	strip teaser content before the more text
```

#### comments_popup_link
```
comments_popup_link(string $zero = false, string $one = false, string $more = false, string $css_class = '', string $none = false)
$zero
	string to display when no comments
$one 
	string to display when only one comment
$css_class
	css class to use for comments
$none
	string to display when comments have been turned off
comments_popup_link( 'No comments yet', '1 comment', '% comments', 'comments-link', 'Comments are off for this post');
```


#### the_title
```
the_title(string $before = '', string $after = '', bool $echo = true)
$before
	content to prepend to the title
$after
	$content to append to the title
$echo
	whether to display or return
the_title( '<h3>', '</h3>' );
```

#### the_category
```
the_category(string $separator = '', string $parents = '', int $post_id = false)
$separator
	separator for between the categories
$parents
	how to display the parents
$post_id
	post id to retrieve categories
the_category( ', ' );
```

#### the_author
```
the_author(string $deprecated = '', string $deprecated_echo = true )
$deprecated
$deprecated_echo
	use the_get_author();
```

#### edit_post_link
```
edit_post_link($string $text = null, string $before = '', string $after = '', int $id)
$text
	anchor text
$before
	display before edit link
$after
	display after edit link
$id
	post id
```

#### get_links_list
```
get_links_list(string $order = 'name')
$order
	sort link categories by 'name' or 'id'
```

#### wp_list_pages
```
wp_list_pages(array|string $args = '')
$args
	array or string of arguments
'child_of'
	(int) Display only the sub-pages of a single page by ID. Default 0 (all pages).
'authors'
	(string) Comma-separated list of author IDs. Default empty (all authors).
'date_format'
	(string) PHP date format to use for the listed pages. Relies on the 'show_date' parameter. Default is the value of 'date_format' option.
'depth'
	(int) Number of levels in the hierarchy of pages to include in the generated list. Accepts -1 (any depth), 0 (all pages), 1 (top-level pages only), and n (pages to the given n depth). Default 0.
'echo'
	(bool) Whether or not to echo the list of pages. Default true.
'exclude'
	(string) Comma-separated list of page IDs to exclude.
'include'
	(array) Comma-separated list of page IDs to include.
'link_after'
	(string) Text or HTML to follow the page link label. Default null.
'link_before'
	(string) Text or HTML to precede the page link label. Default null.
'post_type'
	(string) Post type to query for. Default 'page'.
'post_status'
	(string) Comma-separated list of post statuses to include. Default 'publish'.
'show_date'
	(string) Whether to display the page publish or modified date for each page. Accepts 'modified' or any other value. An empty value hides the date.
'sort_column'
	(string) Comma-separated list of column names to sort the pages by. Accepts 'post_author', 'post_date', 'post_title', 'post_name', 'post_modified', 'post_modified_gmt', 'menu_order', 'post_parent', 'ID', 'rand', or 'comment_count'. Default 'post_title'.
'title_li'
	(string) List heading. Passing a null or empty value will result in no heading, and the list will not be wrapped with unordered list <code>&lt;ul&gt;</code> tags. Default 'Pages'.
'walker'
	(Walker) Walker instance to use for listing pages. Default empty (Walker_Page).
```

#### wp_list_categories
```
wp_list_categories(string|array $args = '')
$args
	'show_option_all' (string) - Text to display for showing all categories.
	'orderby' (string) default is 'ID' - What column to use for ordering the categories.
	'order' (string) default is 'ASC' - What direction to order categories.
	'show_count' (bool|int) default is 0 - Whether to show how many posts are in the category.
	'hide_empty' (bool|int) default is 1 - Whether to hide categories that don't have any posts attached to them.
	'use_desc_for_title' (bool|int) default is 1 - Whether to use the
```

#### next_post_link
```
next_post_link(string $format = '%link &raquo;', string $link = '%title', bool $in_same_term = false, array|string $excluded_terms = '', string $taxonomy = 'category' )
$format
	link anchor format
$link
	link permalink format
$in_same_term
	whether link should be in a same taxonomy term
$excluded_terms
	array or comma-separated list of excluded term IDs
$taxonomy
	taxonomy, if $in_same_term is true
```

#### previous_post_link
```
previous_post_link ( string $format = '&laquo; %link', string $link = '%title', bool $in_same_term = false, array|string $excluded_terms = '', string $taxonomy = 'category' )
$format
	link anchor format
$link 
	link permlink format
$in_same_term
	whether link should be in a same taxonomy term
$excluded_terms
	array of comma-separated list of excluded term IDs
$taxonomy
	taxonomy, if $in_same_term is true

get_calendar
get_calendar(bool $initial = true, bool $echo = true)
$initial
	use initial calendar names
$echo 
	set to false for return
```

#### wp_get_archives
```
wp_get_archives(string|array $args = '')
'type'
	(string) Type of archive to retrieve. Accepts 'daily', 'weekly', 'monthly', 'yearly', 'postbypost', or 'alpha'. Both 'postbypost' and 'alpha' display the same archive link list as well as post titles instead of displaying dates. The difference between the two is that 'alpha' will order by post title and 'postbypost' will order by post date. Default 'monthly'.
'limit'
	(string|int) Number of links to limit the query to. Default empty (no limit).
'format'
	(string) Format each link should take using the $before and $after args. Accepts 'link' (<code>&lt;link&gt;</code> tag), 'option' (<code>&lt;option&gt;</code> tag), 'html' (<code>&lt;li&gt;</code> tag), or a custom format, which generates a link anchor with $before preceding and $after succeeding. Default 'html'.
'before'
	(string) Markup to prepend to the beginning of each link.
'after'
	(string) Markup to append to the end of each link.
'show_post_count'
	(bool) Whether to display the post count alongside the link. Default false.
'echo'
	(bool|int) Whether to echo or return the links list. Default 1|true to echo.
'order'
	(string) Whether to use ascending or descending order. Accepts 'ASC', or 'DESC'. Default 'DESC'.
```


#### posts_nav_link
```
posts_nav_link ( string $sep = '', string $prelabel = '', string $nxtlabel = '' )
$sep
	separator for posts navigation links
$prelabel
	label for previous pages
$nxtlabel
	label for next pages
```

#### wp_register
```
wp_register ( string $before = '<li>', string $after = '</li>', bool $echo = true )
$before
	text to output before the link
$after
	text to output after the link
$echo 
	default to echo and not return the link

wp_loginout
wp_loginout ( string $redirect = '', bool $echo = true )
$redirect
	path to redirect to on login/logout
$echo 
	default to echo and not return the link
```


#### the_posts_pagination
```
the_posts_pagination(array $args=array())
```


#### wp_link_pages
```
wp_link_pages(string|array $args = '')
the formatted output  of a a list of pages
'before'
	(string) HTML or text to prepend to each link. Default is <code>&lt;p&gt; Pages:</code>.
'after'
	(string) HTML or text to append to each link. Default is <code>&lt;/p&gt;</code>.
'link_before'
	(string) HTML or text to prepend to each link, inside the <code>&lt;a&gt;</code> tag. Also prepended to the current item, which is not linked.
'link_after'
	(string) HTML or text to append to each Pages link inside the <code>&lt;a&gt;</code> tag. Also appended to the current item, which is not linked.
'next_or_number'
	(string) Indicates whether page numbers should be used. Valid values are number and next. Default is 'number'.
'separator'
	(string) Text between pagination links. Default is ' '.
'nextpagelink'
	(string) Link text for the next page link, if available. Default is 'Next Page'.
'previouspagelink'
	(string) Link text for the previous page link, if available. Default is 'Previous Page'.
'pagelink'
	(string) Format string for page numbers. The % in the parameter string will be replaced with the page number, so 'Page %' generates "Page 1", "Page 2", etc. Defaults to '%', just the page number.
'echo'
	(int|bool) Whether to echo or not. Accepts 1|true or 0|false. Default 1|true.
```

#### 条件标签

- [条件标签](http://codex.wordpress.org/zh-cn:条件标签)

```
is_home			//首页
is_front_page		
is_admin			//管理员面板
is_single			
is_single()
is_single('17')			#post id 17
is_single(17)
is_single('Irish Stew');		#post title Irish Stew
is_sticky				//文章置顶
is_sticky('17')			//id为17的文章置顶
is_comments_popup
comments_open	are comments allowed for current post
pings_open		
are pings allowed for current post
is_page
is_page()			#any page
is_page(42)			#page with post_id 42
is_page('Contact')		#page with post_title 'Contact'
is_page('about-me')		#page with post_name(slug)	'about-me'

is_category
is_category()
is_category('9')		#the archive page for category id 9
is_category('Stink')		#the archive page for category with title  'Stink'
is_category('blue-cheese')	#the archive page for category with slug 'blue-cheese'

is_tag
is_tag()
is_tag('9')
is_tag('name')
```

```
wp_head
function awd_add_header(){
	echo '<meta name="description" value="hello awd theme">';
}
add_action('wp_head', 'awd_add_header');
输出：<meta name="description" value="hello awd theme">

function awd_init_styles(){
	wp_enqueue_style('awd-styles', get_template_directory_uri() . "/main.css", '', '', 'all');
}
add_action('init', 'awd_init_styles');
输出：
<link rel="stylesheet" id="awd-styles-css" href="http://localhost/wp-content/themes/awd/main.css?ver=4.3.1" type="text/css" media="all">


add_action( 'wp_head',     'wlwmanifest_link' );
输出：
<link rel="wlwmanifest" type="application/wlwmanifest+xml" href="http://localhost/wp-includes/wlwmanifest.xml">
```









```
显示Next Page>>
<div class=“navigation”>
	<?php posts_nav_link(); ?>
</div>
posts_nav_link(' in between', ' before', ' after');
问题：如何自定义pagination 



输出category列表ul<li></li>ul
wp_list_categories();
wp_list_categories('sort_column=name&optioncount=1&hierarchial=0');
sort_column=name  - 把分类按字符顺序排列
optioncount=1          - 显示每个分类含有的日志数
hierarchial=0            - 不按照层次结构显示分类
问题：自定义


显示pages列表， ul<li></li>ul
wp_list_pages();
wp_link_page();

wp_get_archives();  => <li></li>
get_links_list();  已经废弃，使用wp_list_bookmarks();




wp_register();  => 输出admin链接
wp_loginout()  => 未登录输出登录链接，已登陆输出登出链接


//评论
comments_template();   ==> comments.php
<?php foreach($comments as $comment) : ?>
	<?php comment_author_link(); ?>
	<?php comment_text(); ?>
<?php endforeach; ?>


系统widget定义于wp-includes/default-widgets.php
自定义widget
class  Awd_Widget extends WP_Widget{
	function __construct(){

	}
	
	function widget($args, $instance) {
		//前台调用显示
	}

	function update($new_instance, $old_instance) {
		//后台保存
	}

	function form($instance) {
		//admin 中显示widget，拖动
	}
}

register_widget('Awd_Widget');

如何在widget函数中使用html
自定义的widget出现在哪里


$wpdb->get_col()
$wpdb->get_row()


nav menu
register_nav_menus(arrray());



调用代码
get_calendar()
get_category_post_list($num, $limit, $order='DESC')
```


# wordpress调试模式

```
wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);		#默认输出到wp-content/debug.log
define('WP_DEBUG_DISPLAY', true);	#再html中显示debug信息
define('SCRIPT_DEBUG', true);		#不再压缩css/js等脚本
define('SAVEQUERIES', true);		#保存每一次的数据库查询




wp-settings.php中打开日志，指定日志文件
@ini_set('log_errors', 'On');
@ini_set('display_errors', 'Off');
@ini_set('error_log', '/var/www.html/test.com/logs/erorr.log');
```


# 文件

```
wp-includes/default-filters.php中			//index.php - get_header(); -> header.php ->do_action('wp_head')
	add_action('wp_head','')
	add_action('wp_head', '')
wp-includes/ms-default-filters.php

wp-includes/general-templates.php
	get_header();
	get_footer();
	get_sidebar();	
	wp_title();
	bloginfo();
author-template.php
	get_the_author();
	get_the_author_meta();
	get_the_author_posts();
	wp_list_authors();
bookmark-template.php
	wp_list_bookmars();
category-template.php
	
comment-template.php
link-template.php
media-template.php
nav-menu-template.php
post-template.php
	get_ID()
	the_title();
	body_class();
	the_meta();
	

wp-includes/theme.php
	wp_get_themes()
	is_child_theme();
	get_stylesheet();
	get_template();
	header_image();
	wp_customize_url();
	is_customize_preview();
	
wp-includes/detault-filters.php
	add_filter($filter_name, $myfunction)
	apply_filter($tilter_name, $args_to_myfunction);
```

# 资源

- [wordpress.com](www.wordpress.com)
- [wordpress.org](www.wordpress.org)
- [主题](www.wordpress.org/themes)		
- [文档](http://codex.wordpress.org)		
- [中文文档](http://codex.wordpress.org.cn)
- [视频(收费)](www.wordpress.tv)			

- [乱炖](http://levi.cg.am/)			
- [露兜](http://www.ludou.org)			
- [wordpress大学](http://www.wpdaxue.com/)		

- [修改文件顺序](http://codex.wordpress.org/Template_Hierarchy#Page_display)





# 翻页代码

```
function my_content_nav() {
	global $wp_query, $wp_rewrite;

	$paged = ( get_query_var( 'paged' ) ) ? intval( get_query_var( 'paged' ) ) : 1;

	$pagenum_link = html_entity_decode( get_pagenum_link() );
	$query_args = array();
	$url_parts = explode( '?', $adminsm_link );

	if ( isset( $url_parts[1] ) ) {
		wp_parse_str( $url_parts[1], $query_args );
	}
	$pagenum_link = remove_query_arg( array_keys( $query_args ), $pagenum_link );
	$pagenum_link = trailingslashit( $pagenum_link ) . '%_%';

	$format = ( $wp_rewrite->using_index_permalinks() AND ! strpos( $pagenum_link, 'index.php' ) ) ? 'index.php/' : '';
	$format .= $wp_rewrite->using_permalinks() ? user_trailingslashit( 'page/%#%', 'paged' ) : '?paged=%#%';

	$links = paginate_links( array(
		'base' => $pagenum_link,
		'format' => $format,
		'total' => $wp_query->max_num_pages,
		'current' => $paged,
		'mid_size' => 3,
		'type' => 'list',
		'add_args' => array_map( 'urlencode', $query_args )
	) );

	if ( $links ) {
		echo "<nav class=\"pagination pagination-centered clearfix\">{$links}</nav>";
	}
}
<?php my_content_nav();?>
```


# 加载js/css脚本
正确加载 Javascript 和 CSS 到 WordPress
正确加载 jQuery、Javascript 和 CSS 到你的WordPress网站也许是一件比较痛苦的事情。 本文将讲解如何使用WordPress官方推荐的方式来加载脚本/ CSS。

有两种常用的 add_action 钩子可以加载 脚本和CSS到WordPress：

init： 确保始终为您的网站头部加载脚本和CSS（如果使用home.php，index.php或一个模板文件），以及其他"前端"文章、页面和模板样式。
wp_enqueue_scripts："适当"的钩子方法，并不总是有效的，根据你的WordPress设置。
下面的所有例子都在WordPress多站点模式、WordPress 3.4.2 通过测试（如果不支持后续版本，请留言告知）

加载外部 jQuery 库和主题自定义的脚本、样式

下面这个例子在 add_action 钩子中使用 init。使用 init 有两个原因，一是因为我们正在注销WordPress默认的jQuery库，然后加载谷歌的jQuery库；二是确保在WordPress的头部就加载脚本和CSS。

使用if ( !is_admin() )是为了确保这些脚本和css只在前端加载，不会再后台管理界面加载。

/** Google jQuery Library, Custom jQuery and CSS Files */  
function myScripts() {  
        wp_register_script( 'google', 'http://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.js' );  
        wp_register_script( 'default', get_template_directory_uri() . '/jquery.js' );  
        wp_register_style( 'default', get_template_directory_uri() . '/style.css' );  
    if ( !is_admin() ) { /** Load Scripts and Style on Website Only */  
        wp_deregister_script( 'jquery' );  
        wp_enqueue_script( 'google' );  
        wp_enqueue_script( 'default' );  
        wp_enqueue_style( 'default' );  
    }  
}  
add_action( 'init', 'myScripts' );
加载WP默认 jQuery 库和主题自定义的脚本、样式

第3行：使用 array('jquery') 是为了告诉 WordPress 这个 jquery.js 是依赖WordPress 的jQuery库文件，从而使 jquery.js 在WordPress jQuery库文件后加载。

/** Add Custom jQuery and CSS files to a Theme */  
function myScripts() {  
        wp_register_script( 'default', get_template_directory_uri() . '/jquery.js', array('jquery'), '' );  
        wp_register_style( 'default', get_template_directory_uri() . '/style.css' );  
    if ( !is_admin() ) { /** Load Scripts and Style on Website Only */  
        wp_enqueue_script( 'default' );  
        wp_enqueue_style( 'default' );  
    }  
}  
add_action( 'init', 'myScripts' );
加载 print.css 到你的WordPress主题

第 3 行：最后的 'print'是媒体屏幕调用，确保 print.css 在网站的打印机中的文件加载时才加载。

/** Adding a Print Stylesheet to a Theme */  
function myPrintCss() {  
        wp_register_style( 'print', get_template_directory_uri() . '/print.css', '', '', 'print' );  
    if ( !is_admin() ) { /** Load Scripts and Style on Website Only */  
        wp_enqueue_style( 'print' );  
    }  
}  
add_action( 'init', 'myPrintCss' );
使用 wp_enqueue_scripts 替换 init

如果你要在文章或页面加载唯一的脚本，那就应该使用 wp_enqueue_scripts 替换 init。使用 wp_enqueue_scripts 仅仅只会在前台加载脚本和CSS，不会在后台管理界面加载，所以没必要使用 !is_admin() 判断。

使用 is_single() 只在文章加载脚本或CSS

第 3 行的 # 替换为文章的ID就可以让脚本和css只加载到那篇文章。当然，如果直接使用 is_single() （不填ID），就会在所有文章加载脚本和CSS。

/** Adding Scripts To A Unique Post */  
function myScripts() {  
    if ( is_single(#) ) { /** Load Scripts and Style on Posts Only */  
        /** Add jQuery and/or CSS Enqueue */  
    }  
}  
add_action( 'wp_enqueue_scripts', 'myScripts' );
使用 is_page() 只在页面加载脚本或CSS

第 3 行的 # 替换为页面的ID就可以让脚本和css只加载到那个页面。当然，如果直接使用 is_single() （不填ID），就会在所有页面加载脚本和CSS。

/** Adding Scripts To A Unique Page */  
function myScripts() {  
    if ( is_page(#) ) { /** Load Scripts and Style on Pages Only */  
        /** Add jQuery and/or CSS Enqueue */  
    }  
}  
add_action( 'wp_enqueue_scripts', 'myScripts' );
使用 admin_enqueue_scripts 加载脚本到后台

这个例子将在整个后台管理界面加载脚本和CSS。这个方法不推荐用在插件上，除非插件重建了整个后台管理区。

第 10 行使用 admin_enqueue_scripts 替换了 init 或 wp_enqueue_scripts

第 5、6 行，如果你要自定义后台管理区，你可以需要禁用默认的WordPress CSS调用。

/** Adding Scripts To The WordPress Admin Area Only */  
function myAdminScripts() {  
    wp_register_script( 'default', get_template_directory_uri() . '/jquery.js', array('jquery'), '' );  
    wp_enqueue_script( 'default' );  
    //wp_deregister_style( 'ie' ); /** removes ie stylesheet */  
    //wp_deregister_style( 'colors' ); /** disables default css */  
    wp_register_style( 'default', get_template_directory_uri() . '/style.css',  array(), '', 'all' );  
    wp_enqueue_style( 'default' );  
}  
add_action( 'admin_enqueue_scripts', 'myAdminScripts' );
加载脚本和CSS到WordPress登录界面

第 6 行：我无法弄清楚如何在在登录页面注册/排序 CSS文件，所以这行手动添加样式表。

第 10-14行：用来移除WordPress默认的样式表。

/** Adding Scripts To The WordPress Login Page */  
function myLoginScripts() {  
    wp_register_script( 'default', get_template_directory_uri() . '/jquery.js', array('jquery'), '' );  
    wp_enqueue_script( 'default' );  
?>  
    <link rel='stylesheet' id='default-css' href='<?php echo get_template_directory_uri() . '/style.css';?>' type='text/css' media='all' />  
<?php }  
add_action( 'login_enqueue_scripts', 'myLoginScripts' );  
/** Deregister the login css files */  
function removeScripts() {  
    wp_deregister_style( 'wp-admin' );  
    wp_deregister_style( 'colors-fresh' );  
}  
add_action( 'login_init', 'removeScripts' );
加载脚本和CSS到WordPress插件

WordPress插件加载脚本和CSS也是常见的。主要的不同之处在于文件的 URL。主题使用的是 get_template_directory_uri ，而插件应该用 plugins_url ，因为文件是从插件目录进行加载的。

从插件加载脚本和CSS

这个例子将在整个网站前端加载脚本和CSS。

/** Global Plugin Scripts for Outside of Website */  
function pluginScripts() {  
    wp_register_script( 'plugin', plugins_url( 'jquery.js' , __FILE__ ), array('jquery'), '' );  
    wp_register_style( 'plugin', plugins_url( 'style.css' , __FILE__ ) );  
    if ( !is_admin() ) { /** Load Scripts and Style on Website Only */  
        wp_enqueue_script( 'plugin' );  
        wp_enqueue_style( 'plugin' );  
    }  
}  
add_action( 'init', 'pluginScripts' );
从插件加载脚本和CSS到后台管理区

如果你需要在整个后台管理区加载脚本和CSS，就使用 admin_enqueue_scripts 替换 init。

/** Global Plugin Scripts for The WordPress Admin Area */  
function pluginScripts() {  
    wp_register_script( 'plugin', plugins_url( 'jquery1.js' , __FILE__ ), array('jquery'), '' );  
    wp_enqueue_script( 'plugin' );  
    wp_register_style( 'plugin', plugins_url( 'style1.css' , __FILE__ ) );  
    wp_enqueue_style( 'plugin' );  
}  
add_action( 'admin_enqueue_scripts', 'pluginScripts' );
从插件加载脚本和CSS到插件设置页面

例子只会加载所需的脚本和CSS到插件设置页面，不会在管理区的其他页面加载。

第 3 行：自定义 page= 后面的值为你的插件设置页面

/** Adding Scripts On A Plugins Settings Page */  
function pluginScripts() {  
    if ( $_GET['page'] == "plugin_page_name.php" ) {  
        wp_register_script( 'plugin', plugins_url( 'jquery.js' , __FILE__ ), array('jquery'), '' );  
        wp_enqueue_script( 'plugin' );  
        wp_register_style( 'plugin', plugins_url( 'style.css' , __FILE__ ) );  
        wp_enqueue_style( 'plugin' );  
    }  
}  
add_action( 'admin_enqueue_scripts', 'pluginScripts' );
将 jQuery 库移动到页脚

你不能将WordPress默认的jQuery 库移动到页面底部，但是你可以将自定义的jQuery 或其他外部jQuery 库（比如Google的）移动到底部。不要将CSS移动到页面底部。

第 3、4 行：最后的 'true'告诉WordPress在页面底部加载这些脚本。

/** Moves jQuery to Footer */  
function footerScript() {  
        wp_register_script('jquery', ("http://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.js"), false, '', true );  
        wp_register_script( 'default', get_template_directory_uri() . '/jquery.js', false, '', true );  
    if ( !is_admin() ) { /** Load Scripts and Style on Website Only */  
        wp_deregister_script( 'jquery' );  
        wp_enqueue_script( 'jquery' );  
        wp_enqueue_script( 'default' );  
    }  
}  
add_action( 'init', 'footerScript' );
根据不用的用户角色和功能加载jQuery和CSS

如果你的网站有作者、编辑和其他管理员，你可能需要通过 jQuery 来为他们显示不同的信息。你需要使用 current_user_can 确定登录的用户的 角色和功能 。

下面三个例子中，如果用户已经登录，将在整个网站加载这些脚本和CSS。使用 !is_admin() 包装 enqueue_script 确保只在前台加载，或者在 add_action 使用 admin_enqueue_scripts 就可以确保只在后台管理区加载。

为可以"编辑文章"的管理员加载脚本和CSS

只对超级管理员和网站管理员生效

/** Add CSS & jQuery based on Roles and Capabilities */  
function myScripts() {  
    if ( current_user_can('edit_posts') ) {  
        /** Add jQuery and/or CSS Enqueue */  
    }  
}  
add_action( 'init', 'myScripts' );
为所有登录用户加载脚本和CSS

/** Admins / Authors / Contributors /  Subscribers */  
function myScripts() {  
    if ( current_user_can('read') ) {  
        /** Add jQuery and/or CSS Enqueue */  
    }  
}  
add_action( 'init', 'myScripts' );
为管理员以外的已登录用户加载脚本和CSS

/** Disable for Super Admins / Admins enable for Authors / Contributors /  Subscribers */  
function myScripts() {  
    if ( current_user_can('read') && !current_user_can('edit_users') ) {  
        /** Add jQuery and/or CSS Enqueue */  
    }  
}  
add_action( 'init', 'myScripts' );
最后的提示

上面的例子如果使用相同的add_action，就可以被合并成一个单一的函数。 换句话说，您可以使用多个 if 语句在一个函数中分裂了你的脚本和CSS调用，如：if_admin！if_admin，is_page，is_single和current_user_can的，因为每次使用相同的add_action的init。

原文：http://technerdia.com/1789_include-jquery-css.html
编译：倡萌@WordPress大学









```
get_categories
get_category($ID | $slug)
get_category_link($ID)

get_the_category_list(',')		current post cat，输出a，如无参数输出ul-li-a
get_the_term_list($post->ID, )

comments_popup_link('0 条评论', '1 条评论', '% 条评论', '评论已关闭');		输出a
wordpress基本模版文件
Loop循环
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
<?php endwhile; else: ?>
  <p><?php _e('Sorry, no posts matched your criteria.'); ?></p>
<?php endif; ?>
```




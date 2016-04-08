---
layout:     post
title:      "laravel"
subtitle:   " \"all about laravel\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - web
    - php
---
## laravel
Laravel
基于composer包管理，composer.json；基于symfony

laravel new my_project_name
composer install

php artisan
命令行
php artisan list			#列出所有命令
php artisan key:generate 		#生成key
php artisan serve 			#开启服务器
make:controller 
make:event
make:job	
make:listener
make:middleware
make:migration			#create new migration file
make:model
make:provider
make:request
make:seeder

migrate:install 			#等同于rails db:create
migrate:refresh
migrate:rollback
migrate:status

app:name
cache:table
db:seed			
route:list				#列出所有route
session:table				#在数据库中生成session表

使用generators
"require-dev": {
    "way/generators": "~2.0"
},
就可以使用类似rails的命令
generate:model
generate:view
generate:controller
generate:seed
generate:migration
generate:resource
generate:scaffold


配置文件：config/app.php




composer 国内镜像
在composer.json中增加如下代码：
{
    "repositories": [
        {   
            "packagist": false
        },  
        {   
            "type": "composer", 
            "url": "http://packagist.cn"
        }   
    ]
}

composer update -vvv

Route规则
4.0: app/routes.php
5.0: app/Http/routes.php

//基础
Route::get(‘/’, function() { return ‘this string is returned’;});
Route::post(‘foo/bar’, function() { return ‘sadfasdfasdf’ ;} );
Route::match([‘get’, ‘post’], ‘url’, function() {});
Route::any();

$url = url(‘for/bar’);

//带参数
Route::get('user/{id}', function ($id) {
    return 'User '.$id;
});
// 可选的参数
Route::get('user/{name?}', function ($name = null) {
    return $name;
});
//正则表达式参数
Route::get('user/{name}', function ($name) {
    //
})
->where('name', '[A-Za-z]+');
//全局正则表达式
//在RouteServiceProvider.php 的boot函数中定义
public function boot(Router $router)
{
    $router->pattern('id', '[0-9]+');

    parent::boot($router);
}



//命名Route
Route::get('user/profile', ['as' => 'profile', function () {
    //
}]);

Route::get('user/profile', [
    'as' => 'profile', 'uses' => 'UserController@showProfile'
]);


$redirect = redirect()->route(‘profile');

///////////////带参数route
Route::get('user/{id}/profile', ['as' => 'profile', function ($id) {
    //
}]);

$url = route('profile', ['id' => 1]); 

//route 组
//middleware
Route::group(['middleware' => 'auth'], function () {
    Route::get('/', function () {
        // Uses Auth Middleware
    });

    Route::get('user/profile', function () {
        // Uses Auth Middleware
    });
});

//namespaces
Route::group(['namespace' => 'Admin'], function()
{
    // Controllers Within The "App\Http\Controllers\Admin" Namespace

    Route::group(['namespace' => 'User'], function()
    {
        // Controllers Within The "App\Http\Controllers\Admin\User" Namespace
    });
});

//sub-domain routing
Route::group(['domain' => '{account}.myapp.com'], function () {
    Route::get('user/{id}', function ($account, $id) {
        //
    });
});


//route 前缀
Route::group(['prefix' => 'admin'], function () {
    Route::get('users', function () {
        // Matches The "/admin/users" URL
    });
});

//csfr protection
  //introduction
  //excluding uris
  //x-csrf-token
  //x-xsrf-token
//from method spoofing
//throw 404


//命名路由器， filter & acton
Route::get(‘user/profile’, array(‘as’ => ‘profile’, ‘before’ => ‘old’, ‘uses’ => ‘UserController@showProfile'));

//<1>Controler Action
Route::get('a', 'ArticleController@index’);

Route::get(‘/‘,  function(){
	echo "work";				//<2>直接输出

	echo Form::open();
	echo Form::close();

	return View:make(‘login’);	//<3>输出login.blade.php
});


Route::post(‘login’, function(){
	$name = Input::get(‘username’);	//获得username框数值

	Redirect::to(‘login’);		
	Redirect::route(‘login’);	
});





//Auth
if(Auth::attempt(array(‘username’ => $name, ‘password’ => $password)); //用户验证
Auth::check()		//判断用户是否已经验证
Auth::user()->email	//当前用户email
Auth::validate()	//验证但不登录
Auth::logout();//数据库定义
php artisan migrate:make final_table 
	//编辑好所有的数据库脚本
	Schema::create(‘posts’, function($table){
		$table->increments(‘id’);
			  ->string($column)
			  ->string($column, $length)
			  ->integer($column)
			  ->float($column)
			  ->decimal($column, $precision, $scale)
			  ->boolean($column)
			  ->text($column)
			  ->blob($column)
			 ->binary($column)
			 ->dateTime($column)
			 ->timestamp($column)
			 ->time($column)
			 ->enum($column, array $allowed)
			 ->timestamps()
			 ->nullable()
			 ->default($value)
			 ->unsigned()

		$table->foreign(‘user_id’)->references(‘id')->on(‘users')->onDelete(‘cascade');
	});

	Schema::create()
	Schema::drop()
	Schema::rename($to)
	Schema::dropColumn(columns)
	Schema::dropColumns()
	Schema::primary($columns, $name = null)
	Schema::unique($columns, $name = null)
	Schema::index($columns, $name = null)
	Schema::foreign($columns, $name = null)
	Schema::dropPrimary($index = null)
	Schema::dropUnique($index)
	Schema::dropIndex($index)
	Schema::dropForeightn($index)
	
//Model
<?php 
class Post extends Eloquent{
	protected $table = ‘’my_users’;	//Model 的表名	
	protected $fillable = [];			//指定哪些属性可以被集体赋值
        protected $guarded = [];			//指定哪些属性不可以被集体赋值

	public function user(){
		return->belongsTo(‘User’);
	}
}

//query
$posts = Post::all();   	//获取全部
$post = Post::find(1);	//id == 1
$post = Post::findOrFail(1);
$post = Post:;where(‘votes’, ‘>’ 100)->firstOrFail();
$posts = Post::where(‘votes’, ‘>’, 100)->take(10)->get();
$count = Post::where(‘vote’, ‘<‘, 100)->count();



//注册错误处理，
App::error(function(ModelNotFoundException $e){
	return Response::make(‘Not Found’, 404);
});



//insert / update
$user = new User;
$user->name = ‘John’;
$user->save();


$affectedRows = Post::where(‘votes’, ‘>’, 100)->update(array(’status’ => 2));		//在一组模型上更新


//关系
hasOne(‘Phone’);	//一对一
belongsTo(‘User’);l	//逆向关系

hasmany(‘Comment’)	//一对多
belongsTo(‘Post’)		//逆向关系

belongsToMany(‘Role’)	//多对多
belongsToMany(‘User’)	//逆向关系


















################################################################
balde.php模版
################################################################

//Form
{{ Form::open(array(‘url' => ‘foo/bar') ) }}			//要提交到view的url
{{ Form::open(array(‘route' => ‘route.name') ) }} 	//要提交到的route
{{ Form::open(array(‘action’ => ‘Controller@method') ) }} 		//要提交到的actoin
{{ Form::open(array(‘url’ => ‘foo/bar’, ‘files’ => true)) }}			//允许在表单中提交文件

echo Form::lable(‘emai’, ‘E-Mail Adress’, array(‘class’ => ‘awesome’ ) );	//文本显示
echo Form::text(‘email’, ‘example@gmail.com’);						//获取文本
echo Form::password(‘password’);
echo Form:;checkbox(’name’,  ‘value’);
echo Form::radio(’name’,  ‘value’);
echo Form::file(‘image’);						//文件上传
echo Form::select(’size’, array(‘L’ => ‘Large’, ’S’ => ’Small’ ) );
echo Form::submit(‘Click Me!’);

{{ From::close() }}



//HTML
{{ HTML::link(’assets/images/favicon-32.png’,  [’size’=>’32*32’] )}}			此处都是指public目录下的资源
{{ HTML::style('assets/libraries/bootstrap/css/bootstrap.min.css') }}
{{ HTML::script('assets/libraries/respond.min.js') }}
{{ HTML::image(’image/example.jpg’, ’this is alt’) }}
{{ HTML::linkAsset(ur) }}
{{ HTML::linkRoute(name) }}
{{ HTML::linkActioin }}
{{ HTML::mailto }}
{{ HTML::ol }}
{{ HTML::ullistinglistingElement }}
{{ HTML::nestedListing }}
{{ HTML::attributes }}
{{ HTML::attributeElement }}





<a href="{{ route('dashboard') }}">Dashboard</a>
<a href="{{ URL::to(‘user/login') }}" ——>view/user/login.blade.php
<img src="{{ asset('assets/images/logo.png') }} "/>




//语法
@include(‘layout.header’) layout/header.blade.php

//Layout
//app/viess/layouts/master.balde.php
@section(’sidebar’)
This is the master sidebar.
@show
@yeild(‘content’, ‘Default Content') /空section，等待子view填充

//app/views/subview.blade.php
@	(‘layouts.master’) //扩展
@section(’sidebar’) //覆盖父sidebar secton
@parent
This is appended to the master sidebar.
@stop
@seciotn(‘content’) 填充content secton
this is subview body content
@stop

//注释
{{— —}}  
<!— —>注释方法会在html中渲染输出


{{ $name }}
{{ isset($name) ?name : ‘Defaut'   }}
{{ $name or ‘Default' }}

//if
@if ()
@elseif
@else
@endif


//unless
@unless()
@endunless


//for
@for($i = 0; $i < 10; $i++)
@endfor

@foreach ($posts as $post)
@endforeach

@while(true)
@endwhile



################################################################
帮助
################################################################
json_encode
json_decode

Response::json($data);
Response::download($file);



################################################################
laraval new my-project//创建项目
composer install //安装项目依赖包
composer update

php artisan key:generate    //创建key
php artisan migrate:make users_table //创建migrate文件
php artisan migrate //按照migration文件修改数据库
php artisan db:seed //插入数据库测试数据，seed文件中
php artisan controller:make UserController
php artisan bundle:install bundle-name

//重置密码
//需要User implements Remindableinterface
php artisan auth:reminders-table
php artisan auth:reminders-controller



Laravel Generator
generate:migration create_post_table	//生成migrate文件
	关键词：create、add、delete、drop
generate:migration create_post_table --fields="username:string(30):unique, 									   age:integer:nullable:default(18)"


generate:model Post		//app/model/Post.php
generate:view admin.reports.index //app/view/admin/reports/index.blade.php

generate:seed users             //app/database/seeds/UsersTableSeeder.php
generate:pivot orders users     //user及order的连接表

generate:resource post --fields="title:string, body:text"
	//生成model,views,controller, migrate, seed,再migrate到数据库
generate:scaffold
generate:controller


====================================================
config/app.config
	debug = true 打开调试


//自定义错误页面
app/start/global.php
App::error(function($exception, $code)
{
    switch ($code)
    {
        case 403:
            return Response::view('errors.403', array(), 403);
        case 404:
            return Response::view('awd.404', array(), 404);
        case 500:
            return Response::view('errors.500', array(), 500);
        default:
            return Response::view('errors.default', array(), $code);
    }
});






====================================================
Laravel 可用package
	http://packalyst.com/
	https://packagist.org/
加入composer.json

====================================================
laravel 开源项目
driesvints.com
fideloper.com
invoice-ninja
kk7.com
LaBlog
laravel-bookmark
laravel-tricks
Laravel.fr
LaravelIO
Queiroz
slovenianGooner
snipe-it
wardrobe
Route
Route::get(‘/’, function(){
	return ‘string’;
});

Route::post(‘/url’, function(){    });
Route::put(‘/url’, function(){      });
Route::delete(‘/url’, function() { });

Route::match([‘get’, ‘post’], ‘/url’, function() { });
Route::any(‘url’, function() { });


//使用参数
Route::get(‘user/{id}’, function($id){   });
Route::get(‘posts/{post}/comments/{comment}’,  function($postId, $commentId) {   });


Route::get(‘user/{name?}’, function($name = null) {  });
Route::get(‘user/{name?}’, function($name = ‘John’ ) {  });

//约束参数中format
Route::get(‘user/{name}’, function($name) {})->where(‘name’, ‘[A-Za-z]+’);
Route::get(‘user/{id}’, function($id){ })->where(‘id’, ‘[0-9]+’);
Route::get(‘user/{id}/{name}, function($id, $name) {})->where([‘id’ => ‘[0-9]+’, ‘name’ => ‘[z-a]+’]);

//为route命名
Route::get(‘user/profile’, [‘as’ => ‘profile’, function() {}]);
Route::get(‘user/profile’, [‘as’  => ‘profile’,  ‘users’ => ‘UserController@showProfile’ ]);

//grpu url
Route::group(['as' => 'admin::'], function () {
    Route::get('dashboard', ['as' => 'dashboard', function () {
        // Route named "admin::dashboard"
    }]);
});


//Middleware
Route::group(['middleware' => 'auth'], function () {
    Route::get('/', function () {
        // Uses Auth Middleware
    });

    Route::get('user/profile', function () {
        // Uses Auth Middleware
    });
});




//中间件Middleware
php artisan make:middleware OldMiddleware
app/Http/Middleware

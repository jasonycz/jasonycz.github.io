---
layout:     post
title:      "Introduction of  Laravel"
subtitle:   "Php Framework Laravel"
date:       2017-09-02 16:59:42
author:     "Jasonycz"
header-img: "img/post-php-laravel.jpg"
tags:
    - Php
---

###   Laravel 简介
- [官网](http://www.golaravel.com/)

###   技术优势 
 - 语法优雅、可读性好 
  I- MbdTech::all();  MbdTech::where('id',1)->get()->toArray();
 - 使用composer进行包管理
   - 优点：方便管理依赖的包（版本控制）
 - migration: 数据库迁移
 - ORM:对象关系映射
 - RESTful Routing
   - Laravel拥有类似于Ruby on Rails的，快速、高效的路由系统。
 - 完善的测试机制
 - artisan 命令行执行

###   技术劣势
 - 门槛高
 - 设计复杂
 - 速度慢（需要实例化特别多的对象）（lumen速度大幅度提升 Lumen 是你构建微服务架构和 API 应用的完美解决方案, 事实上, 她是全宇宙最快的框架之一, 甚至要快过以速度著称的 Silex 和 Slim）
 
###     不适用的场景
- 一些工作量不大的项目或者产品。
- 特别强调运行效率的项目或者产品,像WEB2.0网站就是这种情况。

#### 目录结构

![](http://ohn332hz8.bkt.clouddn.com/a6f8f3801dcfd9871f96e78716e1063f)

顶级文件 | 作用 |
-------|-----|
app | 应用的核心代码，用户编写的代码 定时任务、事件、异常、控制器、模型、监听器、中间件|
bootstrap | 框架的启动和自动载入配置，还有一个cache文件夹用于包含框架为提升性能所生成的文件，如路由和服务缓存文件 |
config | 配置相关 app 数据库 日志 ... 包含大量的用来更改框架的各个方面的配置文件。大部分的配置文件中返回的选项关联PHP数组。|
database | 数据迁移及填充  |
public | 入口文件index.php和前端资源文件（图片、JavaScript、CSS等)|
resource | 视图文件及原生资源文件（LESS、SASS、CoffeeScript），以及本地化文件(lang)|
routes | 路由相关  web.php、api.php和console.php [^1] |
vendor | Composer依赖（包括laravel源码） |
storage | 包含编译过的Blade模板、基于文件的session、文件缓存，以及其它由框架生成的文件，该目录被细分为成app、framework和logs子母录，app目录用于存放应用要使用的文件，framework目录用于存放框架生成的文件和缓存，logs目录包含应用的日志文件|
Tests | 自动化测试，包含PHPUnit示例；每一个测试类都要以 Test 开头，你可以通过 phpunit 或 php vendor/bin/phpunit 命令来运行测试。

更详细的参看文档：[laravel 5.3](http://laravelacademy.org/laravel-docs-5_3)


[^1]: http://laravelacademy.org/post/5762.html 1)web.php文件包含的路由都会应用web中间件组，具备Session、CSRF防护以及Cookie加密功能，如果应用无需提供无状态的、RESTful风格的API，所有路由都会定义在web.php文件 2)api.php 文件包含的路由应用了api中间件组，具备频率限制功能，这些路由是无状态的，所以请求通过这些路由进入应用需要通过token进行认证并且不能访问Session状态 3)console.php 文件用于定义所有基于闭包的控制台命令，每个闭包都被绑定到一个控制台命令并且允许与命令行IO方法进行交互，尽管这个文件并不定义HTTP路由，但是它定义了基于控制台的应用入口（路由）

###   Laravel生命周期

#### php生命周期

php有两种运行模式

- WEB模式 
- CLI（命令行）模式。

当我们在终端敲入php这个命令的时候，使用的是CLI模式；
当使用Nginx或者别web服务器作为宿主处理一个到来的请求时，会调用Php运行，此时使用的是WEB模式。
当我们请求一个Php文件时，比如Laravel 的public\index.php文件时，Php 为了完成这次请求，会发生5个阶段的生命周期切换：

1. 模块初始化（MINIT），即调用`php.ini`中指明的扩展的初始化函数进行初始化工作，如`mysql`扩展。
2. 请求初始化（RINIT），即初始化为执行本次脚本所需要的`变量名称`和`变量值内容的符号表`，如`$_SESSION`变量。
3. 执行该PHP脚本。
4. 请求处理完成(Request Shutdown)，按顺序调用各个模块的RSHUTDOWN方法，对每个变量调用`unset`函数，如`unset $_SESSION`变量。
5. 关闭模块(Module Shutdown) ， PHP调用每个扩展的MSHUTDOWN方法，这是各个模块最后一次释放内存的机会。这意味着没有下一个请求了。

WEB模式和CLI 区别？

![](http://ohn332hz8.bkt.clouddn.com/ede47a2f1839811679620185912a04ca)

**ps**

- php的`singleton`只是在某一次请求过程中的`singleton`；
- php 中的静态变量也不能在多个请求之间共享
- 每一次请求结束都会`unset`

*java 呢？ 那如果要实现 不同次请求之间的 静态变量共享应该怎么做？*

符号表是一种用于语言翻译器（例如编译器和解释器）中的数据结构。在符号表中，程序源代码中的每个标识符都和它的声明或使用信息绑定在一起，比如其数据类型、作用域以及内存地址。符号表在编译程序工作的过程中需要不断收集、记录和使用源程序中一些语法符号的类型和特征等相关信息。这些信息一般以表格形式存储于系统中。如常数表、变量名表、数组名表、过程名表、标号表等等，统称为符号表。对于符号表组织、构造和管理方法的好坏会直接影响编译系统的运行效率。


WEB模式和CLI（命令行）模式很相似，区别是：CLI 模式会在每次脚本执行经历完整的5个周期，因为你脚本执行完不会有下一个请求；而WEB模式为了`应对并发`，可能采用`多线程`，因此生命周期`1`和`5`有可能只执行一次，下次请求到来时重复`2-4`的生命周期，这样就节省了系统模块初始化所带来的开销。



###  laravel生命周期

Laravel 的生命周期从`public\index.php`开始，从`public\index.php`结束。

![](http://ohn332hz8.bkt.clouddn.com/b17eb5da23ea1ebe7a91e8d9db3f7644)

如下：
![](http://ohn332hz8.bkt.clouddn.com/90c45e55a0db45bbc21d1671e59dd01b)

public\index.php中源码:

- 注册加载composer自动生成的class loader，包括所有你composer require的依赖 autoload_static;autoload_namespaces; autoload_psr4;autoload_classmap

```
require __DIR__.'/../bootstrap/autoload.php';
```
- 生成容器`Container`，`Application 实例`，并向容器注册核心组件（`HttpKernel`，`ConsoleKernel`，`ExceptionHandler`）检测环境，加载配置，注册Facades（假象），注册服务提供者，启动服务提供者
```
- $app = require_once __DIR__.'/../bootstrap/app.php';
- $kernel = $app->make(Illuminate\Contracts\Http\Kernel::class);
```
- 处理请求，生成并发送响应.

```
捕获请求，生成Illuminate\Http\Request实例，传递给handle方法。
传递给路由是通过`Pipeline`来传递的，但是`Pipeline`有一堵墙，在传递给路由之前所有请求都要经过，这堵墙定义在`app\Http\Kernel.php`中的`$middleware`数组中(中间件)，默认只有一个CheckForMaintenanceMode中间件，用来检测你的网站是否暂时关闭。然后遍历所有注册的路由，找到最先符合的第一个路由，经过它的路由中间件，进入到控制器或者闭包函数，执行你的具体逻辑代码。
```
    protected $middleware = [
        \Illuminate\Foundation\Http\Middleware\CheckForMaintenanceMode::class,
    ];
   	protected $middlewareGroups = [
        'web' => [
            \App\Http\Middleware\EncryptCookies::class,
            \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
            \Illuminate\Session\Middleware\StartSession::class,
            \Illuminate\View\Middleware\ShareErrorsFromSession::class,
            \App\Http\Middleware\VerifyCsrfToken::class,
            \Illuminate\Routing\Middleware\SubstituteBindings::class,
        ],

        'api' => [
            'throttle:60,1',
            'bindings',
        ],
    ];
    protected $routeMiddleware = [
        'auth' => \Illuminate\Auth\Middleware\Authenticate::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
        'bindings' => \Illuminate\Routing\Middleware\SubstituteBindings::class,
        'can' => \Illuminate\Auth\Middleware\Authorize::class,
        'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
        'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
        'wechat.oauth' => \Overtrue\LaravelWechat\Middleware\OAuthAuthenticate::class,
        'age' => \App\Http\Middleware\CheckAge::class,
    ];
```
$response = $kernel->handle(
    $request = Illuminate\Http\Request::capture()
   );
$response->send();
```
- 请求结束，进行回调
```   
	$kernel->terminate($request, $response);
```

###  核心概念介绍
####  服务容器
  - 用来装类的实例，然后在需要的时候再取出来。服务容器实现了控制反转（`Inversion of Control`，缩写为`IoC`）.  
####   控制反转Ioc

- 控制反转（Inversion of Control，缩写为IoC），是面向对象编程中的一种设计原则，可以用来减低计算机代码之间的耦合度。其中最常见的方式叫做依赖注入（Dependency Injection，简称DI），还有一种方式叫“依赖查找”（Dependency Lookup）。
	![1](http://ohn332hz8.bkt.clouddn.com/7956504c94ce41198d908d4245632dfb)
	![2](http://ohn332hz8.bkt.clouddn.com/2e71dd631c51aa7cef4a30d6712c70af)
	![3](http://ohn332hz8.bkt.clouddn.com/c92f3536c6d56ec968133df35a707dcc)
	![4](http://ohn332hz8.bkt.clouddn.com/3285e483b6333069611a85bf99728185)

- 正常情况下类`A`需要一个类`B`的时候，我们需要自己去new类`B`，意味着我们必须知道类`B`的更多细节，比如`构造函数`，随着项目的复杂性增大，这种依赖是毁灭性的。控制反转的意思就是，将类`A`主动获取类`B`的过程颠倒过来变成被动，类`A`只需要声明它需要什么，然后由容器提供。这样做的好处是，类`A`不依赖于类`B`的实现，这样在一定程度上解决了耦合问题。通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体，将其所依赖的`对象的引用`传递给它.

	
- 把`复杂系统`分解成相互合作的对象，这些对象类通过封装以后，内部实现对外部是透明的，从而降低了解决问题的复杂度，而且可以灵活地被重用和扩展。所谓`依赖注入`，就是由IOC容器在运行期间，`动态地`将某种依赖关系注入到对象之中。
	

	
- 在Laravel的服务容器中，为了实现控制反转，可以有以下两种：
   - 依赖注入（Dependency Injection）
     
     ```
     class UserController extends Controller
		{
		    protected $users;
		
		    public function __construct(UserRepository $users)
		    {
		        $this->users = $users;
		    }
		    public function show($id)
		    {
		        $user = $this->users->find($id);
		
		        return view('user.profile', ['user' => $user]);
		    }
		}

     ```
这里UserController需要一个UserRepository实例，我们只需在构造方法中声明我们需要的类型，容器在实例化UserController时会自动生成UserRepository的实例（或者实现类，因为UserRepository可以为接口），而不用主动去获取UserRepository的实例，这样也就`避免了了解UserRepository的更多细节`，`也不用解决UserRepository所产生的依赖`，我们所做的仅仅是声明我们所需要的类型，`所有的依赖问题都交给容器去解决`。
    - 绑定(放在服务提供器`Service Providers`中)
      - 绑定操作一般在ServiceProviders中的register方法中，最基本的绑定是容器的`bind`和`singleton`方法，它接受一个类的别名或者全名和一个闭包来获取实例.通过app这个服务容器来 bind 而不同去管  MapRepository 的依赖 和 具体的实现。
     
     	```
	    $this->app->bind('xblog', function ($app) {
	    	return new MapRepository();
		});
		```
		获取办法
		
		```
		1.  app('xblog');

		2.  app()->make('xblog');
		
		3.  app()['xblog'];
		
		4.  resolve('xblog');
		
		```

还有一种上下文绑定，就是相同的接口，在不同的类中可以自动获取不同的实现，例如：

```
$this->app->when(PhotoController::class)
          ->needs(Filesystem::class)
          ->give(function () {
              return Storage::disk('local');
          });

$this->app->when(VideoController::class)
          ->needs(Filesystem::class)
          ->give(function () {
              return Storage::disk('s3');
          });

```
上述表明，同样的接口`Filesystem`，使用依赖注入时，在`PhotoController`中获取的是`local`存储而在`VideoController`中获取的是`s3`存储。

######  IOC的优缺点
- 优点

  - 接口驱动设计(Interface Driven Design)的好处，可以灵活提供不同的子类实现(其实就是解耦),提高程序的灵活性、可扩展性和可维护性。

  - 管理了对象之间的关系。在OO中组合很有用，如果对象之间有复杂关系的话，那么我们就必须在new对象的时候来构建这种关系，这些关系其实都写死在代码中了。并且我们通过代码会直接把实际的类型写死，降低了针对接口编程的意义。如果能在配置文件中根据自己的需求来配置这种关系，由容器动态创建对象和对象之间关系的话，那么我们就把代码中依赖提取到了外部，由外部注入进去。在一个分层的应用程序中，我们不仅仅注入平行层级的对象，还可以注入下级对象，实现从上到下的自动注入，整个系统就非常灵活。
  
  - 管理了对象的生命周期。有的时候出了单例或是new出来的对象，还会有根据线程、根据请求来的特殊声明周期的对象，如果手写代码来管理声明周期一来很麻烦，二来也不方便调整，通过容器来管理对象的声明周期简单高效，并且我们很容易对容器进行扩展提供不同的声明周期的字典即可扩展生命周期的类型。
   
- 缺点
   - 软件系统中由于引入了第三方IOC容器，生成对象的步骤变得有些复杂，本来是两者之间的事情，又凭空多出一道手续，所以，我们在刚开始使用IOC框架的时候，会感觉系统变得不太直观。所以，引入了一个全新的框架，就会增加团队成员学习和认识的培训成本，并且在以后的运行维护中，还得让新加入者具备同样的知识体系。

   - 由于IOC容器生成对象是通过`反射方式`(反射就是根据给出的字符串(类名等)来生成对象,反射的好处就是可以临时决定要生成哪一种对象，缺点就是生成对象较慢)，在运行效率上有一定的损耗。如果你要追求运行效率的话，就必须对此进行权衡。

   - 具体到IOC框架产品(比如：Spring)来讲，需要进行大量的配制工作，比较繁琐，对于一些小的项目而言，客观上也可能加大一些工作成本。
	
###  Contracts
你只需在配置文件中指明你需要的缓存驱动（`redis`，`memcached`，`file`......），Laravel 就自动办你切换到这种驱动，而`不需要你针对某种驱动更改逻辑和代码`。Why? 很简单，Laravel定义了一系列`Contracts`（翻译：合同），本质上是一系列PHP接口，一系列的标准，用来解耦具体需求对实现的依赖关系。

![](http://ohn332hz8.bkt.clouddn.com/74d894d04b31dfcc1fecf4f829dea66d)

![](http://ohn332hz8.bkt.clouddn.com/0eb827b2def566f12cf2e7d31082aaf6)

上图不使用`Contracts`的情况下，对于一种逻辑，我们只能得到一种结果（方块），如果变更需求，意味着我们必须重构代码和逻辑。但是在使用`Contracts`的情况下，我们只需要按照接口写好逻辑，然后提供`不同的实现`，就可以在不改动代码逻辑的情况下获得更加多态的结果。
场景：我使用了缓存，代码逻辑中充满cache相关的方法：remember，flush，forget等等。但是后来要将缓存变成可选，但因为代码中充满和cache相关的方法，实现起来并不是很容易。
把缓存有关的方法抽象出来形成一个Contracts:xblogCache，实际操作只与Contracts有关，这样问题就得到了解决，而几乎没有改变原有的逻辑。

```
namespace App\Contracts;
use Closure;
interface XblogCache
{
    public function setTag($tag);
    public function setTime($time_in_minute);
    public function remember($key, Closure $entity, $tag = null);
    public function forget($key, $tag = null);
    public function clearCache($tag = null);
    public function clearAllCache();
}


```
完成了两个实现类：`Cacheable`和`NoCache`：

1. 实现具体缓存

```
class Cacheable implements XblogCache
{
	public $tag;
	public $cacheTime;
	public function setTag($tag)
	{
	    $this->tag = $tag;
	}
	public function remember($key, Closure $entity, $tag = null)
	{
	    return cache()->tags($tag == null ? $this->tag : $tag)->remember($key, $this->cacheTime, $entity);
	}
	public function forget($key, $tag = null)
	{
	    cache()->tags($tag == null ? $this->tag : $tag)->forget($key);
	}
	public function clearCache($tag = null)
	{
	    cache()->tags($tag == null ? $this->tag : $tag)->flush();
	}
	public function clearAllCache()
	{
	    cache()->flush();
	}
	public function setTime($time_in_minute)
	{
	    $this->cacheTime = $time_in_minute;
	}
}

```
2. 不缓存

```
class NoCache implements XblogCache
{
	public function setTag($tag)
	{
	    // Do Nothing
	}
	public function setTime($time_in_minute)
	{
	    // Do Nothing
	}
	public function remember($key, Closure $entity, $tag = null)
	{
	    /**
	     * directly return
	     */
	    return $entity();
	}
	public function forget($key, $tag = null)
	{
	    // Do Nothing
	}
	public function clearCache($tag = null)
	{
	    // Do Nothing
	}
	public function clearAllCache()
	{
	    // Do Nothing
	}
}

```
然后再利用容器的绑定，根据不同的配置，返回不同的实现

```
public function register()
{
   $this->app->bind('XblogCache', function ($app) {
       if (config('cache.enable') == 'true') {
           return new Cacheable();
       } else {
           return new NoCache();
       }
   });
}


```
这样，就实现了缓存的切换而不需要更改你的具体逻辑代码。当然依靠接口而不依靠具体实现的好处不仅仅这些。实际上，Laravel所有的核心服务都是实现了某个`Contracts`接口（都在`Illuminate\Contracts\`文件夹下面），而不是依赖具体的实现，所以完全可以在不改动框架的前提下，使用自己的代码改变Laravel框架核心服务的实现方式。


### Facade （门面/假象）

在我们把类的实例绑定到容器的时候相当于给类起了个别名，然后覆盖`Facade`的静态方法`getFacadeAccessor`并返回你的别名，然后你就可以使用你自己的`Facade`的静态方法来调用你绑定类的动态方法了。其实`Facade`类利用了`__callStatic()` 这个魔术方法来延迟调用容器中的对象的方法，这里不过多讲解，你只需要知道`Facade`实现了将对它调用的静态方法映射到绑定类的动态方法上，这样你就可以使用简单类名调用而不需要记住长长的类名。这也是`Facades`的中文翻译为假象的原因。


### 约定优于配置 
约定优于配置（convention over configuration），也称作按约定编程，是一种软件设计范式，旨在减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。[^2]
[^2]: https://zh.wikipedia.org/wiki/%E7%BA%A6%E5%AE%9A%E4%BC%98%E4%BA%8E%E9%85%8D%E7%BD%AE.

eg: 如果模型中有个名为Sale的类，那么数据库中对应的表就会默认命名为sales。只有在偏离这一约定时，例如将该表命名为"products_sold"，才需写有关这个名字的配置。在知名的Java对象关系映射框架Hibernate的早期版本中，将类及其属性映射到数据库上需要是在XML文件中的描述，其中大部分信息都应能够按照约定得到，如将类映射到同名的数据库表，将属性分别映射到表上的字段。后续的版本抛弃了XML配置文件，而是使用这些恰当的约定，对于不符合这些约定的情形，可以使用Java 标注来说明（参见下面提供的JavaBeans规范）。


### ORM
Laravel通过将数据库中的表行转成能被轻松操纵的PHP对象，来连接应用程序的数据模型和数据库表。它还使您能够执行业务规则，描述在应用程序中不同的数据模型之间的关系等。例如，一个人的家庭关系可以用Laravel Eloquent ORM描述如下：

```
class Person extends Eloquent
{
    public function mother()
    {
        return $this->belongsTo('Mother');
    }

    public function father()
    {
        return $this->belongsTo('Father');
    }

    public function spouse()
    {
        return $this->hasOne('Spouse');
    }

    public function sisters()
    {
        return $this->hasMany('Sister');
    }

    public function brothers()
    {
        return $this->hasMany('Brother');
    }
}

```

### [测试](http://laravelacademy.org/post/3274.html#ipt_kb_toc_3274_12)
- 与应用交互
  - 点击链接
  - 处理表单
  - 处理附件
- 测试JSON API


### 演示

```
php artisan make:model Models/MbdTech  	           // create model MbdTech
php artisan make:migration mdbtechs                   // create table mdbtechs
php artisan migrate
php artisan make:controller MbdTech/MbdTechController // create controller
php artisan make:test MbdTechTest                     // test

php artisan make:seeder MbdTechsTableSeeder           // create seeder
php artisan db:seed --class=MbdTechsTableSeeder       // use factory to create test data

add  $this->call(MbdTechsTableSeeder::class); to DatabaseSeeder to run MbdTechsTableSeeder.

run 
php artisan db:seed 
to excute seeder in databaseSeeder
or run 
php artisan db:seeder --class=MbdTechsTableSeeder
to excute just MbdTechsTableSeeder
or run
php artisan migrate:refresh --seed 
to excute all seed when completely restructing your database.

// create route (restful routing)

php artisan migrate:rollback --step=2                 // back migrate
```



### 总结








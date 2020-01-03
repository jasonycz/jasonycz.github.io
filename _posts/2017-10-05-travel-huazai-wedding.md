---
layout:     post
title:      "Travel to Inner Mogolia for HuaJun wedding"
subtitle:   "Travel Inner Mongolia for CollegeRoomate Wedding"
date:       2017-10-04 17:19:42 
author:     "Jasonycz"
header-img: "img/innermongolia-travel-guide-bg.png"
tags:
    - Travle
---

## HuaJun Wedding

### 旅途
<figure>
    <img src="http://public.minapplat.com/f18e3ee1af034cb580f2fe349cda0919">
    <img src="http://public.minapplat.com/f0560347004549fceb4ef394895646d4">
    <img src="http://public.minapplat.com/e95b734b026945687d32a85d06875e2f">
</figure>

### 婚礼
<figure>
    <img src="http://public.minapplat.com/d17b82bb81e1537e559306b6a6247546">
    <img src="http://public.minapplat.com/923607d51cc18b78a9e0338cec0292f7">
    <img src="http://public.minapplat.com/9e31a8f959622b3119e20a830b6fe2bb">
    <img src="http://public.minapplat.com/4d31831496d474f1ff9287982e7eb2e5">
    <img src="http://public.minapplat.com/1a269ae1a9a4adf652e22f5f44e10dcf">
</figure>

### 那时的我们

<figure>
    <img src="http://public.minapplat.com/e0055ab7fc6f96967ea1c4086d5cd52f">
    <img src="http://public.minapplat.com/3ecfcb0fed4616a941495e45020af184">
</figure>

## Travel experience
- 想要就要去追求, 勇敢前行
- 用积极的心态感染周边的人 
- 用积极的行动感动身边的人
- 用诚心诚意感动身边的人
- 遵循自己的内心

## convenient album 一期
- 图片上传 编辑 删除 移动  
- 相册的 新建 编辑 删除 

## Reading Laravel Guider

> APP_KEY 

- APP_KEY 用于加密一些数据用途
- 生成办法: php artisan key:generate

> 默认值的访问

- 使用函数 `config` 如 `config('app.timezone')`;
- 运行是设置 config 数组的值,可以使用的办法是 `config(['app.timezone' => 'America/Chicago']);`

> Cache

- `Cache::store('memcached')->get('xxx');` 才能够获取到 `cache` 的内容 是因为使用的还是 `file` 作为`cacha` 需要修改 `.evn` 文件里面的配置

> 环境配置

- 访问当前app的环境  `\App::environment()`

> 维护模式

- `php artisan down`  // 开启维护模式  状态码为 503 的 MaintenanceModeException 将会被抛出
- `php artisan up`    // 关闭维护模式
- 维护模式相应模板  `resources/views/errors/503.blade.php`

> 疑问点

- 为什么在 .env 中设置 cache 为 memcached 报错 class Memcached not found ?

> 控制器 路由缓存

- 如果你的应用完全基于控制器路由,可以使用 Laravel 的路由缓存,使用路由缓存将会极大减少 注册所有应用路由所花费的时间开销. 
- 开启路由缓存 `php artisan route:cache` 
- 关闭路由缓存 `php artisan route:clear`

> 用户认证

- `php artisan make:auth` 

> Laravel 通过运行如下命令可快速生成认证所需要的路由和视图

- `php artisan make:auth`

> 登录失败次数限制

- 如果你使用了Laravel内置的类, 可以使用 trait 来限制用户登录失败次数。默认情况下,用
户在几次登录失败后将在一分钟内不能登录,这种限制基于用户的用户名/邮箱地址+IP 地址。























































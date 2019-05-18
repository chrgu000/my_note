# laravel

 #### route

-  如果路由是定义在 routes/web.php 的话，在测试 POST 请求之前，需要将对应路由取消 CSRF 保护检查，否则会返回 419 状态码导致无法请求成功，取消的方法是在 app/Http/Middleware/VerifyCsrfToken 中设置排除检查路由, 　事实这样也不安全
-  如果路由是定义在 routes/api.php 的话，则无需关注 CSRF 保护问题
    ```
    背后的原因是因为web路由文件中定义的路由都位于web中间件群组，
    该群组默认启用 CSRF 保护检查，而 api 路由文件位于 api 路由
    群组，该群组下的路由主要用于 第三方 API 请求，没办法进行CSRF 
    检查，所以不需要做任何处理。
    ```
    
- 在 routes/web.php 路由文件中所有请求方式为 PUT、POST 或 DELETE 的路由对应的 HTML 表单都必须包含一个 CSRF 令牌字段，否则，请求会被拒绝。
  ```php+HTML
   <form method="POST" action="/profile">
       {{ csrf_field() }}
        ...
    </form>
  ```
  
- ######  路由参数  注意参数不能key=value 不能带空格
    路由参数需要通过花括号 {} 进行包裹并且是拼音字母，这些参数在路由被执行时会被传递到路由的闭包。路由参数名称不能包含 - 字符，如果需要的话可以使用 _ 替代，比如如果某个路由参数定义成 {post-id} 则访问路由会报错，应该修改成 {post_id} 才行。路由参数被注入到路由回调/控制器取决于它们的顺序，与回调/控制器名称无关。
    ```php
    Route::get('posts/{post}/comments/{comment}', function ($postId, $commentId) {
           return $postId . '-' . $commentId;
    });
    ```
    
- ###### 正则约束 
    ```php
    Route::get('user/{name}', function ($name) {
       // $name 必须是字母且不能为空
    })->where('name', '[A-Za-z]+');

    Route::get('user/{id}', function ($id) {
        // $id 必须是数字
    })->where('id', '[0-9]+');

    Route::get('user/{id}/{name}', function ($id, $name) {
    // 同时指定 id 和 name 的数据格式
    })->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
        
    ```
- ###### 路由名称前缀
    name 方法可通过传入字符串为分组中的每个路由名称设置前缀，例如，你可能想要在所有分组路由的名称前添加 admin 前缀，由于给定字符串和指定路由名称前缀字符串完全一样，所以需要在前缀字符串末尾后加上 . 字符

    ```php
    Route::name('admin.')->group(function () {
    Route::get('users', function () {
            // 新的路由名称为 "admin.users"...
    })->name('users');
    }) ;
    ```
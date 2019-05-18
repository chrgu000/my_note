创建响应

**字符串 & 数组**

所有路由和控制器处理完业务逻辑之后都会返回一个发送到用户浏览器的响应，Laravel 提供了多种不同的方式来返回响应，最基本的响应就是从路由或控制器返回一个简单的字符串，框架会自动将这个字符串转化为一个完整的 HTTP 响应：

Route::get('/', function () {     return 'Hello World'; }); 

除了从路由或控制器返回字符串之外，还可以返回数组。框架会自动将数组转化为一个 JSON 响应：

Route::get('/', function () {     return [1, 2, 3]; }); 

注：你知道还可以从路由或控制器返回 [Eloquent 集合](http://laravelacademy.org/post/8210.html)吗？这也会被自动转化为 JSON 响应。

**Response 对象**

通常，我们并不只是从路由动作简单返回字符串和数组，大多数情况下，都会返回一个完整的 Illuminate\Http\Response 实例或[视图](http://laravelacademy.org/post/7903.html)。

返回一个完整的 Response 实例允许你自定义响应的 HTTP 状态码和头信息。Response 实例继承自 Symfony\Component\HttpFoundation\Response 基类，该类提供了一系列方法用于创建 HTTP 响应：

Route::get('cookie/response', function () {     return response('Hello World', 200)         ->header('Content-Type', 'text/plain'); }); 

**添加响应头**

大部分响应方法都可以以方法链的形式调用，从而可以流式构建响应（[流接口模式](http://laravelacademy.org/post/2828.html)）。例如，在发送响应给用户前可以使用 header 方法来添加一系列响应头：

return response($content)     ->header('Content-Type', $type)     ->header('X-Header-One', 'Header Value')     ->header('X-Header-Two', 'Header Value'); 

或者你可以使用 withHeaders 方法来指定头信息数组添加到响应：

return response($content)     ->withHeaders([         'Content-Type' => $type,         'X-Header-One' => 'Header Value',         'X-Header-Two' => 'Header Value',     ]); 

**添加 Cookie 到响应**

使用响应实例上的 cookie 方法可以轻松添加 Cookie 到响应。例如，你可以使用 cookie 方法生成 Cookie 并添加将其添加到响应实例：

return response($content)     ->header('Content-Type', $type)     ->cookie('name', 'value', $minutes); 

cookie 方法还可以接收更多使用频率较低的额外可选参数，一般来说，这些参数和 PHP 原生提供的 [setcookie](https://secure.php.net/manual/zh/function.setcookie.php) 方法目的和意义差不多：

->cookie($name, $value, $minutes, $path, $domain, $secure, $httpOnly) 

此外，还可以使用 Cookie 门面将应用于附件的 Cookie 推送到输出响应队列。queue 方法接收 Cookie 实例或创建 Cookie 所必要的参数，这些 Cookie 会在响应被发送到浏览器之前添加到响应：

Route::get('cookie/response', function() {     Cookie::queue(Cookie::make('site', 'Laravel学院',1));     Cookie::queue('author', '学院君', 1);     return response('Hello Laravel', 200)         ->header('Content-Type', 'text/plain'); }); 

我们在浏览器中访问 http://blog.test/cookie/response 就能看到这两个新增的 Cookie：

![img](file:///D:/YoudaoNote/YoudaoNoteFile/qq4BDDC0AB6D73F4584555C13816962A6F/70d1d78517ff41e5bf31f02ab593273f/76234164970.jpeg)

**Cookie & 加密**

默认情况下，Laravel 框架生成的 Cookie 都经过了加密和签名，以免在客户端被篡改。如果你想要让特定的 Cookie 子集在生成时取消加密，可以通过 app/Http/Middleware 目录下的中间件 App\Http\Middleware\EncryptCookies提供的 $except 属性来排除这些 Cookie：

/**  * 不需要被加密的cookies名称  *  * @var array  */ protected $except = [     'cookie_name', ]; 

重定向

重定向响应是 Illuminate\Http\RedirectResponse 类的实例，包含了必要的头信息将用户重定向到另一个 URL，有很多方式来生成 RedirectResponse 实例，最简单的方法就是使用全局辅助函数 redirect：

Route::get('dashboard', function () {     return redirect('home/dashboard'); }); 

有时候你想要将用户重定向到上一个请求的位置，比如，表单提交后，验证不通过，你就可以使用辅助函数 back 返回到前一个 URL（由于该功能使用了 [Session](http://laravelacademy.org/post/7954.html)，使用该方法之前确保相关路由位于 web 中间件组或者应用了 Session 中间件）：

Route::post('user/profile', function () {     // 验证请求...     return back()->withInput(); }); 

重定向到命名路由

如果调用不带参数的 redirect 方法，会返回一个 Illuminate\Routing\Redirector 实例，然后就可以使用 Redirector 实例上的所有方法。例如，要生成一个 RedirectResponse 到命名路由，可以使用 route 方法：

return redirect()->route('login'); 

如果路由中有参数，可以将其作为第二个参数传递到 route 方法：

// For a route with the following URI: profile/{id} return redirect()->route('profile', ['id'=>1]); 

**通过 Eloquent 模型填充参数**

如果要重定向到带 ID 参数的路由（ Eloquent 模型绑定 ），可以传递模型本身，ID 会被自动解析出来：

return redirect()->route('profile', [$user]); 

如果你想要自定义这个路由参数中的默认参数名（默认是 id），需要重写模型实例上的 getRouteKey 方法：

/**  * Get the value of the model's route key.  *  * @return mixed  */ public function getRouteKey() {     return $this->slug; } 

重定向到控制器动作

你还可以生成重定向到[控制器动作](http://laravelacademy.org/post/8753.html)的响应，只需传递控制器和动作名到 action 方法即可。记住，你不需要指定控制器的完整命名空间，因为 Laravel 的 RouteServiceProvider 将会自动设置默认的控制器命名空间：

return redirect()->action('HomeController@index'); 

和 route 方法一样，如果控制器路由要求参数，你可以将参数作为第二个参数传递给 action 方法：

return redirect()->action('UserController@profile', ['id'=>1]); 

重定向到外部域名

有时候你可能需要重定向到应用之外的其他域名，这可以通过调用 away 方法来实现，该方法会创建一个 RedirectResponse，没有任何额外的 URL 编码或验证：

return redirect()->away('http://laravelacademy.org'); 

带一次性 Session 数据的重定向

重定向到一个新的 URL 并将数据存储到[一次性 Session](http://laravelacademy.org/post/7954.html#toc_6) 中通常是同时完成的，为了方便，可以创建一个 RedirectResponse 实例然后在同一个方法链上将数据存储到 Session，这种方式在 action 之后存储状态信息时特别方便：

Route::post('user/profile', function () {     // 更新用户属性...     return redirect('dashboard')->with('status', 'Profile updated!'); }); 

用户重定向到新页面之后，你可以从 [Session](http://laravelacademy.org/post/7954.html) 中取出并显示这些一次性信息，使用 [Blade 语法](http://laravelacademy.org/post/8773.html)实现如下：

@if (session('status'))     <div class="alert alert-success">         {{ session('status') }}     </div> @endif 

注：这个一次性体现在从 Session 取出数据之后，这些数据就会被销毁，不复存在。

其它响应类型

上面我们讲了 Response 和 RedirectResponse 两种响应类型，我们还可以通过辅助函数 response 很方便地生成其他类型的响应实例，当无参数调用 response 时会返回 Illuminate\Contracts\Routing\ResponseFactory [契约](http://laravelacademy.org/post/8710.html)的一个实现，该契约提供了一些有用的方法来生成各种响应，如视图相应、JSON 响应，文件下载、流响应等等。

视图响应

如果你需要控制响应状态和响应头，并且还需要返回一个[视图](http://laravelacademy.org/post/7903.html)作为响应内容，可以使用 view 方法：

return response()         ->view('hello', $data, 200)         ->header('Content-Type', $type); 

当然，如果你不需要传递自定义的 HTTP 状态码和头信息，只需要简单使用全局辅助函数 view 即可：

Route::get('view/response', function() {    return view('hello'); }); 

我们需要在这个路径下创建这个文件才能正常访问其内容：

![img](file:///D:/YoudaoNote/YoudaoNoteFile/qq4BDDC0AB6D73F4584555C13816962A6F/61100c0b2e5843e18e32a6b245bba75c/76251341299.jpeg)

JSON响应

json 方法会自动将 Content-Type 头设置为 application/json，并使用 PHP 函数 json_encode 方法将给定数组转化为 JSON 格式数据：

return response()->json([         'name' => 'Abigail',          'state' => 'CA' ]); 

如果你想要创建一个 JSONP 响应，可以在 json 方法之后调用 withCallback 方法：

return response()         ->json(['name' => 'Abigail', 'state' => 'CA'])         ->withCallback($request->input('callback')); 

或者直接使用 jsonp 方法：

return response()         ->jsonp($request->input('callback'), ['name' => 'Abigail', 'state' => 'CA']); 

文件下载

download 方法用于生成强制用户浏览器下载给定路径文件的响应。download 方法接受文件名作为第二个参数，该参数决定用户下载文件的显示名称，你还可以将 HTTP 头信息作为第三个参数传递到该方法：

return response()->download($pathToFile); return response()->download($pathToFile, $name, $headers); return response()->download($pathToFile)->deleteFileAfterSend(true); 

注：管理文件下载的 Symfony HttpFoundation 类要求被下载文件有一个 ASCII 文件名，这意味着被下载文件名不能是中文。

举个例子，我们可以通过以下代码下载[上一篇文档](http://laravelacademy.org/post/8764.html#toc_7)上传的图片：

Route::get('download/response', function() {     return response()->download(storage_path('app/photo/test.jpg'), '测试图片.jpg'); }); 

**流式下载**

有时候你可能想要将给定操作的字符串响应转化为可下载的响应而不用将操作内容写入磁盘。这种场景下可以使用 streamDownload 方法，该方法接收一个回调、文件名以及可选的响应头数组作为参数：

return response()->streamDownload(function () {     echo GitHub::api('repo')                 ->contents()                 ->readme('laravel', 'laravel')['contents']; }, 'laravel-readme.md'); 

文件响应

file 方法可用于直接在用户浏览器显示文件，例如图片或 PDF，而不需要下载，该方法接收文件路径作为第一个参数，头信息数组作为第二个参数：

return response()->file($pathToFile); return response()->file($pathToFile, $headers); 

响应宏

如果你想要定义一个自定义的可以在多个路由和控制器中复用的响应，可以使用 Response 门面上的 macro 方法。例如，在某个[服务提供者](http://laravelacademy.org/post/8697.html)的 boot 方法中编写代码如下：

<?php  namespace App\Providers;  use Illuminate\Support\Facades\Response; use Illuminate\Support\ServiceProvider;  class ResponseMacroServiceProvider extends ServiceProvider {     /**      * Perform post-registration booting of services.      *      * @return void      */     public function boot()     {         Response::macro('caps', function ($value) {             return Response::make(strtoupper($value));         });     } } 

macro 方法接收响应名称作为第一个参数，闭包函数作为第二个参数，响应宏的闭包在 ResponseFactory 实现类或辅助函数 response 中调用宏名称的时候被执行：

Route::get('macro/response', function() {     return response()->caps('LaravelAcademy'); }); 

在浏览器中访问 http://blog.test/macro/response，输出入下：

LARAVELACADEMY
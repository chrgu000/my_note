# middleware

- ###### 生成中间件 
    - php artisan make:middleware CheckToken
    这个命令会在这个命令会在 app/Http/Middleware 目录下创建一个新的中间件类 CheckToken
        ```php
        public function handle($request, Closure $next)
        {   
        if ($request->input('token') != '123456') {
                return redirect()->to('http://laravel.test')
            }
            return $next($request);
        }
        ```
        如果 token != 'laravelacademy.org'，中间件会返回一个 HTTP 重定向到 Laravel 学院；否则，请求会被传递下去。将请求往下传递可以通过调用回调函数 $next 并传入当前 $request。
    - 此时只是定义好了中间件的逻辑，要让这个中间件生效，还要将其注册到指定路由中
- 中间件：全局中间件，中间件组，直径路由中间件
    - 如果你想要定义的中间件在每一个 HTTP分配中间件到指定路由 请求时都被执行，只需要将相应的中间件类添加到 app/Http/Kernel.php 的数组属性 $middleware 中即可：但除非真的需要，否则我们一般不会把业务级别的中间件放到全局中间件中。
        ```php
        protected $middleware = [
            \App\Http\Middleware\CheckForMaintenanceMode::class,
            \Illuminate\Foundation\Http\Middleware\ValidatePostSize::class,
            \App\Http\Middleware\TrimStrings::class,
            \Illuminate\Foundation\Http\Middleware\ConvertEmptyStringsToNull::class,
            \App\Http\Middleware\TrustProxies::class,
            CheckToken::class,
        ];
        ```
    - 分配中间件到指定路由
    首先应该在 app/Http/Kernel.php 文件中分配给该中间件一个 key，默认情况下，该类的 $routeMiddleware 属性包含了 Laravel 自带的中间件，要添加你自己的中间件，只需要将其追加到后面并为其分配一个 key，例如：
        ```php
        protected $routeMiddleware = [
            'auth' => \App\Http\Middleware\Authenticate::class,
            'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
            'bindings' => \Illuminate\Routing\Middleware\SubstituteBindings::class,
            'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
            'can' => \Illuminate\Auth\Middleware\Authorize::class,
            'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
            'signed' => \Illuminate\Routing\Middleware\ValidateSignature::class,
            'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
            'verified' => \Illuminate\Auth\Middleware\EnsureEmailIsVerified::class,
                'token' => CheckToken::class,
        ];
        ```
    - 中间件在 HTTP Kernel 中被定义后，可以使用 middleware 方法将其分配到路由

        ```php
        Route::get('/', function () {
            //
        })->middleware('token');
        
        ```
    
    - 可以使用数组分配多个中间件到路由：
        ```php
        Route::get('/', function () {
            //
        })->middleware('token', 'auth');
        ```
- ###### 中间件组
    - 有时候你可能想要通过指定一个键名的方式将相关中间件分到同一个组里面，这样可以更方便地将其分配到路由中，这可以通过使用 HTTP Kernel 提供的 $middlewareGroups 属性实现。
        ```php
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
                'auth:api',
            ],
        ];
        ```
        
    - 中间件组使用和分配单个中间件同样的语法被分配给路由和控制器动作。再次申明，中间件组的目的只是让一次分配给路由多个中间件的实现更加方便
        ```php
        Route::get('/', function () {
            //
        })->middleware('web');
        
        Route::group(['middleware' => ['web']], function () {
            //
    });
    
        ```
    
    - 默认情况下， RouteServiceProvider 自动将中间件组 web 应用到 routes/web.php 文件，将中间件组 api 应用到 routes/api.php：
    
- controller 使用中间件
    - 路由中添加
        ```php
        Route::get('profile', 'UserController@show')->middleware('auth');
        ```
    - 控制器中使用
        ```php
        public function __construct()
        {
            $this->middleware('token');
        }
        ```
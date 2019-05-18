#### 源码位置 vendor/laravel/framework/src/Illuminate/Http/Concerns/InteractsWithInput.php
- input 方法会从整个请求负载（包括查询字符串）中获取数值，query则只会从查询字符串中获取数值：
- 使用动态属性的时候，Laravel 首先会在请求中查找参数的值，如果不存在，还会到路由参数中查找。该功能的实现原理自然是魔术函数 __get 了：    
    ```php
    $name = $request->name;
    ```
- 如果你想要判断参数存在且参数值不为空，可以使用 filled 方法：
    ```php
    if ($request->filled('name')) {
    //
    }   
    ```
- Laravel 允许你在两次请求之间保存上一次输入数据，这个特性在检测校验数据失败后需要重新填充表单数据时很有用，不过如果你使用的是 Laravel 自带的验功能，则不需要手动使用这些方法，因为一些 Laravel 自带的校验设置会自动调用它们
    - 将输入存储到 Session
        - Illuminate\Http\Request 实例的 flash 方法会将当前输入存放到一次性 Session（所谓的一次性指的是从 Session 中取出数据后，对应数据会从 Session 中销毁）中，这样在下一次请求时上一次输入的数据依然有效
        ```php
        $request->flash();
        ```
    - 你还可以使用 flashOnly 和 flashExcept 方法将输入数据子集存放到 Session 中，这些方法在 Session 之外保存敏感信息时很有用，该功能适用于登录密码填写错误的场景：
        ```php
        $request->flashOnly('username', 'email');
        $request->flashExcept('password');
        ```
    - 将输入存储到 Session 然后重定向
        - 如果你经常需要一次性存储输入请求输入并返回到表单填写页，可以在 redirect 之后调用 withInput 方法实现这样的功能：
            ```php
            return redirect('form')->withInput();
            return redirect('form')->withInput($request->except('password'));
            ```
    - 取出上次请求数据

        ```php
        $username = $request->old('username');
        ```
        
        - Laravel 还提供了一个全局的辅助函数 old()，如果你是在 Blade 模板中显示上次输入数据，使用辅助函数 old() 更方便，如果给定参数没有对应输入，返回 null：
            ```php
            <input type="text" name="username" value="{{ old('username') }}">
            
            ```
- ## Cookie
    - 为了安全起见，Laravel 框架创建的所有 Cookie 都经过加密并使用一个认证码进行签名，这意味着如果客户端修改了它们则需要对其进行有效性验证。我们使用 Illuminate\Http\Request 实例的 cookie 方法从请求中获取 Cookie 的值：
        ```php
        $value = $request->cookie('name');
        ```
        ```php
        Route::get('cookie/add', function () {
            $minutes = 24 * 60;
            return response('欢迎来到 Laravel 学院')->cookie('name', '学院君', $minutes);
        });
        
        Route::get('cookie/get', function(\Illuminate\Http\Request $request) {
            $cookie = $request->cookie('name');
            dd($cookie);
        });
        ```
    - 生成cookie实例
        ```php
        Route::get('cookie/add', function () {
            $minutes = 24 * 60;
            //return response('欢迎来到 Laravel 学院')->cookie('name', '学院君', $minutes);
            $cookie = cookie('name', '学院君X', $minutes);
            return response('欢迎来到 Laravel 学院')->cookie($cookie);
        });
        ```
- input 方法会从整个请求负载（包括查询字符串）中获取数值，query则只会从查询字符串中获取数值：
    ```php
    $name = $request->query('name', '学院君');
    ```
- 此外，你还可以通过使用 Illuminate\Http\Request 实例上的动态属性来访问用户输入。例如，如果你的应用表单包含 name 字段，那么可以像这样访问提交的值：
    ```php
    $name = $request->name;
    ```
- 发送 JSON 请求到应用的时候，只要 Content-Type 请求头被设置为 application/json，都可以通过 input 方法获取 JSON 数据，还可以通过“.”号解析数组：

    ```php
    $name = $request->input('user.name');
    ```
- 判断参数在请求中是否存在，可以使用 has 方法，如果参数存在则返回 true：
    ```php
    if ($request->has('name')) {
        //
    }
        
    ```
- 该方法支持以数组形式查询多个参数，这种情况下，只有当参数都存在时，才会返回 true：
    ```php
    if ($request->has(['name', 'email'])) {
       //
    }
    ```

- ## 文件上传
    ```php
    Route::post('file/upload', function(Request $request) {
        if ($request->hasFile('photo') && $request->file('photo')->isValid()) {
            $photo = $request->file('photo');
            $extension = $photo->extension();
            // 随机生成文件名
            $store_result = $photo->store('photo');
            // 指定文件名
            $store_result = $photo->storeAs('photo', 'test.jpg', 'public');
            $output = [
                'extension' => $extension,
                'store_result' => $store_result
            ];
            print_r($output);exit();
        }
        exit('未获取到上传文件或上传过程出错');
    });
    ```
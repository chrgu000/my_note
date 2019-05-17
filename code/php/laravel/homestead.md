##### 	homestead安装

<!--[TOC]-->


- ###### virtualbox
- ###### vagrant
- ######  homesetead box  迅雷下载或者其他  
    - vagrant box add laravel/homestead  这个命令从国外网站下载太慢了
    - https://vagrantcloud.com/laravel/boxes/homestead/versions/7.1.0/providers/virtualbox.box

---

- ###### 启动homestead时出现错误found a tab character that violate intendation while scanning a plain scalar解决方法
    - 通常都是复制粘贴代码或者配置文件导致
    - 可以检查最近做过的配置的地方，看看有什么地方是使用了tab代替了空格，修改后重新启动  常发生在文件yaml配置文件中

---

- ###### 启动vagrant up 时提示　VirtualBox is complaining that the kernel module is not loaded.
    - 解决安装 VirtualBox　sudo pacman -S virtualbox
    - 此时虚拟机已经安装完成，但是创建虚拟机之后启动会报错。提示内核问题。
    - 查询当前内核版本 uname -r 
        1. 4.14.71-1-MANJARO.
        2. sudo pacman -S linux414-virtualbox-host-modules
    - 将VirtualBox模块添加到内核中。重启。sudo vboxreload

---


- ###### 删除homestead盒子
    - vagrant box list 查看已经安装的盒子
    - vagrant box remove   ' 盒子名称'

---

- ###### 已经安装'laravel/homestead' box，但是执行homestead up时提示找不到box
    -  打开homestead.rb文件 把 
    ```
    config.vm.box_version = settings["version"] ||= ">= 0.4.0" 
    ```
    改为
    ```
    config.vm.box_version = settings["version"] ||= ">= 0"
    ```
- 数据库
    - 127.0.0.1
    - 33060
    - homestead/secretoptirun

---

- ###### composer 国内镜像地址
    - composer config -g repo.packagist composer https://packagist.phpcomposer.com
    - composer config -g repo.packagist composer https://packagist.laravel-china.org
    -  查看配置
        ```
        composer config -gl
        ```
    

---
- ###### redis
    1. Homestead 下安装redis,按顺序执行如下命令
        ```
        sudo apt-get update
        sudo apt-get install redis-ser
        redis-serve 启动redis
        redis-cli 检查redis是否启动(如下图redis已经在虚拟机上正常启动)
        ```
        
	2. 	修改redis配置文件（默认路径/etc/redis/redis.conf）,  要不链接会出现问题
      
    	```
        requirepass   yourpassword----设置任何你想要的密码 
        bind 127.0.0.1 修改为 bind 0.0.0.0
    	```
    	
    3. 一些操作
        1. keys * 获取所有 key
        2. flushall 清空所有缓存
        3. del key 删除某一个索引相当于清除某一个缓存
    
    4. 在Laravel上安装配置redis,
        通过composer安装redis
    
        ```
        composer require predis/predis -vvv
        ```
        
    5. 修改端口映射
    
        	```
        ports:
        	- send: 63790
        	to: 6379 
        ```
- ###### phpstrom 配置laravel提示
  
    - 安装laravel-plugin
    - 在项目的composer.json中添加如下一行
        ```
        "require": {
        "laravel/framework": "5.1.*",
        "barryvdh/laravel-ide-helper": "^2.3"
        }
        ```
    - 执行更新  
        ```
        composer update
        ```
    - 打开项目config/app.php 于providers添加如下一行
        ```
        Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
        ```
    - 生成代码助手  注意要在进入vagrant ssh 后，进入该目录执行4
        ```
        php artisan ide-helper:generate  
        ```
    - phpstrom mode方法不提示findOrFail
        ```
        composer require --dev barryvdh/laravel-ide-helper
        ```
    - 默认支持blade提示
        - 要在keymap 里completion->basic 添加一个快捷键ctrl+j
        然后leavel
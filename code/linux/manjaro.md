# manjaro_deepin

#### 快捷建

- win+a全部任务 win+s当前桌面任务
- 命令行中输入htop 启动系统监控
- screenfetch 显示安装的系统信息
---

####  主题切换

- 地址　https://www.gnome-look.org/browse/
- manjaro deepin 需要将图标放进  /usr/share/icons
- manjaro deepin 需要将主题放进  /usr/share/themes 　主题需注销重启
- icon 
    ```
    git clone https://github.com/zayronxio/Mojave-CT.git
    ```
- cursors
  
    - serch capitaine cursors
- themes 
    ```
    git clone https://github.com/vinceliuice/Sierra-gtk-theme.git
    ```

---
#### 双显卡设置

  1. 在硬件管理里面卸载掉所有的显卡驱动

  2. **解决依赖**

     ```bash
     sudo pacman -S virtualgl lib32-virtualgl lib32-primus primus
     ```

  3. **安装双显卡切换程序bumblebee, 不要安装其他的显卡驱动会导致开机黑屏**

     ```bash
     sudo mhwd -f -i pci video-hybrid-intel-nvidia-bumblebee
     ```

  4. **启动服务**

     ```bash
     sudo systemctl enable bumblebeed
     ```

  5. **添加用户**

     ```bash
     sudo gpasswd -a $USER bumblebee
     ```

  6. **reboot**

  7. 测试显卡的FPS, 会发现独显的FPS明显有了变化

     ```
     glxgears    //测试集显的FPS
     optirun glxgears	//测试独显的FPS
     ```

  8. 显卡驱动安装好后，如何在程序中用独立显卡来运行呢，可以用到optirun命令，格式为：

     ```bash
     optirun ~/.local/share/Steam/ubuntu12_32/steam-runtime/run.sh /bin/sh ./Empire.sh
     ```


#### 安装

- 配置国内的软件源 
    ```
    sudo pacman-mirrors -i -c China -m rank
    ```

- 刷新缓存
    ```
    sudo pacman -Syy
    ```
    
- 更新
    ```
    sudo pacman -Syu
    ```
    
- 添加 `Archlinux` 中文社区仓库 在 `/etc/pacman.conf`文件末尾添加一下两行:
    ```
    [archlinuxcn] 
    Server = https://mirrors.shu.edu.cn/archlinuxcn/$arch
    或
    Server = http://mirrors.163.com/archlinux-cn/$arch
  ```
  
- 安装 `archlinuxcn-keyring` 包导入GPG key.  

- sudo pacman -Sy archlinuxcn-keyring

- 安装搜狗输入法
    ```
    sudo pacman -S fcitx-sogoupinyin
    sudo pacman -S fcitx-im
    sudo pacman -S fcitx-configtool # 图形化的配置工具
    ```
    
- 需要修改配置文件 ~/.xprofile   添加如下语句
    ```
    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    export XMODIFIERS="@im=fcitx"
    ```
    
- 安装配 置 Git
    ```
   sudo pacman -S git 
   ```
   
- 设置个人github信息：
    ```
    git config --global user.name "github昵称" 
    git config --global user.email "注册邮箱" 
    ```
    
- 安装网易云音乐   sudo pacman -S netease-cloud-music 

- 谷歌浏览器    pacman -S google-chrome 

- Git ssh
    ```
     pacman -S git openssh
    ```
    
- 安装 Python3 的 pip     sudo pacman -S python-pip

- 安装oh-my-zsh
    - sudo pacman -S zsh
    - 使用zsh替换bash:  
      ```
      chsh -s /bin/zsh
      ```
    
    - 出现 chsh: 鉴定故障的解决方法考虑到chsh实际上是更改/etc/passwd文件，在这个文件里面有一行是bin/bash，于是我用vi改为了bin/csh，保存。然后重启系统。也实现了更改shell的目的。
    
    -  安装oh-my-zsh    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    
    - 安装autojump   sudo pacman -S autojump
    
    - 再在~/.zshrc中添加:
      ```
       plugins=(git autojump)
      ```
      
    - 主题  powerlevel10k
    	```
    	git clone https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
    	echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>! ~/.zshrc
    	```
    - Set ZSH_THEME=powerlevel10k/powerlevel10k in your ~/.zshrc.
    - 这种安装方式需要禁用掉上面一条
    
- 字体
    - monaco
    - inconsolate 
    - 直接商店里搜

- 翻墙 
  
    - 搭建服务器， https://my.vultr.com/billing/ 买服务器
    
- sl linux彩蛋小火车
    ```
    sudo pacman -S sl
    ```
    - 输入 sl
    ```
    它同样支持下面的选项：

    -a : 似乎发生了意外。你会为那些哭喊求助的人们感到难过。 
    -l : 显示小一点的火车 
    -F : 它居然飞走了 
    -e : 允许被 Ctrl+C 中断
    ```
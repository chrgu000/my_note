- 将单行注释改成注释代码前

	- 去掉 setting-> editot -> code style ->php -> code generation -> line comment as first column 前面的钩

- 快捷键

	```html
	phpstorm快捷键
	alt+alt:                连续两次快速按下alt键不放，显示tool windows（project,database ...)
	alt+F7:                 查找选定变量，方法被调用的地方。选中一个方法或者变量，查找出所有调用的地方
	alt+F3:                 显示搜索窗格，对当前文件进行搜索，然后配合ctrl+alt+r,可以进行替换操作
	alt+F1:                 快速打开当前编辑文件在其他tool windows里，这个很好用的键盘
	alt+方向键：            左右在打开的编辑器标签间切换，上下在打开的文件中的方法里上下切换
	alt+shift+c:            浏览最近的修改历史
	
	ctrl+`:                 选择主题，不常用
	ctrl+F12:               弹出一个对话框，显示当前文件里的所有方法，变量，直接输入方法变量名，回车即可跳转到定义位置
	ctrl+k:                 快速调用 commit changes 对话框
	ctrl+l 或 f3            上一个函数
	ctrl+n:                 快速打开任意类，弹出一个对话框，输入类名称，跳转到类文件
	ctrl+tab:               switcher,在已打开文件之间或者工具窗口间切换
	ctrl+alt+d:             快速复制多行，哈哈，这个vim里更加简单
	ctrl+alt+左右方向键     上次编辑位置
	ctrl+shift+backspace:   上次编辑位置
	ctrl+shift+f:           find in path 在指定文件夹或者整个project内搜索，ctrl+shift+r进行替换操作
	ctrl+shift+F7:          在当前文件高亮选定的标识符，esc退出高亮，f3,shift f3向下向上导航高亮标识符
	ctrl+shift+i:           快速查找选中内容定义的位置 quick definition viewer
	ctrl+shift+n:           快速导航到指定文件，弹出一个dialog，输入文件名即可
	ctrl+shift+p:           显示函数方法的参数列表
	ctrl+shift+alt+e:       exploer最近打开的文件
	ctrl+shift+alt+n:       快速打开指定的method，field.弹出一个对话框，输入标识符，选择后跳转到指定内容
	ctrl+shift+alt+t:       快速rename，里面有好几个选项，慢慢理解吧
	
	ese:                    退出tool windows，焦点返回到编辑器里
	
	F12:                    光标从编辑器里移动到最后一个关闭的tool windows里
	
	shift+F6:               rename，自动重命名该变量所有被调用的地方
	shift+esc:              退出并隐藏tool windows,焦点返回编辑器里
	```


- ##### pytcharm

	- pycharm 出现 "`PEP:8 expected 2 blank lines ，found 0 `在声明函数的那一行的上方必须有两行的空行，否则便出现这个情况

	- 显示每个变量 的方法

		- 在运行下选edit configerations ....
		- 勾选Run with python console

	- 设置多个断点

		1. f8 Step Over：在单步执行时，在函数内遇到子函数时不会进入子函数内单步执行，而是将子函数整个执行完再停止，也就是把子函数整个作为一步

		2. 注意：在不存在子函数的情况下Step Over是和Step Into效果一样的

			f7 Step Into：单步执行，遇到子函数就进入并且继续单步执行(即进入子函数）

- vscode

	- 设置方法自动加括号时要先发其他的格式代码工具先关掉

		```json
		"python.autoComplete.addBrackets": true,
		```


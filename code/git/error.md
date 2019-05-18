# git

- ###### Permanently added the RSA host key for IP address '13.250.177.223' to the list of known hosts.

	- 警告的大概意思就是：警告：为IP地址13.250.177.223的主机（RSA连接的）持久添加到hosts文件中，那就来添加吧！

	- 解决办法：nano /etc/hosts 添加一行：

		```json
		13.250.177.223 github.com
		```


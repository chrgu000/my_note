csv 导出时特殊字符导致全局乱码

- 例 ： Pete 💙

- solution: 由于项目默认是UTF-8编码，Excel不支持，所以得把UTF-8转GB2312。

	```php
	function fputcsv2($handle, array $fields, $delimiter = ",", $enclosure = '"', $escape_char = "\\") {
	    foreach ($fields as $k => $v) {
	        $fields[$k] = iconv("UTF-8", "GB2312//IGNORE", $v);  // 这里将UTF-8转为GB2312编码
	    }
	    fputcsv($handle, $fields, $delimiter, $enclosure, $escape_char);
	}
	```

- 测试上述方法只对字符管用，对表情不起作用， 在收到一段可能含有emoji表情的文本内容后，可以简单的使用 json_encode($str) 将其进行JSON编码，此时消息中的表情、中文等字符将会被转为unicode编码显示。（这里进行JSON编码就是为了获得字符的unicode码，所以json_encode函数中不需要增加避免unicode的可选参数了）表情的话用json_encode 转化为16进制在导出

	- 例如： “你好  hello 123″ 将被编码为” \u4f60\u597d \ue415 hello 123 “

	- 简单粗暴式

		```php
		$str = json_encode($str);
		$str = preg_replace("/\\\u[ed][0-9a-f]{3}\\\u[ed][0-9a-f]{3}/","??",$str);//替换成*
		$str = json_decode($str);
		```
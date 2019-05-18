- ##### array_unshift

	- array_unshift — 在数组开头插入一个或多个单元， array_unshift() 将传入的单元插入到 array 数组的开头。注意单元是作为整体被插入的，因此传入单元将保持同样的顺序。所有的数值键名将修改为从零开始重新计数，所有的文字键名保持不变。

		```php
		$queue = array("orange", "banana");
		array_unshift($queue, "apple", "raspberry");
		print_r($queue);
		```

		```php
		Array
		(
		    [0] => apple
		    [1] => raspberry
		    [2] => orange
		    [3] => banana
		)
		```

- ##### arrayKeyChange

	- 更换二维数组的键名

		```php
		public function arrayChangeKey($old, $keys = 'key')
		{
		    $new = [];
		    foreach ($old as $key => $vol) {
		        $new[$vol[$keys]] = $vol;
		    }
		    return $new;
		}
		```

- ##### 数组 字符串转化

	- ###### 将数组转换为字符串

		- implode

			```php
			$arr = array('Hello','World!','I','love','Shanghai!');
			echo implode(" ",$arr);
			```

			```json
			Hello World! I love Shanghai!
			```

	- ###### 字符串转化为数组

		- explode

			```php
			$str = "Hello world. I love Shanghai!";
			print_r (explode(" ",$str));
			```

			```json
			Array ( [0] => Hello [1] => world. [2] => I [3] => love [4] => Shanghai! )
			```
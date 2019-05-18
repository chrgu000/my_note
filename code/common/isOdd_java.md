- - #### isOdd

		- ###### 解法，first come out

			- 判断条件也是boolean 可以去掉 if判断语句

			```java
			@staticmethod
			def is_odd(nums):
			    if nums % 2 == 1:
			        return True
			    else:
			        return False
			        
			```

		- ###### 解法一 改进 -> 解法1: v2

			- 未考虑到负数

			```java
			@staticmethod
			def is_odd_v2(nums):
			    return nums % 2 == 1
			```

		- ###### 解法1 : v2 -> 解法 1: v3

			- 自然数除以2 只有两个结果 0和1 所以可以用下面这种方法

			```java
			@staticmethod
			def is_odd_v3(nums):
			    # return  nums % 2 == 1 || nums % 2 == -1
			    return nums % 2 != 0
			```

		- ###### 解法2 取模操作比较慢，试试位操作，奇数二进制最后一位是1，偶数最后一位是0

			- 奇葩解

			```java
			@staticmethod
			def is_odd_bit(nums):
			    return nums >> 1 << 1 != nums
			```

			- 正常解

			```java
			@staticmethod
			def is_odd_bit_v2(nums):
			    return (nums & 1) == 1
			```

			- 例如43，二进制表示为00101011，注意 b0 位为 1，我们将 43 与 1 做 & 运算

			```json
			    00101011
			&   00000001   (note: 1 is the same as 00000001)
			    --------
			    00000001
			```

			从中看到 & 运算怎样擦除了高位的 b7 ～ b1 位的数据只保留了 b0 位，结果为 1，因此知道 43 是奇数。

			- 实际代码测试过，发现上面的按位与操作和取模操作，实际运行的时间是差不多 因为编译器会将对2的指数的取模操作，优化成位运算操作。
- python3 里类名用驼峰 AbA

- 方法名用下划线 a_a

- True False 没有小写

- 静态方法在方法上用 @staticmethod 标记

- 可以这样编辑数组

	```python
	sqlist = [x*x for x in range(1,11) if x&1]
	[1, 9, 25, 49, 81]
	
	[ch.upper() for ch in 'comprehension' if ch not in 'aeiou']
	```

- 处理异常

	```python
	try:
	    print(math.sqrt(-23))
	except Exception as e:
	    print(str(e))
	```

- 定义从写实例化类的显示，和加法 输出一个类

	```python
	class Fraction:
	
	def __init__(self, top, bottom):
	
	    self.num = top
	    self.den = bottom
	
	# 定义一个默认的显示类的方法
	def __str__(self):
	    return str(self.num)+"/"+str(self.den)
	
	def __add__(self, otherfraction):
	    newnum = self.num * otherfraction.den + self.den * otherfraction.num
	    newden = self.den * otherfraction.den
	    return Fraction(newnum, newden)
	    
	def __eq__(self, otherfraction):
	    return self.num * otherfraction.den == otherfraction.num * self.den
	
	
	# myf = Fraction(3, 5)
	# print(myf)
	# print("I ate", myf, "of the pizza")
	# print(myf.__str__())
	# print(str(myf))
	myf = Fraction(1, 4) + Fraction(1, 2)
	print(myf)
	```
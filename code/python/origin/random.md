random.randrange(start, stop[, step]) 从range(start, stop, step)返回一个start到end范围内的随机整数（译者注：start，end，step都是整数，不包含end），可以指定step。这等同于choice(range(start, stop, step)),但实际上没有编译range对象。 位置参数模式与range()匹配。不应使用关键字参数，因为函数可能以意想不到的方式使用它们。 在版本3.2中更改： randrange()更复杂地生成平均分布的值。以前，它使用类似int(random()*n)这样可能产生轻微的不均匀分布。

```python
randrange(100, 1000, 3) :  520
```


### 1 基本语法

#### 1.1 呈现位置

- 正文(inline)中的LaTeX公式用`$...$`定义

- 语句为`$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$` 

- 显示在当前行内

	```
	(简书目前不支持mathjax 只好暂时用图片代替了→_→)
	```

	

	![img](https:////upload-images.jianshu.io/upload_images/436556-f69f0619c0c46d9f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/140/format/webp)

	

- 单独显示(display)的LaTeX公式用`$$...$$`定义，此时公式居中并放大显示

- 语句为$$\sum_{i=0}N\int_{a}{b}g(t,i)\text{d}t$$

- 显示为

	

	![img](https:////upload-images.jianshu.io/upload_images/436556-dfe2fe10c60897b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/156/format/webp)

	

- 下列描述语句中若非特别指出均省略`$...$` 

### 2 希腊字母

| 显示 |   命令   | 显示 |  命令  |
| :--: | :------: | :--: | :----: |
|  α   |  \alpha  |  β   | \beta  |
|  γ   |  \gamma  |  δ   | \delta |
|  ε   | \epsilon |  ζ   | \zeta  |
|  η   |   \eta   |  θ   | \theta |
|  ι   |  \iota   |  κ   | \kappa |
|  λ   | \lambda  |  μ   |  \mu   |
|  ν   |   \nu    |  ξ   |  \xi   |
|  π   |   \pi    |  ρ   |  \rho  |
|  σ   |  \sigma  |  τ   |  \tau  |
|  υ   | \upsilon |  φ   |  \phi  |
|  χ   |   \chi   |  ψ   |  \psi  |
|  ω   |  \omega  |      |        |

- 若需要大写希腊字母，将命令首字母大写即可。
	 \Gamma呈现为

	

	![img](https:////upload-images.jianshu.io/upload_images/436556-9a4b775a910858e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/109/format/webp)

	

- 若需要斜体希腊字母，将命令前加上var前缀即可。

	

	![img](https:////upload-images.jianshu.io/upload_images/436556-f45007284686302b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/134/format/webp)

	

### 3 字母修饰

##### 3.1  上下标

- 上标：`^` 

- 下标：

	```
	_
	```

	

	![img](https:////upload-images.jianshu.io/upload_images/436556-94b27f9c8c8ecfef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/209/format/webp)

	

##### 3.2 矢量



![img](https:////upload-images.jianshu.io/upload_images/436556-b28d6791cb87765b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/104/format/webp)





![img](https:////upload-images.jianshu.io/upload_images/436556-d6d39c57da3aec1f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/230/format/webp)



##### 3.3 字体



![img](https:////upload-images.jianshu.io/upload_images/436556-45c8673c41af7c42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/446/format/webp)



##### 3.4 分组



![img](https:////upload-images.jianshu.io/upload_images/436556-434dd3242e693d70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/375/format/webp)



##### 3.5 括号



![img](https:////upload-images.jianshu.io/upload_images/436556-6ef5dd4fd56680f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/599/format/webp)



##### 3.6 求和、极限与积分



![img](https:////upload-images.jianshu.io/upload_images/436556-fb2604765d03c8d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/526/format/webp)



##### 3.7 分式与根式



![img](https:////upload-images.jianshu.io/upload_images/436556-ccb12bbfeaf06412.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/440/format/webp)



##### 3.8 特殊函数



![img](https:////upload-images.jianshu.io/upload_images/436556-95f54171208e97bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/562/format/webp)



##### 3.9 特殊符号



![img](https:////upload-images.jianshu.io/upload_images/436556-a0a75e713b2b3e9c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/681/format/webp)



##### 3.10 空格



![img](https:////upload-images.jianshu.io/upload_images/436556-f9b9a026db748466.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/264/format/webp)



### 4 矩阵

##### 4.1 基本语法

起始标记`\begin{matrix}`，结束标记`\end{matrix}`
 每一行末尾标记`\\\`，行间元素之间以`&`分隔
 举例:

```
$$\begin{matrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{matrix}$$
```

呈现为：



![img](https:////upload-images.jianshu.io/upload_images/436556-1548fa2d1079ef70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/113/format/webp)



##### 4.2 矩阵边框

- 在起始、结束标记处用下列词替换 `matrix` 
-  `pmatrix` ：小括号边框
-  `bmatrix` ：中括号边框
-  `Bmatrix` ：大括号边框
-  `vmatrix` ：单竖线边框
-  `Vmatrix` ：双竖线边框

##### 4.3 省略元素

- 横省略号：`\cdots` 
- 竖省略号：`\vdots` 
- 斜省略号：`\ddots`
	 举例

```
$$\begin{bmatrix}
{a_{11}}&{a_{12}}&{\cdots}&{a_{1n}}\\
{a_{21}}&{a_{22}}&{\cdots}&{a_{2n}}\\
{\vdots}&{\vdots}&{\ddots}&{\vdots}\\
{a_{m1}}&{a_{m2}}&{\cdots}&{a_{mn}}\\
\end{bmatrix}$$
```

呈现为：



![img](https:////upload-images.jianshu.io/upload_images/436556-72c03690ce9e63b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/235/format/webp)



##### 4.4 阵列



![img](https:////upload-images.jianshu.io/upload_images/436556-19f8205a2b599b86.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/384/format/webp)



举例

```
$$\begin{array}{c|lll}
{↓}&{a}&{b}&{c}\\
\hline
{R_1}&{c}&{b}&{a}\\
{R_2}&{b}&{c}&{c}\\
\end{array}$$
```

呈现为



![img](https:////upload-images.jianshu.io/upload_images/436556-84dac3a98e0e44a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/154/format/webp)



##### 4.5 方程组

- 需要cases环境：起始、结束处以{cases}声明

举例

```
$$\begin{cases}
a_1x+b_1y+c_1z=d_1\\
a_2x+b_2y+c_2z=d_2\\
a_3x+b_3y+c_3z=d_3\\
\end{cases}
$$
```

呈现为



![img](https:////upload-images.jianshu.io/upload_images/436556-8e608fa9d8906bf1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/250/format/webp)



### 5 参考文献

作者：ColdRomantic

链接：https://www.jianshu.com/p/a0aa94ef8ab2

来源：简书

简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。
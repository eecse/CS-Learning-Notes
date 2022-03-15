# Matlab 基础与图像处理工具包

> - Matlab基本语法
> - 向量和矩阵的创建
> - 向量和矩阵的操作
> - Matlab图像处理工具包
> - Matlab的控制语句

## Matlab基本语法

### 什么是Matlab

> Cleve Moler创造的一个用于数学，工程的计算工具。

> （就是这么简洁）

### Matlab变量

> 变量命名规则和绝大多数编程语言一样，blablablah

```matlab
# MATLAB Commands
>> x = 1

x =

     1
>> y1 = 3 * x^2 + 2*x -6; # 用`;`来抑制输出
>> 3*pi^2 + 2*pi -6	# pi为matlab内置变量

ans =

   29.8920
```

### Matlab作为计算器

举例: `二次方程根的求解`
$$
x = \frac{-b \pm \sqrt(b^2-4ac)}{2a}
$$
基本运算符：

加: `+`;

减: `-`;

乘: `*`;

除: `/`;

指数: `^`;

括号: `(``)`;

```matlab
# MATLAB Commands
>> a = 3;
>> b = 2;
>> c = -6;
>> x1 = (-b+sqrt(b^2-4*a*c))/(2*a)

x1 =

    1.1196
>> x2 = (-b-sqrt(b^2-4*a*c))/(2*a)

x2 =

   -1.7863
```

### Matlab 函数

> matlab函数调用也与其他编程语言大致相同

如:

```python
# Example Functions
y = fun(x)
y = sin(x)
y = log10(x)
```

> 值得一提的是，matlab本身是为矩阵打造的，所以matlab函数的参数可以是一个矩阵，如

```matlab
# MATLAB Commands
>> x = [0, pi/2, pi, 3*pi/2, 2*pi];
>> sin(x)

ans =

         0    1.0000    0.0000   -1.0000   -0.0000
```

`min`函数

```matlab
# MATLAB Commands
>> a = min(ans)

a =

    -1
>> [a,I] = min(ans) # 当提供两个变量时，min会返回值(第一个变量)，值的下标（第二个变量）

a =

    -1


I =

     4
```

`plot(x, y)`函数

```matlab
>> plot(x, ans)
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/plot.png" alt="function" style="zoom:50%;" />

## 向量和矩阵的创建

> 简单的函数例子

$$
y = 3x^2 + 2x-6
$$

### 创建向量

```matlab
>> x = [-2, -1, 0, 1, 2]	# 创建行向量

x =

    -2    -1     0     1     2

>> xCol = [-2;-1;0;1;2]		# 创建列向量

xCol =

    -2
    -1
     0
     1
     2
>> y = [-2,-5,-6,-1,10]

y =

    -2    -5    -6    -1    10

>> plot(x, y)
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/plot_2.png" alt="function" style="zoom:50%;" />

### 创建矩阵

$$
\left[
\begin{array}{ccc}
	a_{11}&  a_{12} & a_{13}  \\
  a_{21}&  a_{22} & a_{23}  \\
  a_{31}&  a_{32} & a_{33}  
\end{array}
\right]
$$

> 例： 创建一个3 x 3矩阵

$$
\left[
\begin{array}{ccc}
	1 &  2 & 3  \\
    4 &  5 & 6  \\
    7 &  8 & 9
\end{array}
\right]
$$

```matlab
# MATLAB Commands
>> M = [1, 2, 3; 4, 5, 6;7, 8, 9]

M =

     1     2     3
     4     5     6
     7     8     9
```

### 矩阵创建函数

- `eye`: 单位矩阵

- `ones`: 矩阵赋值为`1`

- `zeros`: 矩阵赋值为`0`

- `rand`: 矩阵赋值为随机值

- `diag`: 三角矩阵

```matlab
# MATLAB Commands
>> e = eye(5)

e =

     1     0     0     0     0
     0     1     0     0     0
     0     0     1     0     0
     0     0     0     1     0
     0     0     0     0     1

>> x = zeros(5)

x =

     0     0     0     0     0
     0     0     0     0     0
     0     0     0     0     0
     0     0     0     0     0
     0     0     0     0     0

>> x = zeros(5, 2) 	# 五行二列矩阵

x =

     0     0
     0     0
     0     0
     0     0
     0     0

>> x = rand(3)

x =

    0.0975    0.9575    0.9706
    0.2785    0.9649    0.9572
    0.5469    0.1576    0.4854
```

## 向量和矩阵的操作

> 之前提到的简单函数

$$
y = 3x^2 + 2x-6
$$



<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/plot_2.png" alt="function" style="zoom:50%;" />

> 显然，输出与我们熟知的二次函数曲线还是有差距的，那么，如何得到一条相对光滑的曲线呢？

### 向量的计算

> 我们尝试下直接对x向量进行运算

```matlab
# MATLAB Commands
>> x = -2:0.1:2;
>> y = 3 * x^2 + 2*x -6
错误使用  ^  (line 51)
用于对矩阵求幂的维度不正确。请检查并确保矩阵为方阵并且幂为标量。要执行按元素矩阵求幂，请使用 '.^'。
```

> **注意**：`*`, `^`, `/` 在matlab中都是优先用于矩阵运算的，如果我们想做元素级别的操作(Element-wise operations),就该用到如下的运算符：`.*`, `./`, `.^`

举例：

```matlab
v1 [1, 2, 3, 4]
v2 [2, 4, 6, 8]

v1.*v2 = [1*2, 2*4, 3*6, 4*8]
v1./v2 = [1/2, 2/4, 3/6, 4/8]
v1.^2 = [1^2, 2^2, 3^2, 4^2]
```

> 由于矩阵的`+`, `-`以及数乘运算并不特殊，所以这些运算均无需特殊化处理

```matlab
v1 + v2 = [1+2, 2+4, 3+6, 4+8]
v1 - v2 = [1-2, 2-4, 3-6, 4-8]
```

> 回到一开始的操作

```matlab
# MATLAB Commands
>> x = -2:0.1:2;
>> y = 3*x.^2 + 2*x - 6

y =

  列 1 至 9

    2.0000    1.0300    0.1200   -0.7300   -1.5200   -2.2500   -2.9200   -3.5300   -4.0800

  列 10 至 18

   -4.5700   -5.0000   -5.3700   -5.6800   -5.9300   -6.1200   -6.2500   -6.3200   -6.3300

  列 19 至 27

   -6.2800   -6.1700   -6.0000   -5.7700   -5.4800   -5.1300   -4.7200   -4.2500   -3.7200

  列 28 至 36

   -3.1300   -2.4800   -1.7700   -1.0000   -0.1700    0.7200    1.6700    2.6800    3.7500

  列 37 至 41

    4.8800    6.0700    7.3200    8.6300   10.0000
>> plot(x, y)
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/plot_smoother.png" alt="Smoother" style="zoom:50%;" />

### 访问矩阵元素

> 如下矩阵： 横向分别表示周一至周五，纵向则分别表示下午1点至6点，其值指的是相应时间点的`污染指数`

$$
data =\left[
\begin{array}{ccc}
	18 & 32 & 26 & 28 & 46 \\
	25 & 42 & 35 & 30 & 52 \\
	43 & 44 & 37 & 52 & 54 \\
	49 & 38 & 59 & 54 & 55 \\
	55 & 48 & 61 & 69 & 61 \\
	48 & 34 & 56 & 42 & 56 
\end{array}
\right]
$$

> 如果我们需要得到其中某个元素的值，那么如`x = data(5, 3)`, 我们就取得了该矩阵`第五行`, `第三列`的元素值，即`61`.

> 如果我们需要获得一个更大的子集呢？

> 比如我们要分别取得`周二到周四`下午`1点`和下午`5点`的污染指数：

```matlab
# MATLAB commands
>> rows = [1, 5];
>> cols = 2: 4;
>> subdata = data(rows, cols);
```

$$
subdata=\left[
\begin{array}{ccc}
  32 & 26 & 28 \\
	48 & 61 & 69
\end{array}
\right]
$$

> 我们经常需要获取某一纬度的元素（在这个例子中某一行或者某一列的元素），matlab为这个操作提供了简便的方式，比如我们需要获取第一列的元素：

```matlab
# MATLAB commands
>> col1 = data(:, 1);
```

### 矩阵的统计函数

> 如下矩阵： 横向分别表示科目，纵向则分别表示不同的学生，其值指的是相应学生对应科目的`考试成绩`

$$
scores=\left[
\begin{array}{ccc}
  85 & 88 & 92 \\
  88 & 95 & 90 \\
  40 & 60 & 75 \\
  60 & 82 & 82
\end{array}
\right]
$$

```matlab
# MATLAB commands
>> testAvg = mean(scores)

testAvg =

   68.2500   81.2500   84.7500 # testAvg 得出了每一列的平均值，即每门科目的平均值

```

> `testAvg` 得出了每一列的平均值，即每门科目的平均值,因此`mean`函数实际上默认将每一列作为一个数据集，所得出来的行向量为每一列元素的平均值

> 如果我们想计算各个学生每门科目的平均值呢？

```matlab
# MATLAB commands
>> studentAvg = mean(scores, 2)

studentAvg =

   88.3333
   91.0000
   58.3333
   74.6667
```

> `mean`的第二个参数指的是函数运用的`维度`, 在这里即`行向量`

> 最后，我们想要计算出所有成绩的平均值，这里我们有两种思路，一是先计算出每一列的平均值，再对该平均值向量运用`mean`函数， 二是直接将`scores`矩阵转为一个一维向量，再运用`mean`函数来计算平均值

```matlab
# MATLAB commands
>> mean(mean(scores))

ans =

   78.0833

>> mean(scores(:))

ans =

   78.0833
```

> 除了`mean`以外，还有许多相关的统计函数如`max`, `min`, `std`在matlab中都已集成，可以自行尝试。

### 指定数组的大小和长度

> 指定有如下属性的向量和矩阵

```matlab
v <1x24 double>
A <24x30 double>
```

分别执行`length`函数

```matlab
# MATLAB commands
>> n = length(v)
n = 
		24
>> m = length(A)
m = 
		30
```

> 对于向量，无论是行向量还是列向量，`length`函数都会返回向量中元素的个数，然而，如果对于矩阵，`length`则会返回**其较大的一个纬度的数值**，这就会造成一定的困扰，所以，对于矩阵

```matlab
>> [nrows, ncols] = size(A);
nrows 24
ncols 30
```

> 我们选择使用`size`函数，以保证每一个值都被正常的接受

## 图像处理工具包

> `Image Processing Toolbox`

### 加载与保存图像

灰度图像：

```matlab
# MATLAB commands
>> moon = imread('Fig0338(a)(blurry_moon).tif');
moon <540x466 uint8>	# 以矩阵形式保存
>> imshow(moon)
```

> 我们可以发现图像是以`矩阵`的形式存储的

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/moon.png" alt="moon" style="zoom:50%;" />

> 对图像进行一系列处理后保存

```matlab
# MATLAB commands
>> imwrite(newMoon, 'newMoonPic.png');
```

> 彩色图像：

```matlab
# MATLAB commands
>> lena = imread('lena_std.bmp');
lena <512x512x3 uint8>	# 以矩阵形式保存
>> imshow(lena)
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/lena.png" alt="lena" style="zoom:50%;" />

> 我们可以发现，彩色图像是用一个`三维矩阵`存储的

### 图像矩阵处理

> `灰度图像`是一个二维矩阵表示的

```matlab
# MATLAB commands
>> grayMan = imread('Fig2.22(b).jpg');
>> imshow(grayMan)
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/greyMan.png" alt="GreyMen" style="zoom:50%;" />

截取一部分

```matlab
>> Icrop = grayMan(32:101,87:175);
>> imshow(Icrop)
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/Icorp.png" alt="Icrop" style="zoom:50%;" />

> `彩色图像`是一个三维矩阵表示的

```matlab
# MATLAB commands
>> I = imread('lena_std.bmp');
>> Ired = I(:,:,1); # 红分量
>> Igreen = I(:,:,2); # 绿分量
>> Iblue = I(:,:,3); # 蓝分量
```

截取一个`彩色图像`

```matlab
>> Icrop = I(100:300, 60:490, :);
```

> 注意，截取的是前两维的子集，第三维用`:`全选

> 我们也可以对图像矩阵进行修改，比如我们显示出三个分量的图像：

```matlab
# MATLAB commands
>> I = imread('lena_std.bmp');
>> Ired = I;
>> Ired(:,:,2) = 0;
>> Ired(:,:,3) = 0;
>> Igreen = I;
>> Igreen(:,:,1) = 0;
>> Igreen(:,:,3) = 0;
>> Iblue = I;
>> Iblue(:,:,1) = 0;
>> Iblue(:,:,2) = 0;

>> subplot(2,2,1);imshow(I);title('Origin');
>> subplot(2,2,2);imshow(Ired);title('R');
>> subplot(2,2,3);imshow(Igreen);title('G');
>> subplot(2,2,4);imshow(Iblue);title('B');
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/RGB.png" alt="RGB" style="zoom:50%;" />

### 转换图像数据类型

> `Gamma Adjustment`伽马校准

$$
I_{new} = 255 * \left( \frac{I_{old}}{255} \right)^y
$$

其中`y`为校准参数

```matlab
# MATLAB commands
>> I1 = imread('Fig0338(a)(blurry_moon).tif');
>> gamma = 0.5;
>> I2 = 255*(I1/255).^gamma;
错误使用  .^ 
整数只能提升为正整数幂。
```

> 我们可以发现这个操作matlab报错了，原因是`imread`读取的矩阵数据类型为`uint8`，运算后会失去数据，我们可以使用`im2double`函数将原`uint8`数字类型转为`double`型，方便进行运算

```matlab
# MATLAB commands
>> I1 = imread('Fig0338(a)(blurry_moon).tif');
>> I2 = im2double(I1);
>> gamma = 0.5;
>> I2 = I2.^gamma;
>> subplot(1,2,1);imshow(I1);title('Origin');
>> subplot(1,2,2);imshow(I2);title('Adjusted');
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/gamma.png" alt="gamma" style="zoom:50%;" />

### 空间图像过滤

> 加强部分图像属性或过滤图像

`fspecial`函数，以及常用过滤参数

```matlab
fspecial('type', parameters)
```

`Average`:

`Disk`:

`Gaussian`:

`Laplacian`:

`Log`:

`Motion`:

`Prewitt`:

`Sobel`:

> 我们用`laplacian`转换来提取月球图像的边缘

```matlab
# MATLAB commands
>> moon = imread('Fig0338(a)(blurry_moon).tif');
>> h = fspecial('laplacian', 0.5);
>> newMoon = imfilter(moon, h);
>> imshow(newMoon);
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/edge.png" alt="edge" style="zoom:50%;" />

> 我们还可以做一些操作使得图像更锐利

```matlab
# MATLAB commands
>> sharpend = moon - newMoon;
>> subplot(1,3,1);imshow(moon);title('origin');
>> subplot(1,3,2);imshow(newMoon);title('edge');
>> subplot(1,3,3);imshow(sharpend);title('sharpened');
```

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/laplacian_trans.png" alt="processed" style="zoom:50%;" />

## Matlab流程控制

> 流程控制是任何编程语言都共有的属性之一，`matlab`也不例外

### 写一个`for`循环

>假设一个场景，年化率是`0.02`，初始资金为`20000`,需要将之后一百年的资金状况计算出来并存入数组

```matlab
# MATLAB script
r = 0.02;
balance = zero(1, 100);
balance(1) = 20000;
for k = 1: 99
	balance(k+1) = (1+r) * balance(k);
end
```

### `If`-`ELSE`语句

> 假设有如下的场景，考虑停车费用问题

<img src="https://picgo-1252947055.cos.ap-guangzhou.myqcloud.com/parking.png" alt="parking" style="zoom:50%;" />

```matlab
# MATLAB script
if hours <= 1
	fee = 0;
elseif hours > 1 & hours < 7
	fee = 5*(hours - 1);
else
	fee = 35;
end
```

# 完

# Latex数学公式

> 在Markdown中 `-`和 `/`需要用 `/`转义！

<!--more-->

## 行内公式

```latex
行中公式a^2+b^2=c^2在同一行中显示
```

行中公式$a^2+b^2=c^2$在同一行中显示

## 块状公式

```latex
块状公式 3^2+4^2=5^2
```

块状公式

$3^2+4^2=5^2$

## 分数

```latex
1+2+3+\dots+(n-1)+n = \frac{n(n+1)}{2}
```

$1+2+3+\dots+(n-1)+n = \frac{n(n+1)}{2}$

## 累加

```latex
\sum_{i=1}^{n}i=\frac{n(n+1)}{2}
```

$\sum_{i=1}^{n}i=\frac{n(n+1)}{2}$

## 极限

```latex
\lim_{x\rightarrow{\infty}}(1+\frac{1}{x})^{x}=e
```

$\lim_{x\rightarrow{\infty}}(1+\frac{1}{x})^{x}=e\\$

## 积分

```latex
\int_{a}^{b}f(x)dx=F(b)-F(a)
```

$\int_{a}^{b}f(x)dx=F(b)-F(a)\\$

## 导数

```latex
\frac{\partial f(x)}{\partial x}=x^2
```

$\frac{\partial f(x)}{\partial x}=x^2$

## 分行

```latex
x+y = z\\a=4
```

$$
x+y = z \\ a=4
$$

## 分段函数

```latex
f(x) = 
\begin{cases}
x+2y^2-z+\frac{1}{x} & x = 10\\
-x & x < 1
\end{cases}
```

$$
f(x) = 
\begin{cases}
x+2y^2-z+\frac{1}{x} & x = 10\\
-x & x < 1
\end{cases}
$$

## 矩阵

```latex
\left[
\begin{array}{ccc}
	a_{11}&  a_{12} & a_{13}  \\
  a_{21}&  a_{22} & a_{23}  \\
  a_{31}&  a_{32} & a_{33}  
\end{array}
\right]
```

$$
\left[
\begin{array}{ccc}
	a_{11}&  a_{12} & a_{13}  \\
  a_{21}&  a_{22} & a_{23}  \\
  a_{31}&  a_{32} & a_{33}  
\end{array}
\right]
$$

## 行列式

```latex
\left|
\begin{array}{ccc}
	a_{11}&  a_{12} & a_{13}  \\
  a_{21}&  a_{22} & a_{23}  \\
  a_{31}&  a_{32} & a_{33}  
\end{array}
\right|
```

$$
\left|
\begin{array}{ccc}
	a_{11}&  a_{12} & a_{13}  \\
  a_{21}&  a_{22} & a_{23}  \\
  a_{31}&  a_{32} & a_{33}  
\end{array}
\right|
$$

## 分块矩阵

```latex
\left[
\begin{array}{cc|c}
1&1&1 \\ 
2&2&2 \\  \hline
3&3&3 
\end{array}
\right]
```

$$
\left[
\begin{array}{cc|c}
1&1&1 \\  
2&2&2 \\  \hline
3&3&3 
\end{array}
\right]
$$


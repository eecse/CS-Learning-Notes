## Julia学习笔记

安装好Julia环境之后，在terminal中输入Julia，启动Julia CLI环境

```julia
# bobby @ MacBook-Pro in ~ [17:49:20] 
$ julia
               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.7.0 (2021-11-30)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

julia>
```

### 变量赋值

和大多数语言一样，Julia也是通过`=`进行赋值的：

```julia
julia> x = 3
3

julia> y = 2x
6
```

Julia默认显示最后一个操作的输出，可以用`;`结尾来抑制输出（类似Matlab)

用`typeof`可以查看变量的类型

```julia
julia> typeof(y)
Int64
```

### 函数

对于一些简单的函数，可以使用one-line function定义：

```julia
julia> f(x) = x + 2
f (generic function with 1 method)

julia> f(10)
12
```

对于一些相对比较长的函数，可以使用`function`关键字来定义：

```julia
julia> function g(x , y)
           z = x + y
           return z ^ 2
       end
g (generic function with 1 method)

julia> g(1, 2)
9
```

### for 循环

用`for`可以遍历指定的值：

```julia
julia> let s = 0
           for i in 1:10
               s += i
           end
           s
       end
55
```

如上为Julia中用`for`循环计算1到10的和，其中`1:10`指[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

上面还用到了`let`这个关键字来定义一个新的本地变量`s`。一般如果需要实现这样的操作，我们可以用一个函数来实现它，以方便重复使用：

```julia
julia> function mysum(n)
           s = 0
           
           for i in 1:n
               s += i
           end
           
           return s
       end
mysum (generic function with 1 method)

julia> mysum(100)
5050
```

### if条件语句

使用`==`、`!=`、`>`、`<`、`>=`、`<=`等条件语句可以得出`bool`型变量:

```julia
julia> a = 3
3

julia> a == 3
true

julia> typeof(a == 3)
Bool

julia> a > 5
false
```

有了`bool`型之后，可以使用`if`来控制程序：

```julia
julia> if a < 5
           "small"
       else
           "big"
       end
"small"
```

### 数组(向量)

```julia
julia> v = [1, 2, 3]
3-element Vector{Int64}:
 1
 2
 3

julia> typeof(v)
Vector{Int64} (alias for Array{Int64, 1})
```

用方括号可以定义一维向量，向量的下标从1开始，可以用如下的方式访问向量元素

```julia
julia> v[2]
2

julia> v[2] = 10
10

julia> v
3-element Vector{Int64}:
  1
 10
  3
```

和python一样，可以使用列表生成式来定义一个向量：

```julia
julia> v2 = [i^2 for i in 1:10]
10-element Vector{Int64}:
   1
   4
   9
  16
  25
  36
  49
  64
  81
 100
```

### 二维数组（矩阵）

Julia生成矩阵的方式如下：

```julia
julia> [1 2
   	   3 4]

2×2 Matrix{Int64}:
 1 2
 3 4
```

对于一些特殊矩阵，我们可以使用一些内置的函数生成：

```julia
julia> zeros(5, 5)
5×5 Matrix{Float64}:
 0.0  0.0  0.0  0.0  0.0
 0.0  0.0  0.0  0.0  0.0
 0.0  0.0  0.0  0.0  0.0
 0.0  0.0  0.0  0.0  0.0
 0.0  0.0  0.0  0.0  0.0

julia> zeros(Int, 5, 5)
5×5 Matrix{Int64}:
 0  0  0  0  0
 0  0  0  0  0
 0  0  0  0  0
 0  0  0  0  0
 0  0  0  0  0
```

也可以通过双重`for`循环来生成制定序列的矩阵:

```julia
julia> [i + j for i in 1:5, j in 1:6]
5×6 Matrix{Int64}:
 2  3  4  5   6   7
 3  4  5  6   7   8
 4  5  6  7   8   9
 5  6  7  8   9  10
 6  7  8  9  10  11
```

Julia的基础部分就到这里了

# 小学生 算法入门 案例精讲系列 2024 Python 版

## 系列之四：求阶和、阶乘，学习迭代和递归

---

**说明：**

> 本文内容较长，持续更新中，连载于：
> 
> - `github` [loongba/Algorithm_Learning_Insights](https://github.com/LoongBa/Algorithm_Learning_Insights)
> 
> - `gitcode` [loongba/Algorithm_Learning_Insights](https://gitcode.com/LoongBa/Algorithm_Learning_Insights)
> 
> - `gitee` [loongba/Algorithm_Learning_Insights](https://gitee.com/LoongBa/Algorithm_Learning_Insights)
> 
> - [loongba 个人网站1](https://coffeedrunk.cn) | [loongba 个人网站2](https://loongba.cn)

在 `github` 或 `markdown` 编辑器中阅读本文时，可打开其目录功能方便浏览和跳转。

> - `github` 页面中，点击文档右上角的目录图标；
> 
> - `marktext` 编辑器中，按 `Ctrl-K`

---

## 算法入门 案例精讲 Python 版 目录

0. [前言：使用说明](README.md)

1. [求回文数，练习拆分数字和进制转换](Readme_01.md)

2. [求水仙花数，了解枚举和迭代](Readme_02.md)

3. [判断素数，初步学习穷举法及优化](Readme_03.md)

4. [求阶和、阶乘，学习迭代和递归](Readme_04.md)

5. [求斐波那契数列，学习迭代和递归](Readme_05.md)

6. [辗转相除法求最大公约数，继续练习迭代和递归](Readme_06.md)

7. [求解汉诺塔问题，继续练习迭代和递归](Readme_07.md)

8. [求解迷宫问题，初步学习回溯](Readme_08.md)

9. [求解八皇后问题，继续练习回溯](Readme_09.md)

---

# 四、求阶和、阶乘，学习迭代和递归

背景知识：

##### 1. 阶和：

> `阶和` 是指从 `1` 到某个正整数 `n` 的 `所有正整数的和`。
> 
> `阶和` 可以用公式表示为：
> 
> \sum_{i=1}^{n} i = 1 + 2 + 3 + ... + n

##### 2. 阶乘：

> `阶乘` 是指一个正整数 `n` 与 `小于等于 n` 的所有 `正整数` 的 `乘积`。
> 
> `阶乘` 可以用符号 `!` 表示，例如5的阶乘可以表示为 `5!`，其计算方法为：
> 
> 5! = 5 × 4 × 3 × 2 × 1 = 120
> 
> `阶乘` 在数学和计算机中经常被使用，常用于排列组合、概率统计、递归算法等领域。

#### 编程练习：分别用迭代和递归的方式编写两个函数，计算 n 的阶和与阶乘

##### 1. 迭代方式：

> [求阶和阶乘 C 代码](https://github.com/coffeescholar/C_CPP-Learning/blob/main/%E7%AE%97%E6%B3%95%E5%85%A5%E9%97%A8%E7%BB%83%E4%B9%A0/04_%E6%B1%82%E9%98%B6%E5%92%8C%E9%98%B6%E4%B9%98_%E4%BA%86%E8%A7%A3%E9%80%92%E6%8E%A8%E5%92%8C%E9%80%92%E5%BD%92.c)

```python
# 计算 n 的阶和
def sum_of_Factorials(n):
    sum = 0
    for i in range(1, n+1):
        sum += i
    return sum

# 计算 n 的阶乘
def factorial(n):
    fact = 1
    for i in range(1, n+1):
        fact *= i
    return fact
```

例如，如果想计算数字 5 的阶和和阶乘，可以调用函数：

```python
n = 5
print(sum_of_Factorials(n))   # 输出：15
print(factorial(n))           # 输出：120
```

##### 2. 递归方式：

上面的代码中，解决问题所采用的是 迭代 的编程方式。

> 递推是指根据已知的初始条件和递推公式，通过迭代计算来求解问题的方法。在递推中，问题的解是通过不断迭代计算前一项或多项得到的。

进一步思考，很显然，求 `5!` 先求 `4!`，因为 `5! = 4! × 5`，阶和类似。

那么，泛化推理可以得到结论：求 `n!` 就相当于先求 `(n-1)!` 然后乘以 `n`，可以表示为：

> n! = f(n-1) × n

那么，在 `factorial()` 函数里，可以简化为：

```python
# 计算阶和的递归函数
def sum_of_Factorials_Recursive(n):
    return n + sum_of_factorials(n-1)

# 计算阶乘的递归函数
def factorial_Recursive(n):
    return n * factorial_Recursive(n-1)
```

但因为参数 `n` 可能为负数，所以需要加上限制条件，否则就会无穷无尽、无法终止了。

```python
# 计算阶和的递归函数
def sum_of_Factorials_Recursive(n:int):
    if n <= 0 return 0  # 终止递归（以后还要学习处理错误的方式）
    if n == 1:
        return 1
    else:
        return n + sum_of_Factorials_Recursive(n-1)

# 计算阶乘的递归函数
def factorial_Recursive(n:int):
    if n < 0 return 0 # 终止递归（以后还要学习处理错误的方式）
    if n == 1:
        return 1
    else:
        return n * factorial_Recursive(n-1)
```

于是，将求阶和、求阶乘的方式，从循环 `1 - n` 的递推方式，改为了 **"自己调用自己" 的递归方式**。

——对比可见，采用`递归方式`的代码逻辑，理解起来简单多了。

但一定注意：采用递归方式必须确保有 ”终止条件“，否则就会陷入 “无穷无尽” 的`无限递归`。

逻辑上的 “无穷无尽”，在计算机编程中，`无限递归` 会导致运行程序的计算机为了避免耗尽内存资源而终止该程序——**你的程序将被强迫终止**。

**特别注意**：实际应用中，并不采用递归的方式来求解`阶和`、`阶乘` 以及后面的 `斐波那契数列` 等等，有更优的方法。学习 `递归` 的主要目的是**掌握递归的思维方式和处理好其中的推出条件**。

> 递归是指一个函数在其定义中调用自身的过程。在递归中，函数通过将问题分解为更简单的子问题来解决复杂的问题。
> 
> 递归通常包含两个要素：
> 
> 1. 递归基础（base case）：定义递归的终止条件，当满足终止条件时，递归将停止。
> 2. 递归步骤（recursive step）：将原始问题分解为一个或多个更小的子问题，并通过调用自身来解决这些子问题。
> 
> 递归在解决问题时可以提供简洁而优雅的解决方案，特别是对于那些可以分解为相同类型的子问题的问题。然而，递归也需要小心使用，确保终止条件正确设置，避免进入无限递归的循环。
> 
> 需要注意的是，递归不仅限于函数调用自身，也可以是函数调用其他函数，只要函数最终可以通过一系列调用解决问题。

##### 3. 对比递推与递归：

> 递推是指根据已知的初始条件和递推公式，通过迭代计算来求解问题的方法。在递推中，问题的解是通过不断迭代计算前一项或多项得到的。
> 
> 递推与递归有以下区别和特点：
> 
> 1. **调用方式**：递归是函数调用自身，而递推是通过循环迭代计算得到结果。
> 2. **结构**：递归是将问题分解为子问题并通过递归调用来解决，而递推是根据已知的初始条件和递推公式来计算得到结果。
> 3. **性能**：递推通常比递归具有更好的性能，因为递推不需要频繁地进行函数调用，而是通过循环迭代计算得到结果。
> 4. **空间复杂度**：递归在计算过程中需要使用函数调用栈来保存每一次递归调用的状态，可能会**占用较多的内存空间**。而递推只需要使用有限的变量来保存计算结果，空间复杂度相对较低。
> 5. **适用场景**：递归通常适用于问题可以自然地分解为子问题的情况，而递推则适用于问题可以通过迭代计算得到结果的情况。
> 
> 总的来说，在实际应用中，需要根据问题的特点和需求选择适合的方法。

后续，继续用递推、递归的方式解决求斐波那契数列的练习。

> **单词助手：**
> 
> - `recursion n. 递归`，`recursive adj. 递归的、递归式的`
> 
> - `iteration n. 递推`，`iterative adj. 迭代的、循环的、递推的`
>   
>   > 注意：**虽然递推和迭代用同一个单词**，严格意义上，**递推不等于迭代**，**迭代也不是简单的循环**：
>   > 
>   > - 迭代主要强调`重复执行特定的处理`，计算机编程领域往往用循环来实现迭代，所以`有时候会混用 循环 和 迭代 这两个概念`；
>   > 
>   > - 而 `"递推" 则是一种数学或逻辑推理的方法`，通过已知的初始条件和递推关系式，逐步推导出后续的数值或解决方案。所以，`在某些情况下会混用 递推 和 迭代 这两个概念`。

---

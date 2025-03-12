# 小学生 算法入门 案例精讲系列 2024 Python 版

## 系列之五：求斐波那契数列，学习迭代和递归

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

# 五、求斐波那契数列，学习迭代和递归

背景知识：

> 斐波那契数列是一个经典的数学序列，以数学家列昂纳多·斐波那契（`Leonardo Fibonacci`）的名字命名。这个序列的前两个数字是0和1，后续的每个数字都是前两个数字之和。换句话说，第三个数字是前两个数字的和，第四个数字是前两个数字之和，以此类推。
> 
> 斐波那契数列的前几个数字依次是 `0、1、1、2、3、5、8、13、21、34` 等等。这个序列在数学和计算机科学中具有广泛的应用。它的特点包括：
> 
> 1. 递归性质：斐波那契数列的定义本身就是递归的，每个数字都是前两个数字之和。这种递归性质也可以通过递归函数来实现。
> 
> 2. 快速增长：斐波那契数列的每个数字都比前一个数字大，增长速度非常快。随着序列的增长，相邻两个数字的比值趋近于黄金分割比例（约为1.618）。
> 
> 3. 自相似性：斐波那契数列具有自相似性，即序列的一部分可以看作是整个序列的缩小版。例如，去掉前两个数字后剩下的部分仍然是一个斐波那契数列。
> 
> 斐波那契数列在数学、编程、金融等领域都有广泛的应用，例如在算法设计、动态规划、金融建模、自然科学模型等方面。

#### 题目要求：

> 请用递推和递归方式编写一个 Python 函数，接收一个整数 `n` 作为参数，返回斐波那契数列的前 `n` 个数字。
> 
> - 用递推方式实现的函数名为 `fibonacci_iterative(n)`，返回一个包含斐波那契数列前 `n` 个数字的列表。
> 
> - 用递归方式实现的函数名为 `fibonacci_recursive(n)`，返回一个包含斐波那契数列前 `n` 个数字的列表。

#### 思路分析：

> - 斐波那契数列的前两个数字为 `0 和 1`，后续的每个数字都是`前两个数字之和`；
> 
> - 递推方式需要使用循环来计算斐波那契数列的每个数字；
> 
> - 递归方式需要使用函数自身来计算斐波那契数列的每个数字。

#### 编程练习：

> [求斐波那契数列 C 代码](https://github.com/coffeescholar/C_CPP-Learning/blob/main/%E7%AE%97%E6%B3%95%E5%85%A5%E9%97%A8%E7%BB%83%E4%B9%A0/05_%E6%B1%82%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97_%E7%BB%83%E4%B9%A0%E9%80%92%E6%8E%A8%E5%92%8C%E9%80%92%E5%BD%92.c)

请自行编程实现，分别用递推和递归方式实现的参考代码如下：

##### 1. 递推方式：

```python
# 用递推方式求斐波那契数列
def fibonacci_Iterative(n:int):
    if n <= 0:
        return "输入的数必须是正整数"
    elif n == 1:
        return [0]
    elif n == 2:
        return [0, 1]
    else:    # 从 3 开始采用递推，小于 3 直接返回结果
        fib_sequence = [0, 1]
        for _ in range(3, n+1):
            fib_next = fib_sequence[-1] + fib_sequence[-2]
            fib_sequence.append(fib_next)
        return fib_sequence
```

函数 `fibonacci_iterative(n)` 使用循环迭代的方式来计算斐波那契数列的前 `n` 个数。它从初始的前两个斐波那契数开始，通过迭代计算得到前 `n` 个斐波那契数，并将它们存储在一个列表中返回。

##### 2. 递归方式：

```python
# 用递归方式求斐波那契数列
def fibonacci_Recursive(n:int):
    if n <= 0:
        return "输入的数必须是正整数"
    elif n == 1:
        return [0]
    elif n == 2:
        return [0, 1]
    else:    # 从 3 开始采用递归，小于 3 终止递归，直接返回结果
        fib_sequence = fibonacci_Recursive(n-1)
        fib_sequence.append(fib_sequence[-1] + fib_sequence[-2])
        return fib_sequence
```

函数`fibonacci_Recursive(n)`使用递归的方式来计算斐波那契数列的前 `n` 个数。它通过将问题分解为两个子问题：计算前 n-1 个斐波那契数，并将结果存储在一个列表中，然后将最后两个数相加得到第 `n` 个斐波那契数，并将其添加到列表中返回。

请注意，递归函数中一定要设置终止递归的条件。本例中，当 n < 3 时，将不再 ”**自己调用自己**“ 从而终止继续递归。

可以通过调用这两个函数来计算斐波那契数列的前 `n` 个数。例如，计算斐波那契数列的前 `10` 个数，可以这样调用函数：

```python
n = 10
print(fibonacci_Iterative(n)) # 输出：[0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
print(fibonacci_Recursive(n)) # 输出：[0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

上面的例子中，可以用推导式简化列表部分，有兴趣的话请自行练习，就不展开了。

> 单词助手：
> 
> - `iterative 迭代的、循环的、递推的`
> 
> - `recursive 递归的、递归式的`

---

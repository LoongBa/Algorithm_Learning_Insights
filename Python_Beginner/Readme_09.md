# 小学生 算法入门 案例精讲系列 2024 Python 版

## 系列之九：求解八皇后问题，继续练习回溯

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

# 九、求解八皇后问题，继续练习回溯

背景知识

> 八皇后问题是一个经典的数学和计算机科学问题，旨在找到在一个8x8的棋盘上放置8个皇后，使得它们互相不能攻击到对方的情况下，所有皇后的位置组合。

> > 在国际象棋中，皇后是最强大的棋子，可以在横、竖和对角线上任意距离移动。因此，八皇后问题要求在8x8的棋盘上放置8个皇后，使得每个皇后都不在同一行、同一列和同一对角线上。
> 
> 由于皇后的特殊移动能力，这个问题本质上是一个组合优化问题。解决八皇后问题的一种常见方法是使用回溯算法。回溯算法通过尝试不同的解决方案，并进行适当的剪枝，直到找到所有满足条件的解决方案。

八皇后问题是一个经典的练习问题，它有助于提高问题解决和编程技巧。通过解决这个问题，可以加深对回溯算法和组合优化问题的理解。

#### 题目要求：

> 请用递推和递归方式编写一个函数，解决八皇后问题：
> 
> - 用递推方式实现的函数名为 `eight_queens_iterative()`，它应该返回一个包含所有可行解的列表。每个可行解都是一个列表，其中每个元素表示每行皇后所在的列号。
> 
> - 用递归方式实现的函数名为 `eight_queens_recursive()`，它应该返回一个包含所有可行解的列表。每个可行解都是一个列表，其中每个元素表示每行皇后所在的列号。

#### 思路分析：

> - 要确保每个皇后在同一行、同一列和同一对角线上都没有其他皇后；
> 
> - 递推方式可以使用循环来尝试不同的列号，逐行放置皇后；
> 
> - 递归方式可以使用递归函数来尝试不同的列号，逐行放置皇后。

#### 编程练习：

当解决八皇后问题时，递推方式和递归方式的实现略有不同。

> [求解八皇后问题 C 代码](https://github.com/coffeescholar/C_CPP-Learning/blob/main/%E7%AE%97%E6%B3%95%E5%85%A5%E9%97%A8%E7%BB%83%E4%B9%A0/09_%E6%B1%82%E8%A7%A3%E5%85%AB%E7%9A%87%E5%90%8E%E9%97%AE%E9%A2%98_%E7%BB%A7%E7%BB%AD%E7%BB%83%E4%B9%A0%E5%9B%9E%E6%BA%AF.c)

下面是递推和递归方式的解答和调用示例代码，请自行编程实现再参考：

> 单词助手：
> 
> - `stack 栈`——一种基础的数据结构，类似列表
> 
> - `solution 解决方案、解答`

##### 1. 递推方式：

```python
def eight_Queens_Iterative():
    solutions = []
    stack = [(0, [])]  # 使用栈来存储每一行的状态，每个元素为 (row, queens)，其中 row 表示当前行数，queens 表示已放置皇后的列号列表

    while stack:
        row, queens = stack.pop()

        if row == 8:  # 找到一个解
            solutions.append(queens)
        else:
            for col in range(8):
                if all(col != q and abs(row - i) != abs(col - q) for i, q in enumerate(queens)):
                    stack.append((row + 1, queens + [col]))

    return solutions

solutions = eight_queens_iterative()
for solution in solutions:
    print(solution)
```

##### 2. 递归方式：

```python
def eight_Queens_Recursive(row=0, queens=[]):
    if row == 8:
        return [queens]

    solutions = []
    for col in range(8):
        if all(col != q and abs(row - i) != abs(col - q) for i, q in enumerate(queens)):
            solutions.extend(eight_Queens_Recursive(row + 1, queens + [col]))

    return solutions

solutions = eight_Queens_Recursive()
for solution in solutions:
    print(solution)
```

调用函数的示例代码：

```python
# 调用递推方式的八皇后问题解答函数
solutions_Iterative = eight_Queens_Iterative()
print("递推方式解答八皇后问题:")
for solution in solutions_Iterative:
    print(solution)

# 调用递归方式的八皇后问题解答函数
solutions_Recursive = eight_Queens_Recursive()
print("递归方式解答八皇后问题:")
for solution in solutions_Recursive:
    print(solution)
```

注意：八皇后问题的解决方案可能有多个，每个解决方案都是一个列表，其中每个元素表示每行皇后所在的列号。因此，可能会有多行输出。

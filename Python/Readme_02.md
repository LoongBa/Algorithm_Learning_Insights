# 小学生 算法入门 案例精讲系列 2024 Python 版

## 系列之二：求水仙花数，了解枚举和迭代

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

# 二、求水仙花数，了解枚举和迭代

## 背景知识：

> `水仙花数`指的是一个 `n 位数`，它的每个位上的数字的 `n 次幂之和`等于它本身。例如，`153` 是一个`水仙花数`，因为 1^3 + 5^3 + 3^3 = 153 。

> `水仙花数` 又称为 `阿姆斯特朗数` `Armstrong Number` 得名于美国数学家`迈克尔·D·阿姆斯特朗` `Michael D. Armstrong` 。他在1969年的一篇论文中提到了这个概念。
> 
> 虽然 `水仙花数` 以 `迈克尔·D·阿姆斯特朗` 的名字命名，但他并不是首个研究这个概念的人。早在1917年，印度数学家 `斯里尼瓦瑟·拉马努金` `Srinivasa Ramanujan` 就提到了类似的数学问题。

## 题目要求：

> - 编写一个函数 `isArmstrongNumber(number:int)`，判断传入的参数 `number` 是否是水仙花数。如果是，返回 `True`，否则返回 `False`；
> 
> - 调用这个函数，判断 `10000` 以内的水仙花数并输出。

> [求水仙花数 C 代码](https://github.com/coffeescholar/C_CPP-Learning/blob/main/%E7%AE%97%E6%B3%95%E5%85%A5%E9%97%A8%E7%BB%83%E4%B9%A0/03_%E6%B1%82%E6%B0%B4%E4%BB%99%E8%8A%B1%E6%95%B0_%E4%BA%86%E8%A7%A3%E6%9E%9A%E4%B8%BE%E5%92%8C%E8%BF%AD%E4%BB%A3.c)

## 思路分析：

很显然，又需要拆分数字了：

- 拆分数字的每一位；

- 将每一位的三次方求和；

- 将和与这个数本身进行比较;

- 注意范围：题目要求 `10000` 以内，结合水仙花数的定义，可以简单剪枝。

有了上一次`判断回文数`的经验，拆分数字有很多种方法。

这一次的练习，重点在复习和巩固的基础上，学习和练习 Python 特有的`推导式`，理解和掌握`迭代/可枚举类型`。

> 注意：部分编程语言有类似的方式实现类似推导式的功能，但 Python 将之内置在 “语言” 级别提供，而不需要依赖外部函数等。
> 
> 所以，在享受 `Python 语法糖` 之余，一定要掌握 `通用方法`。

## 编程练习：注意对比以下各版本的差异

请先自行实现判断一个数字是否是水仙花数的函数，
再对照看下面的代码如何演进。

1. **版本 1.0：** 通用解法

```python
# 判断一个数字是否是水仙花数，这里默认按每位上的数字的三次方计算
def is_Armstrong_Number1(number:int, power:int = 3):
    # 将整数值的 number 转为字符串 digits
    digits = str(number)
    result = 0    # 这一句可以省略：Python 中不需要定义变量和赋予初始值
    for i in range(len(digits)):       # 循环，用 number 的长度作为循环次数
        item = int(digits[i])**power   # 计算每一位的 power 次方
        result += item                # 累加

    return result == number    # 是否是水仙花数   # 累加
```

2. **版本 2：** 基于索引的取值方式改为对集合元素的直接访问
   
   将 `循环获取每一位数字字符并求 power 次幂后进行累加` 这部分改为

```python
for digit in digits:           # 迭代 number 的每一位
    item = int(digit)**power   # 计算每一位的 p
```

### 关于迭代和可枚举类型

> 迭代允许我们对一个数据集合中的每个元素执行相同的操作，或者按照一定的规则重复执行某段代码。迭代是一种在编程中常见且重要的概念，它可以帮助我们处理大量的数据、执行重复的任务或实现算法的逻辑。比如：
> 
> `循环访问数据集的每一项元素` 又称为 `遍历数据集`；
> 
> `遍历某个数据集并进行特定的处理`，这个过程叫做 `迭代` ；

迭代处理数据集中每一个元素的方法，常见有两类：

- 用 `for i in range(n)` 循环，和 `item = items[i]` 用索引访问每一项；

- 用 `for item in items` 的方式遍历数据集 `items`，而不必用数值索引去访问数据集 `items` 的每一项：
  
  - `item` 已经是数据集的每一项，不必再用 `items[i]` 访问；
  
  - 数据集 `items` 属于 `可枚举类型` 才能用这样的方法；
  
  - Python 中的 `列表、元组、字典` 是 `可枚举类型`；
  
  - 注意：**部分语言不支持对可枚举类型的 for in range 方式迭代，所以还是需要掌握通用方法**。

```python
# 判断一个数字是否是水仙花数，这里默认按每位上的数字的三次方计算
def is_Armstrong_Number2(number:int, power:int = 3):
    # 将整数值的 number 转为字符串 digits
    digits = str(number)

    result = 0    # 这一句可以省略：Python 中不需要定义变量和赋予初始值
    for digit in digits:           # 迭代 number 的每一位
        item = int(digit)**power   # 计算每一位的 power 次方
        result += item            # 累加

    return result == number    # 是否是水仙花数
```

3. **版本 3：** Python 推导式
   
   用 Python 推导式，将 `digits` 字符串中的每一位转换成数值再求 `power` 次幂。

```python
# 判断一个数字是否是水仙花数，这里默认按每位上的数字的三次方计算
def is_Armstrong_Number3(number:int, power:int = 3):
    # 将整数值的 number 转为字符串 digits
    digits = str(number)
    # 用推导式生成一个列表，列表中的每个元素是 number 的每一位的 power 次方
    list = [int(digit)**power for digit in digits]
    # digit 是式子中的临时变量

    result = 0    # 这一句可以省略：Python 中不需要定义变量和赋予初始值
    for item in list:           # 迭代列表中的每一个元素，对应 number 的每一位的 power 次方
        result += item         # 累加

    return result == number    # 是否是水仙花数
```

4. **版本4：** 将迭代列表并累加求和部分，改为 Python 内置函数 `sum()`
   
   注意：`sum()` 函数可以对 `列表、元组、字典` 进行求和。
   ——注意观察：它们是 `可枚举类型`，所以，... ...，请多想一想。

```python
# 判断一个数字是否是水仙花数，这里默认按每位上的数字的三次方计算
def is_Armstrong_Number4(number:int, power:int = 3):
    digits = str(number)
    list = [int(digit)**power for digit in digits] #推导式， digit 是式子中的临时变量
    result = sum(list)         # 用 Python 内置的 sum 函数计算列表中所有元素的和

    return result == number    # 是否是水仙花数素的和
```

5. **版本5：** 基于 `Python 语法糖` 的**极简 “优化”**

```python
# 判断一个数字是否是水仙花数：极简版本
def is_Armstrong_Number5(number:int, power:int = 3):
    return number == sum(int(digit)**power for digit in str(number))
```

**特别注意：版本5 中的“极简”版本函数，在实际软件开发中并不提倡**，主要原因如下：

- 不利于 “阅读” 代码，尤其    团队开发往往需要交叉评审，时间长了甚至自己也未必记得；

- 不利于 调试，比如加断点——不是不能加，是不便加；

- 不利于维护，因为后续维护代码的人未必是你，谁都害怕遇到 “屎山代码”。

所以，面对这类技巧——掌握它，可以用，但不要滥用，不要给自己和别人留下麻烦。

如果有人用来 “炫技”，记住：`不与夏虫语冰`，呵呵一笑而过。

参考上一节 《求回文数》中学习到的 `用数学方法拆分每一位上的数字` 的方法，重新实现求水仙花数的代码，请自行尝试，参考代码如下：

```python
def is_Armstrong_Number(number, power:int = 3):
    n = len(str(number))
    result = 0
    temp = number
    while temp > 0:
        digit = temp % 10        # 求末位上的数字
        result += digit ** power # 累加到结果变量
        temp //= 10              # 缩小十倍，以便求下一位
    return result == number
```

## 扩展练习：

> 请仿照 `sum()` 自行编写一个函数 `summation()`，用来对 `列表、元组、字典` 求和。记住：Python 中的 `列表、元组、字典` 是 `可枚举类型`。
> 
> 再注意一下，`对 字典 求和`，与 `对 列表、元组 求和` 有什么不同之处？

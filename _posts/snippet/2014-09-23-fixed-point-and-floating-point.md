---
layout: post
title: 定点数和浮点数
category: 摘录
tags: snippet
description: 
---

在计算机存储器中，整数和分数之间的转换并不是这么随意。现在我们应该清楚，计算机中的一切数据都是以位的形式存储的，这就意味着所有的数都表示为二进制形式。但另一个不可否认的事实是，某些类型的数比其他类型更容易用位的形式来表示。

### 整数

我们将从整数的二进制表示开始，这里的整数被数学家称作“自然数”（positive whole number），即计算机程序员口中的“正整数”（positive integers），之后将介绍如何利用2的补数来表示“负整数”（negative integers），该方法可以让正数和负数的相加变得非常简单。下面的表格列出了8位，16位，32位二进制数所能表示的正整数及其2的补数的范围。

| 数的位数 | 正整数的范围    | 整数的2的补数范围            |
| -------- | -----------     | ----------------             |
| 8        | 0~255           | -128~127                     |
| 16       | 0~65 535        | -32 768~32 767               |
| 32       | 0~4 294 967 295 | -2 147 483 648~2 147 483 647 |

我们所要介绍的整数部分就是这样。

### 有理数

除此之外，数学家还定义了用两个整数的比值表示的一类数，称作有理数（rational number）或分数（fraction）。例如3/4是一个有理数，因为它是整数3和4的比。我们也可以把3/4表示成十进制小数的形式，即0.75.尽管我们可以把它写成十进制书的形式，但它实际上代表一个分数，即75/100.

如第7章所述，在十进制数字系统中，小数点左边的数的每一位都和10的正整数次幂相关，而其右边的数的每一位都和10的负整数次幂相关。我们在第7章用到了42705.684这个实例，现在，我们把它表示为以下等价形式：

```
4 x 10000 +
2 x 1000 +
7 x 100 +
0 x 10 +
5 x 1 +
6 / 10 + 
8 / 100 +
4 / 1000
```
上面的除号表示了该位置的数与10的负整数次幂相关的情况，用下面的表达方式可以用除号：

```
4 x 10000 +
2 x 1000 +
7 x 100 +
0 x 10 +
5 x 1 +
6 x 0.1 + 
8 x 0.01 +
4 x 0.0010
```
最后，我们将该数表示为10的幂的形式：

```
4 x 10^4 +
2 x 10^3 +
7 x 10^2 +
0 x 10^1 +
5 x 10^0 +
6 x 10^-1 + 
8 x 10^-2 +
4 x 10^-3
```
有一些有理数很难表示成小数，最明显的一个例子是1/3，如果用3来除1，会得到这样的结果：

```
0.33333333333333...
```
尽管如此，把1/3表示为小数还不是很方便，但它毕竟是一个有理数，因为在本质上它是两个整数的比。类似的，1/7可以表示为：

```
0.142857142857142857......
```

### 无理数

无理数（irrational number）是一些更加奇特的数，如2的平方根等。它们不能表示为两个整数的比，这就意味着其小数部分是无穷的，而切毫无规律，没有循环，例如：

```
√2 = 1.414213562373095...
```
下面这个数学方程式的正数解就是2的平方根：

```
x*x - 2 = 0
```
如果某个数不是任何以整数为系数的代数方程的解，那么这个数称作超越数（transcendental，所有的超越数都是无理数，但是反之不成立）。π就是一个典型的超越数，它是周长与其直径的比值，可以近似的表示为：

```
3.14159265359...
```

### 虚数

目前我们所讨论过的所有数——有理数和无理数——统称为实数（real numbers）。使用实数定义它们的目的是为了将其与虚数（imaginary numbers）区别开来，虚数是负数的平方根。实数和虚数一起构成了复数（complex numbers）。不管名称如何，它们都有重要的作用，例如，虚数确实存在于现实世界，它在解决电子学的某些高级问题中有重要应用。

### 二进制表示小数

小数也可以表示为二进制数吗？当然可以，最简单的方法可能就是使用BCD码（二进制编码的十进制数）。如第19章所述，BCD码是将十进制数以二进制的形式进行编码，0～9之间的每一个数都需要用4位来表示，如下表所示。

| 十进制数字 | BCD代码  |
| ---------- | -------- |
| 0          | 0000     |
| 1          | 0001     |
| 2          | 0010     |
| 3          | 0011     |
| 4          | 0100     |
| 5          | 0101     |
| 6          | 0110     |
| 7          | 0111     |
| 8          | 1000     |
| 9          | 1001     |

BCD编码在程序处理用美元和美分表示的钱款，账户时特别有用。银行和保险公司时非常典型的两类整日与钱打交道的机构，这些机构所使用的计算机程序中，大多数小数所占用的存储空间仅仅相当于两个十进制数所占用的位数。

通常把两个BCD数字放在一个字节，这种方式称为压缩BCD（packed BCD）。由于2的补数不和BCD数一起使用，因此压缩BCD通常需要增加1位用来标识数的正负，该位被称作符号位（sign bit）。用一整个字节保存某个特定的BCD数是很方便的，但要为这个短小的符号位牺牲4位或8位的存储空间。

让我们来看一个例子，假设计算机程序所要处理的钱款数目在+/-100万美元之间，这就意味着，需要表示的钱的数目的范围是-9 999 999.99~99 999 999.99,因此保存在存储器中的每一笔钱的金额都需要5个字节。因此，-4 325 120.25 可以表示为下面5个字节：

```
00010100 00110010 01010001 00100000 00100101
```
将每个字节转换成十六进制数，上面的数可以等价地表示成：

```
14h 32h 51h 20h 25h
```
> 注意，最左边的半个字节所构成的1用来指明该数是负数，这个1即符号位。如果这半个字节所构成的数是0，则说明该数是正数。组成该数的每一个数字都需要用4位来表示，从十六进制的表示形式中可以很直观地看到这一点。

如果要表示的数的范围扩大到－99 999 999.99～99 999 999.99，则我们需要用6个字节来实现，其中5个字节用来表示10个数字，另一个字节整个用来做符号位。

### 定点格式

这种基于二进制的存储和标记方式也别称作定点格式（fixed-point format), 所谓的“定点”是指小数点的位置总是在数的某个特定位置——在本例中，它位于两位小数之前。值得注意的是，有关小数点位置的计数信息并没有与整个数字一起存储。所以，使用定点小数的程序必须知道小数点的位置。你可以设计有任意小数位的定点小数，并且可以在程序中混合使用它们，但程序中对这些数进行算数运算的部分都需要知道小数点的位置，这样才能正确地对其做各种运算处理。

### 浮点数

#### 科学计数法

如果可以确定程序用到的数字不会大到超过预定的存储空间，并且这些数的小数位不会很多，那么使用定点格式的小数将是一个很好的选择。在表示非常大或非常小的数时，使用定点格式数时绝对不合适的。假设需要保留一块内存空间用来存放以英尺为单位的距离数据，可能存在的问题是某些距离的长度可能超出范围。地球与太阳之间的距离是490 000 000 000英尺，而氢原子的半径只有0.000 000 000 26英尺，如果采用定点格式的存储方案，为了存储这些极大或极小的数需要12个字节。

科学家和工程师们喜欢使用一种称为“科学计数法”（scientific notation）的方法来记录这类较大或较小的数，利用这种计数系统可以更好地在计算机中存储这些数。科学计数法把每个数表示成有效位与10的幂的乘积的形式，这样就可以避免写一长串的0，因此这种计数方式特别适合表示极大或极小的数。采用科学计数法，下面这个数：

````
490 000 000 000
```
可以记为

```
4.9 x 10^11
```
而

```
0.000 000 000 26
```
可以表示为：

```
2.6 x 10^-10
```
在上面的两个例子中，4.9和2.6被称作小数部分或者首数（characteristic），有时候也被称作为尾数（mantissa，这个词通常与对数运算一起使用）。在计算机术语中这一部分被称作有效数（significand），因此为了保持一致，这里把科学计数法表示形式中的这一部分也称作有效数。

采用科学计数法表示的数可以分为两部分，其中指数（exponent）部分用来表示10的几次幂。在第一个例子中，指数是11，第二个例子中指数是－10.指数可以表明小数点相对于有效数移动的距离。

为了便于操作，一般规定有效数的取值范围是大于或等于1而小于10.尽管下面列出的各种写法表示的都是同一个数：

```
4.9 x 10^11 = 49 x 10^10 = 490 x 10^9 = 0.49 x 10^12 + 0.49 x 10^13
```
但是上面等式中的第一种写法是最恰当的。这种写法有时候被称作科学计数法的规范式（normalized）。

这里需要说明，指数的正负性只是表明了数的大小，它并不能指明数本身的正负性。下面列出两个负数的科学计数法表示形式：

```
-5.8125 x 10^7
```
与－58125 000相等。而

```
-5.8125 x 10^-7
```
则与

```
-0.000 000 058 125
```
相等。

在计算机中，对于小数的存储方式，除了定点格式外还有另外一种选择，它被称作浮点格式（floating－point notation）。因为浮点格式是基于科学计数法的，所以它是存储极大或极小值的理想方式。但计算机中的浮点格式是借助二进制数实现的科学计数法形式，因此我们首先要了解如何用二进制表示小数。

#### 二进制表示小数

实际操作比预想的要简单。在十进制数中，小数点右边的数字与10的负整数次幂相关联；而在二进制数中，二进制小数点（就是一个简单的句点，看起来同十进制小数点一样）右边的数字和2的负整数次幂相关。例如，下面的这个二进制数：

```
101.1101
```
可以用如下方式转换为十进制数：

```
1 x 2^2 +
0 x 2^1 +
1 x 2^0 +
1 x 2^-1 +
1 x 2^-2 +
0 x 2^-3 +
1 x 2^-4
```
经过这种计算，101.1101与十进制数5.8125是相等的。

在十进的科学计数法中，规范化式的有效数应该大于或等于1且小于10；类似的，在二进制数的科学计数法中，规范化式的有效数应该大于或等于1且小于10（即十进制的2）。因此，在二进制的科学计数法中，下面这个数字：

```
101.1101
```
其规范化式应该是：

```
1.011101 x 2^2
```
> 这个规则暗示了这样一个有趣的现象：在规范化二进制浮点数中，小数点的左边通常只有一个1，除此之外没有其他数字。

#### IEEE二进制浮点数算术运算标准

当代大部分计算机和计算机程序在处理浮点数时所遵循的标准是IEEE（Institute of Electrical and Electronics Engineers，美国电气和电子工程师协会）于1985年制定的，ANSI（American National Standards Institute，美国国家标准局）也认可该标准。ANSI/IEEE Std 754-1985 称作IEEE 二进制浮点数算数运算标准（IEEE Standard for Binary Floating-Point Arithmetic)——它只有18页——相对于其他标准来说是非常简单了，但却奠定了以简便方式编码二进制浮点数的基石。

IEEE浮点数标准定义了两种基本的格式：以4个字节表示的单精度格式和以8字节表示的双精度格式。

让我们首先来了解一下单精度格式。它的4个字节可以分为三个部分：1位的符号位（0代表正数，1代表负数），8位用作指数，最后的23位用作有效数。下表给出了但进度格式的三部分的划分方式，其中有效数的最低位在最右边。

![](https://github.com/arcticlion/reading-lists/blob/master/Code/Chapter%2023%20Fixed%20Point%20and%20Floating%20Point/屏幕截图%202014-10-20%2022.54.07.png)


三部分共32位，也就是4个字节。我们刚才提到过，对于二进制科学计数法的规范化式，其有效数的小数点左边有且仅有一个1，因此在IEEE浮点数标准中，这一位没有分配存储空间。在该标准中，仅存储有效数的23位小数部分，尽管存储的只有23位，但仍然称其精度为24位。我们将在下面的内容里体会24位精度的含义。

8位指数部分的取值范围是0～255，称为偏移（biased）指数，它的意思是：对于有符号指数，为了确定其实际所代表的值必须从指数中减去一个值——称作偏移量（bias）。对于单精度浮点数，其偏移量为127.

指数0和255用于特殊的目的，稍后将简单介绍。如果指数的取值范围是1～254，那么对于一个特定的数，可以用s（符号位），e（指数）以及f（有效数）来表述它：

```
(-1)^s x 1.f x 2^e-127
```
-1的s次幂是数学上所采用的一种巧妙的方法，它的含义是：如果s＝0，则该数是正的（因为任何数的0次幂都是1）；如果s＝1，则该数是负的（因为－1的1次幂等于－1）。

表达式的中间部分是1.f，其含义是：1的后面是小数点，小数点后面跟着23位的有效数。1.f与2的幂相乘，其中指数等于内存中的8位的偏移指数减去127.

> 注意，目前为止我们还没有学习如何表达那个经常遇到却又总被遗忘的一个数字：那就是“0”。

这是一种特殊的情况，下面我们对其进行说明。

- 如果e＝0且f＝0，则该数为0.在这种情况下，通常把32位都设置为0以表示该数为0.但是符号位可以设置为1，这种数可以解释为负0.负0可以用来表示非常小的数，这些数极小以至于不能在单精度格式下用数字和指数来表示，但它们仍然小于0.

- 如果e＝0且f≠0，则该数是合法的，但不是规范化的。这类数可以表示为：

  (-1)^s x 0.f x 2^-127

  注意，在有效数中，小数点的左边是0.

- 如果e＝255且f＝0，则该数被解释为无穷大或无穷小，这取决于符号位s的值。

- 如果e＝255且f≠0，则该值被解释为“不是一个数”，通常缩写为NaN（not a number）。NaN用来表示未知的数或非法操作的结果。

单精度浮点格式下，可以表示的规格化的最小，正，负二进制数是：

```
1.00000000000000000000000(2) x 2^-126
```
小数点后面跟着23个二进制0。单精度浮点格式下，可以表示的规格化的最大正，负二进制数是：

```
1.11111111111111111111111(2) x 2^127
```
在十进制下，这两个数近似地等于1.175494351 x 10^-38和3.402823466 x 10^38，这也就是单精度浮点数的有效表示范围。

#### 浮点数精度问题

如前所述，10位二进制数可以近似地用3位十进制数来表示。其含义是，如果把10位都置为1，即十六进制的3FFh或十进制的1023，它近似等于把十进制数的3位都置为9，即999，可以表示为下面的约等式：

```
2^10 ≈ 10^3
```
两者之间的这种关系意味着：单精度浮点数格式存放的24位二进制数大体上与7位的十进制数相等。
如前所述，10位二进制数可以近似地用3位十进制数来表示。其含义是，如果把10位都置为1，即十六进制的3FFh或十进制的1023，它近似等于把十进制数的3位都置为9，即999，可以表示为下面的约等式：

```
2^10 ≈ 10^3
```
两者之间的这种关系意味着：单精度浮点数格式存放的24位二进制数大体上与7位的十进制数相等。其深层的含义是什么呢？

当我们查看定点数时，其精确度是很明显的。例如，当我们表示钱款时，采用两位定点小数就可以精确到美分。但是对于采用浮点数格式的数，就不能如此肯定了。其精确度依赖于指数的值，有时候浮点数可以精确到比美分还小的单位，但有时候其精确度甚至达不到美元。

这样说可能更合适：单精度浮点数的精度为1/(2^24), 或1/16777216， 或百万分之六，但其真正的含义是什么呢？

首先这意味着在单精度浮点格式下，16 777 216和16 777 217将表示成同一个数。不仅如此，处于这两个数之间的所有的数（例如，16 777 216.5）也将被表示成同一个数。所以上面提到的3个十进制数都按32位单精度浮点数：

```
4B800000h
```
来存放。将该数按符号位，指数位和有效数位划分，可以表示为：

```
0 10010111 00000000000000000000000
```
也就是：

```
1.00000000000000000000000(2) x 2^24
```
下一个二进制浮点数可表示的最大有效数是16 777 218，即：

```
1,00000000000000000000001(2) x 2^24
```
以同一个浮点数来表示两个不同的十进制数，有时可能称为一个问题，也可能不会。

但如果你为银行编写程序，用单精度浮点数来存放以美元，美分为单位的数字时，就会发现262144.00美元和262144.01美元在计算机中存储为同一个数：

```
1.00000000000000000000000(2) x 2^18
```
这也是为什么人么在处理以美元，美分表示的钱款数目时更愿意使用定点数的一个原因。当使用了浮点数时，你会发现它还存在着一些让人崩溃的小问题。你的程序进行了一系列计算，应该得到的结果为3.50的，但由于使用了浮点数，你得到的可能是3.499999999999。这种问题在浮点数运算中经常发生，而且没有一套完整的解决方案。

#### 双精度浮点数

如果相在程序中使用浮点格式数，但使用单精度格式又会出现各种问题，这时你可能以考虑使用双精度浮点数（double-precision floating-point format).这种类型的数需要用8个字节来表示，它的结构如下表所示。

![](https://github.com/arcticlion/reading-lists/blob/master/Code/Chapter%2023%20Fixed%20Point%20and%20Floating%20Point/屏幕截图%202014-10-21%2013.01.19.png)

双精度浮点数的指数偏移量是1023，或十六进制的3FFh，因此以该格式存储的数可以表示为：

![](https://github.com/arcticlion/reading-lists/blob/master/Code/Chapter%2023%20Fixed%20Point%20and%20Floating%20Point/屏幕截图%202014-10-21%2013.01.24.png)


上面提到的关于单精度浮点格式下的0，无穷大（小）和NaN的判断规则同样适用于双精度浮点格式。

双精度浮点格式下可以表示的最小正数或负数为：

```
1.0000000000000000000000000000000000000000000000000000(2) × 2^−1022
```
注意，小数点的后面共有52个0.同样的，可以表示的最大数为：

```
1.1111111111111111111111111111111111111111111111111111(2) × 2^1023
```
其所能表示的范围，用十进制可以近似记为：

```
2.2250738585072014 × 10^–308~1.7976931348623158 × 10^308
```
10的308次幂是一个非常巨大的数，在1的后面跟着308个0.

双精度浮点格式的有效数有53位（包括前面没有列出的那一位），大致相当于十进制的16位。与单精度浮点格式相比，这已经有了很大的改进了，但仍然不能避免两个不同的数存储为同一个结果的情况。例如，140,737,488,355,328.00和140,737,488,355,328.01在内存中存放时，会被当作同一个数来处理，它们的双精度浮点格式表示为：

```
42E0000000000000h
```
即：

```
1.0000000000000000000000000000000000000000000000000000(2) × 2^47
```

#### 浮点数运算

当然，为浮点数发明一种在内存中的存储方式，这只是在汇编程序使用浮点数所涉及的工作的一小部分。如果你决定闭门造车，完全独立地开发一台计算机，则必须要独立编写用于浮点数加，减，乘，除运算的函数集。幸运的是，有了前面关于正数四则运算的学习，这些关于浮点数的运算就可以分解成许多小的关于整数的加，减，乘，除运算，这样就能将问题大大简化。

例如，浮点数加法中最重要一点的就是如何对有效数相加，为了能使它们的有效位匹配，需要利用指数来确定对其如何移位。假设要进行下面的加法运算：

```
(1.1101 × 2^5) + (1.0010 × 2^2)
```
你需要把有效数部分的11101和10010相加，但并不是简单地直接相加。两个数的指数部分的不同决定了第二个数必须相对于第一个数右移。实际上，我们要做的整数加法应该是11101000加10010.最后的运算结果是：

```
1.1111010 × 2^5
```
前面我们曾列出过太阳与地球的距离以及氢原子的半径，如果把这两个数相加会是怎样的结果呢？显而易见，因为它们两者的指数相差太大，因此较小的数对结果甚至没有影响。

两个浮点数的乘法意味着要把有效数当作整数相乘，并且把指数部分相加。为了使结果规范化，一般需要对指数调整一到两次。

浮点数运算另一层次的复杂性体现在处理一些较为繁杂的函数运算，例如平方根，指数，对数和三角函数。但所有的这些运算都可以通过加，减，乘，除这四种基本的浮点数运算来实现。

例如，三角函数中的sin函数可以通过下面的一系列展开式近似计算：

```
sin(x) = x - x^3/3! + x^5/5! + x^7/7! + ...
```
参数x的值必须是弧度，360°对应的弧度范围是2 π。上式中的感叹号表示阶乘运算符，ta的意义是把1到该数之间的所有整数相乘，例如5!=1x2x3x4x5.这只是简单的乘法运算。其余的部分也只是简单的除法，加法或减法运算，这些都是容易实现的。上面的算式中，唯一让人感到棘手的地方是最后的省略部分，这意味着计算会一直继续下去。然而事情并没有想象中那么糟糕，在实际运算中，如果把弧度的取值限制在0～ π／2的范围内（从这个范围就可以推导出所有的正弦值），你更不不需要进行多少运算，因为大约展开12项后，就可以使结果精确到双精度浮点数要求的53位。

当然，使用计算机的目的就是帮助人们更加方便地解决问题，而编写程序来进行浮点数运算这一繁杂工作似乎和这个目的背道而驰。但这正是软件的优势所在：一旦某个人为特定的计算机彼岸写了浮点数运算的程序，那么其他的人都可以使用它。浮点数运算在科学和工程类程序中极为重要，因此常常被赋予很高的优先级。在计算机发展的早起，为新制造的计算机做的第一项工作就是为其编写浮点数运算程序。

实际上，甚至可以直接利用计算机机器码指令来实现浮点数的运算。当然，实际做起来要比“动动嘴皮子”困难得多，但这也从另一个方面说明了浮点数运算得重要性。如果可以在硬件上实现浮点数算术运算——类似在16位微处理器上进行乘法和除法运算——则该机器上的所有的浮点数运算都会变得更快。

### 浮点数运算硬件

最早把浮点运算硬件作为选件的商用计算机是1954年的IBM704，704把所有的数按36位来存储。对浮点数，分成27位的有效数、8位指数和1个符号位。浮点运算硬件可做加法、减法、乘法和除法，其他浮点运算功能必须用软件来实现。

从1980年开始，浮点数运算硬件开始应用于桌面计算机，这起始于英特尔当年发布的8087数字协同处理（Numeric Data Coprocessor）芯片，当时这种集成电路被称作数学协同处理器（math coprocessor）或浮点数运算单元（floating-point，FPU）。8087不能独立工作，它只能与8086或8088（Intel的首个16位微处理器）芯片一起工作，因此被称作协处理器。

8087有40个引脚，使用许多与8086和8088相同的信号。微处理器和数学协处理器通过这些信号连接起来。当CPU收到一个特殊指令-—称为`ESC`(Escape)-—则协处理器接管系统控制权并执行下一条机器代码，即包括三角运算、指数、对数运算的68条指令中的一条。数据类型以IEEE标准为基础。那时，8087被认为是所生产的最高级的集成电路。

可以认为协处理器是一个小的自包含的计算机。在响应某个浮点运算机器码指令时（例如，计算平方根的FSQRT指令），协处理器内部执行存放在ROM中的自己的指令序列，这些内部指令称为微代码。这些指令通常是循环的，所以计算结果并不是马上可用。尽管如此，一般来说，数学协处理器至少比用软件来实现的同样例程要快10倍。

初始的IBMPC主板在8088芯片的右边有一个40管脚的插槽供8087用。遗憾的是，这个插槽是空的，需要加速浮点运算的用户必须单独购买8087并自己把它安装上。即使在安装了数学协处理器后，并不是所有的应用程序都可以运行得更快，一些应用程序—如，文字处理程序—几乎不需要浮点运算。其他如电子报表程序则要用到很多浮点计算。这些程序能够运行得更快，但并不是所有程序都是如此。

可以看到，程序员必须用协处理器机器码指令来编写特定的代码供协处理器执行。因为数学协处理器不是硬件的标准部分，因而许多程序员怕麻烦不愿意做。但是，他们还是不得不编写自己的浮点运算子程序（因为许多人并没有安装数学协处理器），所以支持8087芯片就成为一个额外的负担—一个不小的负担。最终，如果他们程序运行的机器上有数学协处理器，程序员要学会编写利用数学协处理器的应用程序；如果没有，则要编写浮点运算仿真程序。

经过几年后，Intel还发布了用于286芯片的287数学协处理器，用于386的387数学协处理器。但对于1989年发布的Intel 486DX，FPU已经做在了CPU里面，而不再是作为一个选件！遗憾的是，1991年Intel发布了一种低价格的486SX，它没有把FPU做在CPU里面，而是提供了487SX数学协处理器作为一个选件。1993年发布的Pentium芯片却再一次使做在CPU内部的FPU成为标准，也许以后永远会这样。Motorola在它的68040微处理器里集成了FPU，该微处理器于1990年发布。以前，Motorola销售68881和68882数学协处理器用来支持早先68000家族的微处理器。PowerPC芯片也把浮点运算硬件集成在内部。

尽管浮点运算硬件对专门从事汇编语言程序设计的程序员来说是一个很好的礼物，但是，与20世纪50年代早期开始的其他一些工作相比这只是微不足道的进步。我们的下一个主题是：计算机语言。


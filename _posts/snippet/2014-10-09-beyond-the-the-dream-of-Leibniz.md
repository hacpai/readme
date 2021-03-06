---
layout: post
title: 超越莱布尼茨之梦
category: 摘录
tags: snippet
description: 
---

图灵在伦敦数学会的演讲中说：

我希望数学计算机能够最终激起人们对符号逻辑的极大兴趣……人与这些机器进行交流的语言……构成了一种符号逻辑。

图灵所暗示的逻辑和计算之间的关联是本书的一个基本主题。然而，读者们也许仍然会问：逻辑和计算之间是如何彼此关联的？算术与推理有什么样的关系？

动词“估计”（reckon）的通俗用法为我们提供了一条线索，在这里它没有了通常的含义：“计算。”

“估计”一词的用法暗示了推理和计算之间真正而深刻的关联。用数进行估计本身就是一种推理形式，人们所作的大量推理都可以被看成一种计算。

把逻辑推理简化为形式规则的努力可以追溯到亚里士多德。他的工作是莱布尼茨关于一种普遍的计算语言的梦想的根本基础。图灵说明了所有的计算都能够在他的通用机上完成，这一成就也是亚里士多德的工作作为支撑的。计算和逻辑推理确实是同一个硬币的两面，利用这一洞见，我们不仅可以为计算机编程，从而使其能够完成各种任务，而且还能设计研制它们。

在过去的25年里，逻辑和计算机科学之间发生了广泛而持续的相互作用，而且仍在不断加强。在许多方面，逻辑为计算机科学提供了一种统一的基础框架和建立模型的工具……这次讨论会通过展示逻辑在其中扮演者至关重要的角色的一些计算机科学领域，如人工智能，计算复杂性，分布式计算，数据库系统和设计验证等等，从而为逻辑在计算机科学汇总的惊人效力进行一次全面考察。

### 计算机，大脑和心灵

1965年，麻省理工学院的计算机科学家约瑟夫编写了一个名为ELIZA的程序。ELIZA有意以一种相当粗糙的方式去模仿一个启动式的精神治疗师。以下是我和ELIZA之间的一次真实的对话：

```
ELIZA: 你好。请告诉我你的问题。
马丁：我的问题很难描述。
ELIZA：为什么你的问题难以描述？
马丁：因为每当我试图去描述它时，我就哭了。
ELIZA：这是真正的原因吗？
马丁：也许不是。
ELIZA：你似乎并不很确定。
马丁：啊，确定。
ELIZA：你能仔细地讲讲吗？
马丁：可以。但这将涉及一些个人隐私。
ELIZA：你为什么如此肯定?
马丁：我试图维护我的尊严。
ELIZA：你的尊严？
马丁：你不会理解这些的。
ELIZA：我们是在讨论你，而不是我。
马丁：我已经受够了。再见！
ELIZA：你说你已经受够了。
马丁：我说再见。
ELIZA：你能说得再具体一些吗？
马丁：再见。
ELIZA：再见。请付75美元。
```

当然，ELIZA什么都不理解。程序执行的是一种非常简单的算法，如果句子中出现关键字，那么它就会作出响应，否则就只是重复用户的句子。例如，“你”是一个关键词，ELIZA对它的响应通常是“我们是在讨论你，而不是我。”句子“你是我的母亲”中包含“母亲”和“你”这两个关键词。由于“母亲”这个关键词的级别要比“你”这个关键词高，所以ELIZA对于该句的响应将是“再告诉我一些你家庭的情况。”“可以”这个关键词引起了“你为什么是如此肯定？”的响应。注意，只有当“再见”一词出现在句首时，ELIZA才会对它作出响应。

正当计算语言学家们为计算机运行日常语言的能力而不解奋斗之时，人们也自然会在那些不依赖于日常语言的领域中去探求机器智能。其中有一个领域就是下棋。

1996年2月，电脑“深蓝”成功地击败了国际象棋世界冠军加里·卡斯帕罗夫。那么，我们能说“深蓝”具有智能吗？

哲学家约翰·R·塞尔告诉我们说，“深蓝”“有一串毫无意义的符号”。然而，假如你能在“深蓝”运行时看到它的内部，那么你将看不到任何符号，无论是有意义的还是无意义的。电子正在电路中来回运动。这就好像，假如你能在卡斯帕罗夫下棋时看到他的头骨内部的情况，那么你将看不到任何棋子，而只能看到神经元的脉冲。

塞尔强调了“深蓝”不“知道”它在下棋这个事实。事实上，他坚持说“深蓝”不知道任何东西。而那些富有专业知识的工程师却有可能声称，“深蓝”的确知道各种东西。例如，他知道能将给定方格中的象移动到哪几个方格去。

出于很好的理由，图灵和冯·诺伊曼都把电脑与人脑进行了比较。既然人们有那么多不同的思维模式，他们猜想，我们之所以能够做那么多极为不同的事情，是因为在我们的大脑中嵌入了一台通用计算机。这就是为什么冯·诺伊曼着手设计EDVAC时，他会被人工神经元理论深深震撼。通用计算机所能做的只是执行算法。

脑海深处冒了出来一个想法，可以假设这是通过某种算法过程从我们大脑中的数据库里提取所需的信息而实现的。

塞尔和彭罗斯拒不承认人类的心灵就其本质而言等同于一台计算机。但他们两人都心照不宣地接受了这样一个前提，即不论人类的心灵可能是什么，它都是由大脑产生出来的，都服从物理化学规律。而库尔特·哥德尔则愿意相信，大脑实际上就是一台计算机，但他拒不接受超越于人脑的心灵并不存在的观点。事实上，古典的心-身问题是哥德尔所关注的问题的核心。他认为心灵以某种方式独立于我们作为物理实体的存在，他的这种立场通常被称为笛卡尔的二元论。


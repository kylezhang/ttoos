---
categories:
- 开源
- 感悟
date: 2019-03-09T17:43:34+08:00
description: "开源之道一再强调社区才是开源的真正奥秘所在，赢得社区就赢得开源，但想要赢得社区，需参与到社区中来，2018年我们花了很大的篇幅介绍了广义的参与社区篇，2019年则就具体的开源项目社区来做文章，当仁不让，Linux 作为迄今为止全球最大的开源项目，是应该被第一个介绍和学习的。"
keywords:
- Open Source
- Culture
- Reading
- News
tags:
- 每周精选
- 开源之道
title: "如何参与到 Linux 社区中来"
url: ""
---

## 内核开发流程指南

本文档旨在帮助开发者（以及他们的经理们）如何以最小的代价参与到内核的开发社区中来，试图解释Linux社区是如何运转的，进而告诉那些对Linux内核开发（或者，更深入的说，普遍意义的自由软件开发）不熟悉的人们如何去做，虽然这里有一些技术资料，但这是一个针对流程方面的讨论，不需要深入了解内核编程就可以理解，这点请毋须担心。

### 内容摘要

本节剩余部分覆盖的内容包括：内核开发流程、开发人员及其雇主可能遇到的各种坑。解释内核代码为什么应该合并到官方（“主线”）中的各种原因: 自动可用到用户、多种形式的社区支持、以及有能力影响社区开发的方向等。为Linux内核做代码贡献还必须承认 GPL兼容的许可协议。

第二节介绍开发流程、内核发布周期、以及合并窗口的机制。涵盖了补丁开发，审查和合并周期中的各个阶段。有一些关于工具和邮件列表的讨论。我们鼓励希望开始使用内核开发的开发人员将bug作为初步练习进行跟踪和修复。

第三节则为大家介绍项目早期的计划，重点在于尽快的让开发者参与到开发社区中来。

第四节是关于编码流程的，讨论人们经常遇到的陷阱。介绍了补丁的一些要求，以及一些有助于确保正确生成内核补丁的工具。

第五节讨论发布补丁以供审核的过程。要得到开发社区的认真对待，必须对补丁进行适当的格式化和描述，并且必须将它们发送到正确的地方，遵循本节中的建议，将有助于确保开发者的补丁能够被最快的接收。

第六节覆盖了发布了补丁之后发生的事情，因为工作并不是说发完补丁就万事大吉了。和审核代码的开发者一起是开发流程中相当重要的一部分，本节提供了许多关于如何在这个重要阶段避免问题的技巧。千万要谨记，代码即使是合并到主干，也并不表示所有的工作已经完成。

第七节则介绍了一些“高级”的主题，使用git管理补丁并查看其他人发布的补丁。

第八届介绍了内核开发的更多关于指向源的文档信息。

### 本文档是关于什么的

Linux 内核，一款代码超过6百万行、拥有1000多活跃贡献者、世上现有的最大、最活跃的自由软件项目。Linux 自从1991年诞生以来，该内核已发展成为同类中最佳的操作系统核心，它不仅运行在袖珍数字音乐播放器、台式机、现有最大的超级计算机乃至介于两者之间的所有类型的系统上。它是一种强大，高效，可扩展的解决方案，几乎能够适用于所有计算机体系架构。

伴随着 Linux 内核项目的快速增长，相应的希望参与到其中来的开发人员（和公司）的数量也在增长。硬件供应商希望确保 Linux 能够得到很好地支持他们的产品，从而让这些产品对Linux用户更具吸引力。而嵌入式供应商，则将Linux作为组件整合到他们的产品中，希望Linux尽可能满足系统当前的任务。而Linux发行版厂商以及其它的软件供应商则更加希望Linux在可靠性、高性能、灵活性方面有突出的能力。最后是最终用户，也同样希望对Linux进行适当的调整，进而满足自己的独特需求。

Linux最引人注目的特性之一就是让所有的开发人员都可以访问它;任何具备相应技能的人都可以去改进Linux，并尝试影响其未来的发展方向。那些专有的产品是无法提供这样的开放性的，这是自由软件的一个独特特性。其实，话说回来，Linux 内核相比于其它绝大多数的自由软件，更具开放性。最好的证据莫过于：每三个月的内核开发周期，要牵涉到超过1000多名开发人员，他们分别来自100多家不同的公司（当然也有的根本就没有公司）。

在内核开发社区中工作其实并不特别的困难，但是，话虽然这么说，仍然有很多的潜在的贡献者认为在创始参与的时候觉得困难。这么多年，内核社区已经相对成熟了，并发展出了自己独特的操作方式，从而能够在每天变更数千行代码的环境中顺利运行（并生成高质量的产品）。因此，Linux内核开发过程与专有开发方法有很大不同，这并不奇怪。

内核的开发过程可能对新人来说有些陌生，有时还会带着一丝的恐慌，这都算正常现象，尽管如此，内核已经用事实证明，这些都不是事。一个不了解内核社区的方式的开发人员（或者更糟糕的是，试图蔑视或逃避）将会在整个过程中，产生令人沮丧的体验。但是一定要明白一个道理：开发社区虽然对于愿意学习的人有莫大的帮助，但是也就到此为止了，对于那些不愿意花时间认真倾听或不关心开发过程的人来说，内核社区只能表示惋惜。

希望阅读本文档的人能够避免那些让人痛苦不堪的经历。本文包含很多的处理细节，如果可能的话，还是要及时的去亲子体验一把。内核开发社区一直缺人，尤其是那些能够帮助内核变得更好的开发者；以下内容可以帮助到你（又或者是为你工作的开发者），加入到内核社区中来。

### 感谢

本文档由Jonathan Corbet 所撰写，其邮箱地址：[corbet@lwn.net](mailto:corbet@lwn.net)。以及James Berry、Alex Chiang、Roland Dreier、Randy Dunlap、Jake Edge、Jiri Kosina、Matt Mackall、Amanda McPherson、Andrew Morton、以及 Jochen Voß 等的改进。

该文档的撰写得到了Linux基金会的大力支持，尤其要感谢 Amanda McPherson，是他看到了这项工作的价值，并让这一切变为现实。

### 将代码并入主干的重要性

总有一些公司和开发人员偶尔会问起：为什么他们应该学习如何使用内核社区并将他们的代码放入主干（“主干”即是有Linus Torvalds所维护，也是很多linux分发版的基础）。从短期来看，为内核上游社区贡献代码看起来有点得不偿失，似乎是保持现有的分支就可以了，且可以直接支持用户。而事实上，时间稍长即可证明，基于现有的分支（“脱离主干”）会付出很大的代价。

那么我们就来说说脱离主干（out-of-tree)的代价是什么，以下列表从内核开发流程上的一小部分，其中大部分内容将在本文档后面详细讨论。考虑如下情形：

* 合并到内核主干的代码是供所有 Linux 用户使用。它将自动出现在使用它的所有发行版中。不需要驱动程序磁盘，下载或支持多个版本的多个发行版的麻烦;这一切都适用于开发人员和用户。换句话说，并入主干解决了大部分的分发、支持问题。
* 虽然内核开发人员在努力的维护和用户空间接口，希望保持稳定，但是事实上，内核内部的 API 仍在不断的变化。缺乏稳定的内部界面是一个深思熟虑的设计决策;它允许随时进行基本改进，并产生更高质量的代码。基于该策略的一个结果就是，那些脱离主干的分支如果要使用新的内核，就要不断的从主干中获取这些代码，即需要不断的进行维护，而这需要大量的工作才能保持代码正常的工作。

相反，在主干中的代码就没有这些额外的工作，如果有 API 的变更，开发者们就会立即在主干中进行修复和处理。所以，合并到主干的代码在维护成本上具有显著的优势。

* 除此之外，内核中的代码通常会被其他开发人员改进。有的时候，用户社区和客户所改进的产品，往往惊喜不断。
* 内核的代码在合并到主干之前和之后均是审核的，无论这些原创开发人员的技能有多强，这个审核过程总会能找到可以改进代码的地方。通常情况下，这样的审核都能够发现Bug以及安全方面的问题。对于在封闭环境中开发的代码尤其如此，某种程度上讲，linux内核非常受益于这些外部的开发人员的审核。脱离主干（Out-of-tree)的代码将意味着质量难以保证。
* 开发者只要参与到内核的开发中来，就可能会影响到项目的发展方向。如果说用户只是在旁边抱怨的话，真的没有啥意思，不如让事情按照自己的意愿去发生。那些活跃的开发者在社区拥有极强的声音 —— 以及改进的能力，这可以让内核满足他们自身的需求来进行发展和进化。
* 当分支代码被单独维护时，始终存在由第三方提供类似功能的不同实现的可能性。如果发生这种情况的话，合并代码将变得更加困难 —— 甚至到了几乎不可能的地步。真到了那个时候，就面临着令人非常不爽的选择：要么选择无限期地保持脱离主干的非标准特征，要么是放弃这些脱离主干的代码，然后回迁到主干版本。
* 代码的贡献是整个流程的最为基本的行为，这也是之所以现有的流程能够良好运作的前提。通过贡献代码，开发者可以向内核添加自己想要的功能，也是对于其他内核开发人员同样有实际用处。如果你已经为Linux写过代码（或者正在考虑这样做），那么您显然对该平台的持续成功感兴趣;贡献代码是帮助确保成功的最佳方式之一。

以上所有的可能结果，都是脱离主干（out-of-tree)所导致，也包括那些以专有的形式、仅发行二进制的方式。但是，在考虑任何类型的仅二进制内核代码分发之前，还应考虑其他因素。这些包括：

* 发行封闭的内核模块会让法律问题的阴影所笼罩。相当多的内核版权持有者认为，大多数仅二进制模块都是内核的派生产品，而这么做的结果就是，他们的再发行违反了 GNU 通用公共许可证（下文会做详尽的解释）。当然本文的作者并不是一名律师，所以请谨慎对待，本文档中的任何内容都不能被视为是法律建议。关于那些闭源的二进制内核模块的法律问题只能由法院去做决定。但是事情毫无疑问，明白在这里的是这些模块的不确定性是存在的。
* 二进制模块大大增加了调试内核问题的难度，大多数内核开发人员都不会做这样徒劳无功的尝试。因此，仅发布二进制模块将会使得贵司的用户几乎无法获得社区的支持。
* 对于仅二进制模块的分发者来说，支持也更加困难，他们必须为每个分发版本以及他们希望支持的每个内核版本都提供相应的模块。这导致的结果就是，这样一个模块想要全面覆盖相应的正在支持中的内核版本的话，就需要分别做十几个版本，而每次升级内核时，都要单独这么做。
* 上面这几条内容，可以覆盖到所有的闭源的代码中。由于代码是无法获得的，所以社区根本就无法对他们进行审核，这毫无疑问是有可能带来严重问题的。

特别是嵌入式系统的制造商，可能会试图忽视本节所说的大部分内容，因为他们认为他们正在使用一种使用 frozen  的内核版本，且认为在发布后不需要做更多开发的自包含产品。这一做法忽略了广泛的代码审查的价值以及允许用户为其产品添加功能的价值。但这些产品的商业寿命有限，之后必须发布新版本。直到这个时候，恐怕这些供应商才能够明白，如果他们所维护的代码是主干是多么的好！重要的是新产品可以快速的上市。

> 开源之道注: 开源有今天的成功，其中尊重知识产权等法律在其中起着最为关键的作用！首先我们要谈的就是许可证的事情。

### 许可证

Linux内核允许开发者以各式各样的许可证方式下来贡献代码，但是所有这些代码必须与GNU通用公共许可证（GPLv2）的版本2兼容，后者是覆盖内核发布的许可协议。在实践中，这意味着所有代码贡献都由GPLv2（可选地，允许在更高版本的GPL下分发的语言）或三款BSD许可证涵盖。任何不属于兼容许可证的贡献都不会被内核接受。

对于内核的代码，不需要（或请求）版权分配。合并到主线内核的所有代码保留其原始所有权;也就是说，现在的内核拥有数千名所有者。

这种所有权结构的一个含义是，任何改变内核许可的尝试都几乎确定注定要失败。很少有实际情况可以获得所有版权所有者的同意（或者从内核中删除他们的代码）。因此，特别是，在可预见的未来，没有可能迁移到GPL版本3。

所有贡献给内核的代码都必须是合法的自由软件。因此，匿名（或假名）贡献者的代码将不被接受。所有贡献者都需要“签署”他们的代码，声明代码可以在GPL下与内核一起分发。未由其所有者许可为自由软件的代码，或者为内核创建与版权相关的问题（例如源自缺乏适当保护措施的逆向工程的代码）的代码无法获得提交的。

有关版权相关问题的问题在Linux开发邮件列表中是蛮常见的事情。这些问题通常不会得到答案，这里特别提醒的是，回答这些问题的人不是律师，也不能提供法律建议。如果看官有与Linux源代码相关的法律问题，那么就应该去和那些理解该领域的律师去沟通、请教。依靠在技术邮件列表上获得的答案是一件讨人嫌弃的事情。

## 开发流程是如何工作的

Linux 内核在早期的阶段（1990年代）开发相当的松散，当然用户和开发人员数量也是相对少的多。后来，凭借数百万用户群和一年内约2,000名开发人员的参与，内核不断发展壮大，必须修改流程以保持平稳发展。为了更为有效的成为内核开发的一份子，有必要对开发过程的工作原理有充分的了解。

### 宏观视野

内核开发人员使用松散的基于时间的发布过程，每两到三个月发布一次新的主要内核版本。最近的发布版本如下所示：

|  版本号   |     日期       |
| -------------  | ------------- |
|2.6.26|July 13, 2008|
|2.6.25   | April 16, 2008  |
|2.6.24   |January 24, 2008   |
|2.6.23   |October 9, 2007   |
|2.6.22   | July 8, 2007  |
|2.6.21   |April 25, 2007   |
|2.6.20   |February 7, 2007   |

每个2.6.x版本都是一个主要的内核版本，包含新功能，内部 API 变更等。典型的2.6版本包含了超过10,000个变更集，其中包含数十万行代码的更改。2.6因此是Linux内核开发的前沿;内核使用滚动开发模型，该模型不断整合主要变更。

### 补丁的生命周期


### 补丁是如何被接受的

### 分支树

### 工具篇

### 邮件列表


### 内核开发入门

## 早期规划

### 明确问题

### 尽早讨论

### 你都和谁聊过

### 什么时候提交？

### 获得正式接纳

## 获得代码相关的权利

### 陷阱

### 代码检查工具

### 文档

### 内部API 变更

## 提交补丁

### 什么时候提交？

### 在制作补丁之前

### 准备补丁

### 补丁格式

### 发送补丁

## 获得通过

### 审核工作

### 接下来干什么

### 其他可能发生的事情

## 高级主题

### 使用git来管理补丁

### 审核补丁

## 更多帮助内容

## 总结

## 原文链接

[How to Participate in the Linux Community](https://www.linux.com/publications/how-participate-linux-community)，作者 JONATHAN CORBET
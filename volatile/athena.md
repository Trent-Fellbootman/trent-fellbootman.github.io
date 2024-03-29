# Athena: 一个面向软件开发者的AI工具包

## 目标

- 为软件开发者提供更高层级的抽象，在[Mercury](mercury.html)的基础上，进一步降低AI软件开发的门槛。
如果把[Mercury](mercury.html)比作Vulkan/OpenGL/DX12，Athena就是游戏引擎；如果把[Mercury](mercury.html)比作CUDA，Athena就是PyTorch。

## 思路

- 内置各种神经网络应用模块，如多模态、纠错、多选一、文本概括、代码生成等等。
- 提供一种通用的AI软件开发模型：多智能体动态系统，下面重点介绍。

## 多智能体动态系统

多智能体动态系统就是一个多个智能体合作完成一项或几项任务的系统。
这个系统不仅包含智能体，还包含智能体能使用的不智能的服务、工具和结构，如文件系统、网络、Python解释器等。
多智能体动态系统这个开发范式适用于各种AI软件，如游戏、游戏引擎、手机app、操作系统、项目生成器（相当于代码生成器，但一次生成一个完整的项目）等等。

### 一些概念

#### 任务与多智能体动态系统

多智能体动态系统的目标是完成一个任务，这个任务既可以是“一次性的”，如写一个软件，
也可以是持续性的，如作为用户的智能助手，满足用户随时产生的各种需求。

任务的实现是分层的。如果一个任务太难，一个智能体实现不了，它就会将这个大任务拆成多个小任务，
每个小任务分给一个由一个或多个智能体组成的子系统完成。如果小任务还是太难，还会继续拆分。
如“写一个软件”可以被拆成写代码、写文档、写单元测试，“写代码”又可以拆成写前端、写后端、写抽象层等等。

#### 智能体之间的通信

智能体之间的通信采用会话机制，会话可以动态建立和释放。
一个会话往往面向一个小任务。小任务开始时会话发起，结束时会话释放。

智能体需要通过某种机制管理当前活跃的会话。这个机制叫做会话表。
会话表中的每一项对应一个会话，并记录了这个会话的大致内容。
这样，智能体可以通过查看会话表了解各个会话的状态。

会话表是很有用的。
例如，如果一个智能体需要协调多个任务，而这些任务中，A，B可以直接开始，C做到了一半，需要A，B完成后才能继续进行，
那么智能体可以等待A，B完成后向会话C发送A，B已经完成的信息。
如果我们需要人工智能来进行复杂的项目协调，通过会话表中的“会话概述”索引会话显然比哈希等机制对AI更友好。

一个智能体可以告诉另一个智能体它所知道的智能体的地址，这样一个智能体可以通过多次“转接”连接到系统中的任何一个智能体。

#### 智能动态控制流

智能体是可以动态产生的，甚至具体使用什么样的模型都是可以动态决策的。
[Mercury](mercury.html)使得这种动态控制流变得简单。
例如，用户让智能体完成一个商业项目，智能体上网搜索后可能发现搞这个项目需要视频制作、文案撰写等等，
它访问用户的文件系统发现用户并没有安装相关的模型，于是可能通过[Mercury](mercury.html)的模型管理器搜索并安装相应的模型，
然后spawn对应的智能体去完成任务。

## 当前进度

- 五一假期把代码都写完了，docstring也都有，但是没调试，没写单元测试。
- 五一假期的时候还没搞[Mercury](mercury.html)，项目用的是很简单的一个小抽象层。可能需要重写部分代码，让这个项目基于Athena提供的底层抽象。

## 链接

- [GitHub](https://github.com/Trent-Fellbootman/athena)

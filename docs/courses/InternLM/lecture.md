---
icon: fontawesome/solid/chalkboard-user
tags: [Updating]
comments: true
---

#  笔记

书生·浦语大模型实战营

1.   [网课地址](https://www.bilibili.com/video/BV1Rc411b7ns)
2.   [学习手册](https://jpf9plilub.feishu.cn/docx/CjEpd96yhoT4owx6GE7cDvZLnWg)
3.   [Q&A文档](https://cguue83gpz.feishu.cn/docx/Noi7d5lllo6DMGxkuXwclxXMn5f)
4.   GPTs: [https://www.glbai.com/](https://www.glbai.com/)

## L1 书生·浦语大模型全链路开源开放体系

本节课程概要：

![书生浦语全链条开源开放体系](https://s2.loli.net/2024/01/11/4jWzSdMZxgoPEet.webp)

通用大模型能够应对多种任务、多种模态

![通用大模型](https://s2.loli.net/2024/01/11/WQKwGi73JgAspNy.webp)

从模型到应用所需的步骤：

![从模型到应用](https://s2.loli.net/2024/01/11/IFWDt3yjCEhvsbd.webp)

### 数据

开源书生万卷数据集，和 OpenDataLab 平台，[https://opendatalab.com/](https://opendatalab.com/)

![书生万卷](https://s2.loli.net/2024/01/11/XAaBER9o7vwePNk.webp)

### 评测

比较流行的评测数据集：

![评测数据集](https://s2.loli.net/2024/01/11/zfJhItYnDgik9QF.webp)

OpenCompass 开源评测平台，[https://opencompass.org.cn/](https://opencompass.org.cn/)

![OpenCompass平台](https://s2.loli.net/2024/01/11/G7d2IgLmNlPo8ZD.webp)

### 部署

大语言模型部署的技术难点：

![部署](https://s2.loli.net/2024/01/11/jyOrhfdxkqE8Nv9.webp)

LMDeploy: [https://github.com/InternLM/lmdeploy](https://github.com/InternLM/lmdeploy)

![LMDeploy](https://s2.loli.net/2024/01/11/LY8adGnZO4Bvhji.webp)

### 应用

从LLM到智能体，Lagent: [https://github.com/InternLM/lagent](https://github.com/InternLM/lagent)

![智能体](https://s2.loli.net/2024/01/11/z8xvO6owILcsfUl.webp)

AgentLego: [https://github.com/InternLM/agentlego](https://github.com/InternLM/agentlego)

![AgentLego](https://s2.loli.net/2024/01/11/KMzRoe1mAJny584.webp)

## L2 轻松玩转书生·浦语大模型趣味 Demo

文档地址：[https://github.com/InternLM/tutorial/blob/main/helloworld/hello_world.md](https://github.com/InternLM/tutorial/blob/main/helloworld/hello_world.md)

### InternLM-Chat-7B 智能对话 Demo

`InternLM`：[https://github.com/InternLM/InternLM](https://github.com/InternLM/InternLM) 是一个开源的轻量级训练框架，旨在支持大模型训练而无需大量的依赖。基于 `InternLM` 训练框架，上海人工智能实验室已经发布了两个开源的预训练模型：`InternLM-7B` 和 `InternLM-20B`。

1.   Command Line Demo:

     ![Cli Demo](https://github.com/InternLM/tutorial/raw/main/helloworld/images/image-18.png)

2.   Streamlit Web Demo:

     ![Web Demo](https://github.com/InternLM/tutorial/raw/main/helloworld/images/image-6.png)

### Lagent 智能体工具调用 Demo

`Lagent`：[https://github.com/InternLM/lagent](https://github.com/InternLM/lagent) 是一个轻量级、开源的基于大语言模型的智能体（agent）框架，支持用户快速地将一个大语言模型转变为多种类型的智能体，并提供了一些典型工具为大语言模型赋能。架构如图所示：

![Lagent](https://github.com/InternLM/tutorial/raw/main/helloworld/images/Lagent.png)

在 `Web` 页面选择 `InternLM` 模型，等待模型加载完毕后，输入数学问题 已知 `2x+3=10`，求`x` ,此时 `InternLM-Chat-7B` 模型理解题意生成解此题的 `Python` 代码，`Lagent` 调度送入 `Python` 代码解释器求出该问题的解。

![Lagent Demo](https://github.com/InternLM/tutorial/raw/main/helloworld/images/image-7.png)

### 浦语·灵笔图文理解创作 Demo

浦语·灵笔：[https://github.com/InternLM/InternLM-XComposer](https://github.com/InternLM/InternLM-XComposer)，是基于书生·浦语大语言模型研发的视觉-语言大模型，提供出色的图文理解和创作能力，结合了视觉和语言的先进技术，能够实现图像到文本、文本到图像的双向转换。使用浦语·灵笔大模型可以轻松的创作一篇图文推文，也能够轻松识别一张图片中的物体，并生成对应的文本描述。

1.   图文创作：

     ![又见敦煌](https://github.com/InternLM/tutorial/raw/main/helloworld/images/image-9.png)

2.   图片理解：

     ![K-On](https://github.com/InternLM/tutorial/raw/main/helloworld/images/image-10.png)

## L3 基于 InternLM 和 Langchain 搭建你的知识库

文档地址：<https://github.com/InternLM/tutorial/blob/main/langchain/readme.md>

## L4 XTuner 大模型单卡低成本微调实战

文档地址：<https://github.com/InternLM/tutorial/blob/main/xtuner/README.md>

## L5 LMDeploy 大模型量化部署实践

文档地址：<https://github.com/InternLM/tutorial/blob/main/lmdeploy/lmdeploy.md>

## L6 OpenCompass 大模型评测解读及实战指南

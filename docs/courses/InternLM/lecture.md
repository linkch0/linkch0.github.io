---
icon: fontawesome/solid/chalkboard-user
tags: [Updating]
comments: true
---

#  笔记

书生·浦语大模型实战营

1.   网课地址：<https://www.bilibili.com/video/BV1Rc411b7ns>
2.   学习手册：<https://jpf9plilub.feishu.cn/docx/CjEpd96yhoT4owx6GE7cDvZLnWg>
3.   Q&A 文档：<https://cguue83gpz.feishu.cn/docx/Noi7d5lllo6DMGxkuXwclxXMn5f>
4.   GPTs: <https://www.glbai.com/>

## L1 书生·浦语大模型全链路开源开放体系

本节课程概要：

![书生浦语全链条开源开放体系](https://s2.loli.net/2024/01/11/4jWzSdMZxgoPEet.webp)

通用大模型能够应对多种任务、多种模态

![通用大模型](https://s2.loli.net/2024/01/11/WQKwGi73JgAspNy.webp)

从模型到应用所需的步骤：

![从模型到应用](https://s2.loli.net/2024/01/11/IFWDt3yjCEhvsbd.webp)

### 数据

开源书生万卷数据集，和 OpenDataLab 平台，<https://opendatalab.com/>

![书生万卷](https://s2.loli.net/2024/01/11/XAaBER9o7vwePNk.webp)

### 评测

比较流行的评测数据集：

![评测数据集](https://s2.loli.net/2024/01/11/zfJhItYnDgik9QF.webp)

OpenCompass 开源评测平台，<https://opencompass.org.cn/>

![OpenCompass平台](https://s2.loli.net/2024/01/11/G7d2IgLmNlPo8ZD.webp)

### 部署

大语言模型部署的技术难点：

![部署](https://s2.loli.net/2024/01/11/jyOrhfdxkqE8Nv9.webp)

LMDeploy: <https://github.com/InternLM/lmdeploy>

![LMDeploy](https://s2.loli.net/2024/01/11/LY8adGnZO4Bvhji.webp)

### 应用

从LLM到智能体，Lagent: <https://github.com/InternLM/lagent>

![智能体](https://s2.loli.net/2024/01/11/z8xvO6owILcsfUl.webp)

AgentLego: <https://github.com/InternLM/agentlego>

![AgentLego](https://s2.loli.net/2024/01/11/KMzRoe1mAJny584.webp)

## L2 轻松玩转书生·浦语大模型趣味 Demo

文档地址：<https://github.com/InternLM/tutorial/blob/main/helloworld/hello_world.md>

### InternLM-Chat-7B 智能对话 Demo

`InternLM`：<https://github.com/InternLM/InternLM> 是一个开源的轻量级训练框架，旨在支持大模型训练而无需大量的依赖。基于 `InternLM` 训练框架，上海人工智能实验室已经发布了两个开源的预训练模型：`InternLM-7B` 和 `InternLM-20B`。

1.   Command Line Demo:

     ![Cli Demo](https://github.com/InternLM/Tutorial/blob/camp1/helloworld/images/image-18.png)

2.   Streamlit Web Demo:

     ![Web Demo](https://github.com/InternLM/Tutorial/blob/camp1/helloworld/images/image-6.png)

### Lagent 智能体工具调用 Demo

`Lagent`：<https://github.com/InternLM/lagent> 是一个轻量级、开源的基于大语言模型的智能体（agent）框架，支持用户快速地将一个大语言模型转变为多种类型的智能体，并提供了一些典型工具为大语言模型赋能。架构如图所示：

![Lagent](https://github.com/InternLM/Tutorial/blob/camp1/helloworld/images/Lagent.png)

在 `Web` 页面选择 `InternLM` 模型，等待模型加载完毕后，输入数学问题 已知 `2x+3=10`，求`x` ,此时 `InternLM-Chat-7B` 模型理解题意生成解此题的 `Python` 代码，`Lagent` 调度送入 `Python` 代码解释器求出该问题的解。

![Lagent Demo](https://github.com/InternLM/Tutorial/blob/camp1/helloworld/images/image-7.png)

### 浦语·灵笔图文理解创作 Demo

浦语·灵笔：<https://github.com/InternLM/InternLM-XComposer>，是基于书生·浦语大语言模型研发的视觉-语言大模型，提供出色的图文理解和创作能力，结合了视觉和语言的先进技术，能够实现图像到文本、文本到图像的双向转换。使用浦语·灵笔大模型可以轻松的创作一篇图文推文，也能够轻松识别一张图片中的物体，并生成对应的文本描述。

1.   图文创作：

     ![又见敦煌](https://github.com/InternLM/Tutorial/blob/camp1/helloworld/images/image-9.png)

2.   图片理解：

     ![K-On](https://github.com/InternLM/Tutorial/blob/camp1/helloworld/images/image-10.png)

## L3 基于 InternLM 和 Langchain 搭建你的知识库

文档地址：<https://github.com/InternLM/tutorial/blob/main/langchain/readme.md>

### 大模型开发范式

LLM 大模型的局限性

-   知识时效性受限：如何让 LLM 能够获取最新的知识

-   专业能力有限：如何打造垂域大模型
-   定制化成本高：如何打造个人专属的 LLM 应用

1.   RAG (Retrieval Augmented Generation) 检索增强生成

     核心思想：给大模型外挂一个知识库，对于用户的提问，会首先从知识库中匹配到提问，对应回答的相关文档，然后将文档和提问一起交给大模型来生成回答，从而提高大模型的知识储备。

     RAG 流程图：

     ![RAG](https://s2.loli.net/2024/01/21/adAKxqfm4QjoRu6.webp)

     1.   对于每一个用户输入，首先将基于向量模型 Sentence Transformer，将输入文本转化为向量；
     2.   在 Chroma 向量数据库中匹配相似的文本段，我们认为与问题相似的文本段大概率包含了问题的答案；
     3.   然后我们会将用户的输入和检索到的相似文本段一起嵌入到模型的 Prompt 中，传递给 InternLM 模型，要求模型对问题作出最终的回答，作为最后的输出。

     RAG 优缺点：

     -   低成本且可实时更新：对于新的知识，只需组织加入到外挂知识库中即可，无需对大模型进行重新训练，不需要 GPU 算力；

     -   能力受基座模型影响：大基座模型的能力上限极大程度决定的 RAG 应用的能力天花板；
     -   单次回答知识有限：RAG应用每次需要将检索到的相关文档和用户提问一起交给大模型进行回答，占用了大量的模型上下文；
     -   对于一些需要大跨度收集知识，进行总结性回答的问题表现不佳。

2.   Finetune 微调

     核心思想：在一个新的较小的训练集上，进行轻量级的训练微调，从而提升模型在这个新数据集上的能力。

     Finetune 优缺点：

     -   可个性化微调：Finetune 范式的应用将在个性化数据上微调，充分拟合个性化数据，尤其是对于非可见知识，如回答风格模拟效果非常好；
     -   知识覆盖面广：Finetune 范式的应用是一个新的个性化大模型，具有大问题的广阔知识域；
     -   成本高昂：需要在新的数据集上进行训练，需要很多的GPU算力和个性化数据；
     -   无法实时更新：更新成本高。

### LangChain 简介

LangChain 框架 (<https://github.com/langchain-ai/langchain>) 是一个开源工具，能够为各种 LLM 提供通用接口来简化应用程序的开发流程，帮助开发者自由构建大模型应用。LangChain 的组件包括：

-   提示 (Prompts) : 使模型执行操作的方式；
-   模型 (Models) ：大语言模型、对话模型，文本表示模型。目前包含多个模型的集成；
-   索引 (Indexes) : 获取数据的方式，可以与模型结合使用；
-   链 (Chains) : 端到端功能实现。Eg. 检索问答链，覆盖实现 RAG 的全部流程；
-   代理 (Agents) : 使用模型作为推理引擎。

基于 LangChain 搭建 RAG 应用：

![LangChain & RAG](https://s2.loli.net/2024/01/21/7P1UgaC5rDxnTG2.webp)

1.   首先对于以本地文档形式存在的个人知识库，会使用 Unstructed Loader 组件来加载本地文档，这个组件会将不同格式的本地文档统一转换为纯文本格式；
2.   然后通过 Text Splitter 组件，对提取出来的纯文本进行分割成 Chunks；
3.   再通过开源词向量模型 Sentence Transformer 来将文本段转化为向量格式，存储到基于 Chroma 的向量数据库中；
4.   接下来对于用户的每一个输入 Query，会首先通过 Sentence Transformer，将输入转化为同样维度的向量；
5.   通过在向量数据库中进行相似度的匹配，找到和用户输入相关的文本段；
6.   将相关的文本段嵌入到已经写好的 Prompt Template 中，再交给 InternLM 进行最后的回答即可。

上述这一整个过程都会被封装在检索问答链中，我们可以直接将个性化的配置引入到检索问答里的对象，即可构建属于自己的 RAG 应用。

### 构建向量数据库

![构建向量数据库](https://s2.loli.net/2024/01/21/9wQ5aqpzBrdAP7I.webp)

### 搭建知识库助手

构建检索问答链：

![构建检索问答链](https://s2.loli.net/2024/01/21/WayFLsSGVIK1lm5.webp)

RAG 方案优化建议：

![RAG 方案优化建议](https://s2.loli.net/2024/01/21/B7zIMNJ4svlnxf2.webp)

## L4 XTuner 大模型单卡低成本微调实战

文档地址：<https://github.com/InternLM/tutorial/blob/main/xtuner/README.md>

Fine-tune 简介

![Fine-tune](https://s2.loli.net/2024/01/27/zHpAcQgj9BWym1k.webp)

### 指令跟随微调

![指令微调1](https://s2.loli.net/2024/01/27/qodwWtXb7KJDFeO.webp)

![System User Assistant](https://s2.loli.net/2024/01/27/LRe5hMJHSldGYg7.webp)

![对话模板](https://s2.loli.net/2024/01/27/fPygQW1HXD8ZvRK.webp)

![Loss](https://s2.loli.net/2024/01/27/x513MK8BXtekh4z.webp)

### 增量预训练微调

![ ](https://s2.loli.net/2024/01/27/2WhmpHljcZ6XNA9.webp)

### LoRA & QLoRA

LoRA: Low Rank Adaptation of Large Language Models

-   LLM 的参数量主要集中在模型中的 Linear，训练这些参数会耗费大量的显存
-   LoRA 通过在原本的 Linear 旁，新增一个支路，包含两个连续的小 Linear，新增的这个支路通常叫做 Adapter
-   Adapter 参数量远小于原本的 Linear，能大幅降低训练的显存消耗

![LoRA](https://s2.loli.net/2024/01/27/hBZQrUXwIOPpH2S.webp)

想象一下，你有一个超大的玩具，现在你想改造这个超大的玩具。但是，对整个玩具进行全面的改动会非常昂贵。因此，你找到了一种叫 LoRA 的方法：只对玩具中的某些零件进行改动，而不是对整个玩具进行全面改动。而 QLoRA 是 LoRA 的一种改进：如果你手里只有一把生锈的螺丝刀，也能改造你的玩具。

-   **Full** : 😳 → 🚲
-   **[LoRA](http://arxiv.org/abs/2106.09685)** : 😳 → 🛵
-   **[QLoRA](http://arxiv.org/abs/2305.14314)** : 😳 → 🏍

![LoRA & QLoRA](https://s2.loli.net/2024/01/27/bWO2I3BHdrEQcUa.webp)

## L5 LMDeploy 大模型量化部署实践

文档地址：<https://github.com/InternLM/tutorial/blob/main/lmdeploy/lmdeploy.md>

## L6 OpenCompass 大模型评测解读及实战指南

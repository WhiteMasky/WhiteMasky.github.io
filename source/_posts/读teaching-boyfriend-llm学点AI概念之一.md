---
title: 读teaching-boyfriend-llm学点AI概念之一
tags: []
categories: []
keywords: []
description: ''
top_img: ''
comments: true
cover: false
date: 2025-05-11 01:26:10
abbrlink:
---

终于在听说了这个很久之后第一次打开，显然既没有boyfriend也不懂LLM。这两年大模型太火了，几乎成为了所有引领科技概念的代名词。不过领域发展得太快了，很多两年前GPT刚出世时的概念现在已经变成了过去式，再加上个人其实能力有限又其实对云本身更感兴趣一些（虽然也不懂），一直来都是半解的状态。接下来要上班的话，好像逃不了学习这方面相关的知识，也不会深入到具体实现，不过我还是看看原理然后记个概念吧。

也没什么具体的内容，就是经常听到的几个概念的英文和通俗化解读。

------

Pre-train: 语料 → 去噪，tokenizer → LLM(Base)

Fine-tune: LLM(Base) → SFT(Supervised Fine-tuning专家)，RLHF(Reinforcement Learning from Human Feedback用户) → Fine-tuned Model

Tokenization的方式

subword-based BPE byte-pair encoding 字符 次数 合并

BBPE 字节

WordPiece 概率而非次数

Unigram 先全初始化再删减

SentencePiece 多语言

------

自注意力机制和KV-Cache（因为单向注意力可以把直接把前面算过的KV存起来）
$$
\text{Attention}(Q, K, V) = \text{softmax} \left( \frac{QK^\top}{\sqrt{d_k}} \right) V
$$

- $ QK^\top \in \mathbb{R}^{n \times n} $：每对单词间的相关性（相似度）  
- $ \sqrt{d_k} $：用于缩放，避免数值过大  
- softmax：将相似度转换为概率分布（注意力权重）

------

`MHA` Multi-head Attention slow

`MQA` Multi-query Attention fast

`GQA` Group-query Attention 折中方案

------

位置编码的方式：

绝对 Transformer

可学习 Bert

旋转 RoPE 关注相对编码信息

Alibi 偏置项 Transformer

------

BatchNorm → LayerNorm → RMSNorm 预归一化
$$
\text{SwiGLU}(x) = \text{Linear}(x) \cdot Sigmoid(\text{Linear}(x))
$$
有主值和激活函数，线性单元加门控机制能够很好地表达非线性关系

P.S. 表示激活函数时Sigmoid和 $\sigma$ 完全等价，不过标准差或者求和时就不等价了

decoding在采样时可以用Beam Search替代Greedy Search（beam_num=1的退化版），保留多个采样点增强性能，因为直接局部贪心不一定全局结果最佳

------

LLAMA3

decoder-only架构

Tokenizer: TikToken

GQA

RMSNorm

RoPE

KV-Cache

Ghost Attention 增强指令的长期记忆

RLHF：PPO近端 DPO直接

SwiGLU

------

PEFT parameter effective fine-tuning

用最小化微调参数的数量和计算复杂度的方式减小模型微调的时间和金钱开销

LoRA Low-Rank Adaptation of Large Language Models

新增低秩矩阵到原权重矩阵

QLoRA 量化+LoRA

Adapter Tuning 新增小的神经网络

Prefix Tuning 输入增加可训练的上下文前缀，同一个模型可以针对前缀完成不同方向的任务

Prompt Tuning 输入增加可训练的嵌入向量提示

P-Tuning 输入增加可训练的LSTM生成的嵌入向量提示

P-Tuning V2 多个N中输入增加可训练的LSTM生成的嵌入向量提示

------

RAG retrieval-augmented generation

知识库 → 粗排SBERT → 精排LTR(LGBMBanker) → Prompt

Pipeline：Query Construction → Query Translation → Routing → Retrieval → Indexing → Generation

自然语言到可查询 → 复杂问题易检索 → 检索方式 → 排序过滤增强相关性 → 文档处理以便高效检索 →答案再优化

前几步：

Multi Query Retriever 多个不同视角查询

RAG-Fusion 互惠排民融合

Decomposition 拆成多个子问题

Step Back 思维链

HyDE 假设文档



LangChain LLM应用的Python框架



- Logical Routing

Question → Function Calling(OpenAI)/Structured Output(LangChain) → Database

- Semantic Routing

Question → Embedding → Prompt 1/2/3 → Best Similar Prompt → LLM



Query Construction

Text to：

​		- metadata filter

​		-  SQL

​		- SQL + semantic

​		- Cypher



KG知识图谱



Indexing

Chunking 文本切分

Multi-representation Indexing 文本&文档



RAPTOR 递归式文档+聚类



ColBERT

解决了DPR的不熟悉的术语名词和不相干的冗余信息问题

------

Summary

听过的概念有 预训练、微调、自注意力机制、KV-Cache、Transformer、BERT、LoRA、RAG、LangChain
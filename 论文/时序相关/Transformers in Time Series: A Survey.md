## Transformers in Time Series: A Survey

类型：综述

作者：达摩院

日期：2022.07

内容：Transformer在时序上的应用

下载：[Transformer应用于时序任务的综述【2022by阿里达摩院】](https://arxiv.org/pdf/2202.07125.pdf)





#### 4.2 Attention Module

Transformer的核心是自注意力机制。它的复杂度是 $O(L^2)$，( $L$ 是输入序列的长度)，因此处理长序列时，Transformer会达到计算瓶颈。 

新的Transformer被提出降低平方复杂度，主要分为两种：

- 引入稀疏注意力机制(sparsity)。

  LogTrans，Pyraformer。

- 探索自注意力矩阵的低秩属性，加速计算。

  Informer，FEDformer。

流行的Transformer模型的时空复杂度：

![image-20221102215146106](.pic/image-20221102215146106.png)



#### 4.3 Architecture-Level Innovation

除了在Transformer的架构上修改之外，很多工作在修改Transformer的架构 [Zhou et al., 2021; Liu et al., 2022] 。
## Transformers in Time Series: A Survey

类型：综述

作者：达摩院

日期：2022.07

内容：Transformer在时序上的应用

下载：[Transformer应用于时序任务的综述【2022by阿里达摩院】](https://arxiv.org/pdf/2202.07125.pdf)



### 1-3 介绍了Transformer



![image-20221103162928223](.pic/image-20221103162928223.png)



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

最近的工作把分层的架构(hierarchical architecture)引入了Transformer，从而考虑时序的muti-resolution方面。

**Informer**在attention块之间插入了一个步长为2的最大池化层，作用是把序列切成一半。

**Pyraformer**设计了一个基于attention机制的 $C-ary$ 树，其中最细尺度的节点对应于原始时间序列，而较粗尺度的节点表示分辨率较低的序列。Pyraformer提出了intra-scale和inter-scale注意力，目的是更好的捕获不同分辨率的时间相关性。分层架构计算更高效，尤其对于长的时间序列来说。



### 5 Applications of Time Series Transformers

预测，异常检测，分类。

#### 5.1 Transformers in Forecasting



##### Time Series Forecasting

**LogTrans**提出了卷积自注意力，使用因果卷积在自注意力层产生q,k。引入了稀疏偏置，一个Logsparse mask，这样在一个自注意力模型中，能够减少计算量($O(l^2)$ 到 $O(LlogL)$)。

**Informer**没有明确提出稀疏自注意力，它使选择基于q,k之间相似度的 $O(log L)$ 的主要queries，实现了和LogTrans相似的计算复杂度。它也设计了一个生成式的decoder去直接生成长周期的预测，并且因此避免了累积的错误(在使用one forward预测时产生的)。

**AST**使用了一个生成式对抗encoder-decoder框架训练一个稀疏Transformer。它展示了对抗训练可以改善序列的预测效果，通过直接shape网络的输出分布，来避免one-step ahead inference的累积错误。

**Autoformer**设计了一个简单的季节性趋势分解架构，并将自相关机制替换了注意力模块。自相关模块测试了time-delay的相似性，在输入信号和聚合顶部k个相似的子序列之间，然后输出，计算复杂度是 $O(LlogL)$ 。

**FEDformer**把attention应用到了频域，使用傅里叶变换和小波变换。它实现了线性的复杂度，通过随机算则一个固定大小的频率子集。

由于Autoformer和FEDformer的成功，吸引了很多人去探索在频域上的自注意力机制。

**TFT**设计了一种多视野预测具有静态协变量的encoder，门控特征选择和自注意力decoder。它编码并选择来自各种协变量的有用信息来执行预测。它还保留了全局可解释性，时间依赖性和event。

**SSDNet**和**ProTran**将Transformer与状态空间模型相结合以提供概率预测。SSDNet首先使用Transformer学习时间模式并估计SSM的参数，然后应用SSM执行季节趋势分解并保持可解释性。ProTran设计了一个基于变分推理的生成建模和推理过程。

**Pyraformer**设计了一个具有二叉树跟踪路径(binary tree following path)的分层金字塔型的注意力模块，以捕捉不同范围的时间依赖性，时空复杂度是线性的。

**Aliformer**通过使用具有分支的Knowledge-guided attention来修改和消除注意力图，对时间序列数据进行顺序预测。



##### Spatio-Temporal Forecasting

我们既要考虑时间又要考虑空间的依赖对于时空预测来说。

**Traffic Transforme**设计了一个使用自注意力encoder-decoder结构捕获时间之间的依赖，一个GNN得到空间依赖。

**Spatial-temporal Transformer**预测交通流动。一个时间Transformer和一个空间Transformer和一个GNN。

**Spatio-temporal graph Transformer**设计了基于注意力的图卷积机制，去捕获更复杂的时空信息，它也用于预测交通流。



##### Event Forecasting

具有不规则和异步时间戳的事件序列数据在许多实际应用中很自然地被观察到，这与具有等采样间隔的规则时间序列数据形成了对比。事件预测或预测旨在根据过去事件的历史，预测未来事件的时间和标志，上述情况通常使用**TPP**(temporal point processes)建模。

最近TPP把Transformer应用到了事件预测。

**Self-attentive Hawkes process (SAHP)**和**Transformer Hawkes process (THP)**使用了Transformer encoder结构总结历史事件的影响，然后计算一个强度函数(intensity function)去预测事件。他们通过将时间间隔转换为正弦函数来修改位置编码，从而可以利用事件之间的间隔。

**attentive neural Datalog through time (A-NDTT)**是上述两个方法的扩展，把所有和事件、时间相关的都用attention做了embedding。



#### 5.2 Transformers in Anomaly Detection

深度学习在异常检测领域的一些工作：**anomaly detection [Ruff et al., 2021]**。重构模型(Reconstruction model)学习一个神经网络：把先验分布 $Q$ 映射到输入的真实分布 $P^+$。$Q$ 一般是高斯分布或均匀分布。异常分数定义为重构的error，即和真实分布之间的差距，越低越好。设置一个阈值检验异常。

[Meng et al., 2019]提出了Transformer在该领域的优点。检测质量高(measured by F1)，由于可以并行，计算的更快(相对于基于LSTM的模型)。

**TranAD**，**MT-RVAE**，**TransAnomaly** 都提出了把Transformer和生成模型结合，像**VAEs**和 **GANs** ，这样可以得到更好的重构模型。

**TranAD**提出了一种对抗性训练程序，以放大重建误差，因为简单的基于Transformer的网络往往会错过异常的小偏差。GAN式对抗训练程序由两个Transformer编码器和两个Transformer解码器设计，以获得稳定性。

**MT-RVAE**和**TransAnomaly**把VAE和Transformer结合到一起, they share different purposes. TransAnomaly为了减少训练的计算量(减少80%)。MT-RVAE使用multiscale Transformer提取不同尺寸的时间序列信息，它克服了传统方法只能提取局部的序列信息的缺点，它能看到全部的序列信息。

**Several time series Transformer**是对于多变量的时间序列设计的，它把Transformer和基于图学习的架构结合起来，比如**GTA**。

MT-RVAE也适用于多变量时间序列，但在图神经网络模型不能很好地工作的情况下，序列之间的维数很少或关系不够紧密。为了解决这个问题，MT-RVAE修改了位置编码，引入了s feature-learning模块。

GTA包含图卷积结构来建模影响传播过程(l the influence propagation process)。和MT-RVAE相似，GTA也考虑了全局的信息，它把多头注意力换成了multi-branch attention，即global-learned attention, vanilla multi-head attention，neighborhood convolution的组合。

**AnomalyTrans**把Transformer和Gaussian Prior-Association组合起来让异常更容易区分。这个和TranAD想法很像，但是他们实现的方法大不一样。一个观点：与正常情况相比，异常情况更难与整个序列建立强关联，而与相邻时间点建立强关联则更容易。AnomalyTrans，先验关联和序列关联被同时建模。除了重建损失之外，异常模型还通过极大极小策略进行优化，以约束先验关联和序列关联，从而更容易区分关联差异。



#### 5.3 Transformers in Classification

用于分类的Transformers通常使用一个简单的encoder结构，自注意力层进行表征学习，MLP输出分类概率。

**GTN**使用一个two-tower的Transformers ，tower分别是：time-step-wise的attention和channel-wise的attention。为了合并和两个tower输出的特征，使用一个可学习的权重concat(也称为"gating")。在13个多变量时间序列分类上达到了SOT。

[Rußwurm and Korner, 2020 ]研究了基于Transformer的方法，用于原始光学卫星(raw optical satellite)的时序分类，达到了最好的结果，和CNN，RNN相比。

**Pre-trained Transformers**在分类问题上也能用。

**[Yuan and Lin, 2020]** 研究了Transformer在卫星上的图像时序分类。作者使用自监督预训练的方法(数据标签不够)。

**[Zerveas et al., 2021]** 引入了无监督预训练方法，模型在预训练时mask掉一定比例的数据。然后预训练模型在之后的下游任务中微调，比如分类。

**[Yang et al., 2021]** 提出使用大规模的预训练语音信号处理模型，然后应用于下游的时序分类，并在30个流行的时序分类数据集上得到了19个不错的结果。
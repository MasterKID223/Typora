## Transformer

作者：谷歌

下载：[https://arxiv.org/pdf/1706.03762.pdf](https://arxiv.org/pdf/1706.03762.pdf)

题目：*Attention Is All You Need*



#### 摘要

之前的序列转导模型都和CNN和RNN(包含encoder和decoder)相关，效果最好的模型也使用一个attention机制把encoder和decoder连接在一起。

Transform：一个简单的网络架构，不用rnn和卷积，只单独的基于attention机制。



#### 结论

提出了Transformer，第一个只基于attention的序列转导模型，用multi-headed self-attention代替了encoder-decoder架构的RNN。

训练比RNN和CNN更快（多头可以并行）。

可以应用到图像，音频，视频上，使得生成不那么时序化。



#### 介绍

RNN，LSTM，Gated RNN（GRU）在序列模型和转导问题(语言模型和机器翻译)上都有SOT的性能。

在一个句子中，RNN顺序的读每一个单词，当前单词的隐层输出是 $h_t = f(h_{t-1}, word_t)$，这样RNN就把之前的单词的所有信息放在了隐藏状态中，这样就能有效的处理时序信息。RNN缺点：不能并行计算，如果要保存前面每个单词的隐藏信息，那么 $h_t$ 就必须很大，内存开销也很大。

attention应用在RNN上增加了计算的并行性。

Transformer不用循环的结构，只用attention来捕捉输入和输出之间的全局依赖。并行性更强。



#### 相关工作

基于CNN的网络，要得到两个记录很远的信号之间的联系，需要大量计算（不停的卷积）。在Transformer中，复杂度降为一个常数。CNN可以输出多个通道，每个通道可以看成识别一个模式，Transformer也想达到这个效果，于是就提出了Multi-Head Attention机制。

Self-attention（也 intra-attention）一种attention机制，把一个序列中不同位置联系起来，然后计算序列的表示。

End-to-end memory networks基于循环注意力机制，代替了序列对齐循环（sequencealigned recurrence）。



#### 模型架构

过去时刻的输出可能作为现在的输入，这个叫自回归。
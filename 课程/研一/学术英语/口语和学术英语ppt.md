#### 口语

题目：Few-shot classification

1. What's is few-shot learning

   - 和传统的大数据训练方式不同，大数据的方式是教会模型如何分类，而这个类在训练集中出现过。
   - 小样本学习可以理解为，是教会模型如何去学，从给定的一些样例中学出一种模式，从而对查询图像进行分类，这个类在训练集中没有出现过。
   - 把数据集分成很多独立的任务，每个任务中都有support set和query set。你可以这样理解，把他们分别对应为大数据方法中的训练集和测试集。

2. Vit

   - 在许多工作中，想得到一张图像的嵌入向量，一般是用基于CNN的特征提取器。
   - 但是由于卷积由于感受野限制，固有局限性，所以我们用一个简单的ViT替换掉原来的卷积网络，以便得到在接下来的步骤中，更有用的特征。
   - ViT是把传统的Transformer应用到视觉上的一个方法，[ViT]的具体方法。

3. contrastive learning

   - 在传统的分类问题中，通常用最小化交叉熵损失的方法去优化网络。
   - 受之前一些对比学习工作的启发，我们发现把对比损失用到小样本学习中可以提高分类的准确率。
   - 那么什么是对比损失呢，一般叫做infoNCE loss，它的作用就是让同类之间的特征更近，不同类之间的特征更远，从而让模型学到一个更具有区分性的模式，用来对图像进行分类。

4. conclusion

   在我们最近的工作中，我们在我们原来的方法中，添加了infoNCE loss 和 ViT 特征提取器，经过实验，这些方法确实带来了一些性能上的提升。



#### 稿子

The title of this academic presentation is few-shot classification.

I will explain my recent work in three points.

First, what is few-shot learning? Few-shot learning is different from those methods that train in a big dataset. The traditional deep learning models try to classify classes which appear in train dataset. But few-shot models can classify classes which are not seen in train dataset. Few-shot learning aims to make the model acquire the ablilty of how to learn to learn from support set in each task. Before starting this process, we divide the dataset into many independent tasks, in each task, there are two sets: support set and query set. You can simply consider them as train set and test set.

Second, before Transformer proposed, in many works, if want to obtain a embedding feature of an image, we usually use a CNN-based network. But convolution is limited to its receptive fields size, to obtain a more efficient feature for next step, we use a ViT instead of original convolution networks. Specifically, we split an tensor, which is transform form an image, into fixed-size patches, linearly embed each of them, add position embeddings, and feed the resulting sequence of vectors to a standard Transformer encoder.

Finally, for a classification, a common method is that use CrossEntropy loss to optimize a network. Inspired by some previous works, we find thet add the contrastive loss to our current work can help to make an performance improvement. We call the contrastive loss InfoNCE loss, which can make features from same classes more closer, meanwhile make features from different classes more discriminate. So we can get a model which learned a more discriminate pattern to finish a classification task.

（学术英语加这一段）Now we get a trained model, in the test stage, we use two methods to classify. If we do not operate normalization, the results are relatively poor. LR is Logistic Regression, we use the function in sklearn repo to implement it. NN is Nearst Neighbors.

In conclusion, in our recent work, we use InfoNCE loss and a ViT feature extractor, and we did some experiments to show these changes exactly make some performance improvements.

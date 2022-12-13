#### 稿子

The title of this academic presentation is few-shot classification.

I will explain my recent work in three points.

First, what is few-shot learning? Few-shot learning is different from those methods that train in a big dataset. The traditional deep learning models try to classify classes which appear in train dataset. But few-shot models can classify classes which are not seen in train dataset. Few-shot learning aims to make the model acquire the ablilty of how to learn to learn from support set in each task. Before starting this process, we divide the dataset into many independent tasks, in each task, there are two sets: support set and query set. You can simply consider them as train set and test set.

Second, before Transformer proposed, in many works, if want to obtain a embedding feature of an image, we usually use a CNN-based network. But convolution is limited to its receptive fields size, to obtain a more efficient feature for next step, we use a ViT instead of original convolution networks. Specifically, we split an tensor, which is transform form an image, into fixed-size patches, linearly embed each of them, add position embeddings, and feed the resulting sequence of vectors to a standard Transformer encoder.

Finally, for a classification, a common method is that use CrossEntropy loss to optimize a network. Inspired by some previous works, we find thet add the contrastive loss to our current work can help to make an performance improvement. We call the contrastive loss InfoNCE loss, which can make features from same classes more closer, meanwhile make features from different classes more discriminate. So we can get a model which learned a more discriminate pattern to finish a classification task.

（学术英语加这一段）Now we get a trained model, in the test stage, we use two methods to classify. If we do not operate normalization, the results are relatively poor. LR is Logistic Regression, we use the function in sklearn repo to implement it. NN is Nearst Neighbors.

In conclusion, in our recent work, we use InfoNCE loss and a ViT feature extractor, and we did some experiments to show these changes exactly make some performance improvements.

### 2022.12.08

disc + ViT-1，准确率是disc计算的，infonce的实现是把所有同类和不同类加起来求平均

<img src="./pic/image-20221214211710614.png" alt="image-20221214211710614" style="zoom: 33%;" />

<img src="./pic/image-20221214211732815.png" alt="image-20221214211732815" style="zoom:33%;" />

只有ViT-1

<img src="./pic/image-20221214211940259.png" alt="image-20221214211940259" style="zoom:33%;" />

<img src="./pic/image-20221214211951720.png" alt="image-20221214211951720" style="zoom: 33%;" />



### 2022.12.14

第3999个episodes开始出现损失计算为nan。infonce计算方式如下，存在的问题如下。infonce出现负值。

<img src="./pic/image-20221214212039985.png" alt="image-20221214212039985" style="zoom:50%;" />

<img src="./pic/image-20221214212144971.png" alt="image-20221214212144971"  />

出现nan的可能原因：[[知乎](https://zhuanlan.zhihu.com/p/89588946)]

<img src="./pic/image-20221214204501422.png" alt="image-20221214204501422" style="zoom: 33%;" />

<img src="./pic/image-20221214204540766.png" alt="image-20221214204540766" style="zoom:33%;" />

<img src="./pic/image-20221214204557110.png" alt="image-20221214204557110" style="zoom: 50%;" />

现在把损失改回来，分母上包含同类和不同类。计算损失之前，对ViT的(128,2)的特征做归一化处理。

<img src="./pic/image-20221214213028772.png" alt="image-20221214213028772" style="zoom: 50%;" />

<img src="./pic/image-20221215150949519.png" alt="image-20221215150949519" style="zoom:33%;" />

<img src="./pic/image-20221215151010587.png" alt="image-20221215151010587" style="zoom:33%;" />

ViT改为6层，输出的特征改成(128,1)，准确率不计算。

<img src="./pic/image-20221215151203938.png" alt="image-20221215151203938"  />

<img src="./pic/image-20221215151217963.png" alt="image-20221215151217963"  />

再上面实验的基础上加了discriminator，用来计算准确率


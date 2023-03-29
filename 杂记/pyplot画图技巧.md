### legend位置

[csdn](https://blog.csdn.net/Poul_henry/article/details/82533569)

在plt.legend()函数中加入若干参数：plt.legend(bbox_to_anchor=(num1, num2), loc=num3, borderaxespad=num4)

bbox_to_anchor(num1,num2)表示legend的位置和图像的位置关系，num1表示水平位置，num2表示垂直位置。num1=0表示legend位于图像的左侧垂直线(这里的其它参数设置：num2=0,num3=3,num4=0)。

由于legend是一个方框，bbox_to_anchor=(num1, num2)相当于表示一个点，那么legend的哪个位置位于这个点上呢。参数num3就用以表示哪个位置位于该点。
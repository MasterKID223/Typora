

##### [超详细 LaTex数学公式](https://blog.csdn.net/ViatorSun/article/details/82826664)

##### 数学公式的例子：

$$
\begin{aligned}
\frac{\partial}{\partial \theta} \mathcal{L}_{\mathrm{MLE}} &=\mathbb{E}_{w \sim \tilde{p}(w \mid c)} \frac{\partial}{\partial \theta} \log u_\theta(w, c)-\frac{\partial}{\partial \theta} \log Z(c) \\
&=\mathbb{E}_{w \sim \tilde{p}(w \mid c)} \frac{\partial}{\partial \theta} \log u_\theta(w, c)-\mathbb{E}_{w \sim p_\theta(w \mid c)} \frac{\partial}{\partial \theta} \log u_\theta(w, c) \\
&=\sum_w \tilde{p}(w \mid c) \frac{\partial}{\partial \theta} \log u_\theta(w, c)-\sum_w p_\theta(w \mid c) \frac{\partial}{\partial \theta} \log _\theta(w, c) \\
&=\sum_w\left[\tilde{p}(w \mid c) \frac{\partial}{\partial \theta} \log u_\theta(w, c)-p_\theta(w \mid c) \frac{\partial}{\partial \theta} \log u_\theta(w, c)\right] \\
&=\sum_w\left[\left(\tilde{p}(w \mid c)-p_\theta(w \mid c)\right) \frac{\partial}{\partial \theta} \log u_\theta(w, c)\right]
\end{aligned}
\tag{9}
$$

- 空格

  ![在这里插入图片描述](./pic/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h5c3RlcmlzaXM=,size_16,color_FFFFFF,t_70.jpeg)


##### 页内跳转

```html
<a href="#233">我想笑</a>
<span name = "233">233</span>
```

##### 修改字体大小

![Typora设置文字属性](pic/format,png.png)

title: 深度学习---之pooling层的作用与缺陷（转载）
author: ZkName
tags:
  - 深度学习
categories: []
date: 2018-08-20 10:20:00
---
###### 作者：谢志宁
链接：[https://www.zhihu.com/question/36686900/answer/130890492](https://www.zhihu.com/question/36686900/answer/130890492 "https://www.zhihu.com/question/36686900/answer/130890492")
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### 个人觉得主要是两个作用：
1、 invariance(不变性)，这种不变性包括translation(平移)，rotation(旋转)，scale(尺度)

2、 保留主要的特征同时减少参数(降维，效果类似PCA)和计算量，防止过拟合，提高模型泛化能力

1. translation invariance：
这里举一个直观的例子(数字识别)，假设有一个16x16的图片，里面有个数字1，我们需要识别出来，这个数字1可能写的偏左一点(图1)，这个数字1可能偏右一点(图2)，图1到图2相当于向右平移了一个单位，但是图1和图2经过max pooling之后它们都变成了相同的8x8特征矩阵，主要的特征我们捕获到了，同时又将问题的规模从16x16降到了8x8，而且具有平移不变性的特点。图中的a（或b）表示，在原始图片中的这些a（或b）位置，最终都会映射到相同的位置。
![](/img/深度学习---之pooling层的作用与缺陷1.png)
2. rotation invariance：
下图表示汉字“一”的识别，第一张相对于x轴有倾斜角，第二张是平行于x轴，两张图片相当于做了旋转，经过多次max pooling后具有相同的特征
![](/img/深度学习---之pooling层的作用与缺陷2.png)
3. scale invariance：
下图表示数字“0”的识别，第一张的“0”比较大，第二张的“0”进行了较小，相当于作了缩放，同样地，经过多次max pooling后具有相同的特征
![](/img/深度学习---之pooling层的作用与缺陷3.png)

转载：[https://blog.csdn.net/zxyhhjs2017/article/details/78607469](https://blog.csdn.net/zxyhhjs2017/article/details/78607469 "https://blog.csdn.net/zxyhhjs2017/article/details/78607469")

![](/img/深度学习---之pooling层的作用与缺陷4.png)
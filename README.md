# dive_into_deeplearning

### 《动手学习深度学习》之---正向传播、反向传播和通过时间反向传播， 课后手推相关公式

主要内容：复现了该课程中关键BP公式的推导、具体化了CELoss下的推导、对BPTT的推导做了复现和讨论

1. 通过一个RNN一个单元的input-output说明BP
   结构图：
   ![一个RNN单元示例](https://github.com/bigheary/dive_into_deeplearning/blob/main/RNN_cell.jpeg)
   推导结果：
   ![loss关于参数的导数推导](https://github.com/bigheary/dive_into_deeplearning/blob/main/RNNCell_Jw1w2.jpeg)
   
   以上， L关于O的导数，跟具体的loss function定义有关，下面以最常用的softmax + 交叉熵loss（CE loss）为例，来进行说明
   对O进行softmax变换之后，再计算CE loss
   ![softmax+celoss](https://github.com/bigheary/dive_into_deeplearning/blob/main/softmax%2Bceloss.jpeg)
   另外，可参考一种更加统一性的公式（来自网络）
    ![softmax+celoss_normed](https://github.com/bigheary/dive_into_deeplearning/blob/main/softmax%2Bceloss_norm.png)

2. BPTT原理说明
   即将RNN的计算图按照时间步展开，来计loss对各参数的梯度（因为参数对各个时间步是共享的）
   结构图：
   ![BPTT示例](https://github.com/bigheary/dive_into_deeplearning/blob/main/BPTT.jpeg)
   
   改图中有个地方值得商榷，即是否将总得loss拆分到具体每个时间步的loss。图中拆分到每个时间步下，导致后续的推导有问题（貌似是不能这拆分的，具体原因未知，可能前后有关联）
   ![BPTT-导数示例](https://github.com/bigheary/dive_into_deeplearning/blob/main/BPTT_daoshu.jpeg)
   ![BPTT-导数示例1](https://github.com/bigheary/dive_into_deeplearning/blob/main/BPTT_daoshu1.jpeg)
   ![BPTT-导数示例2](https://github.com/bigheary/dive_into_deeplearning/blob/main/BPTT_daoshu2.jpeg)
   
   总结，通过BPTT导数推导，可以认识到经典RNN架构容易出现梯度爆炸、梯度消失的原因，即BPTT-导数示例2中得到的递推公示所示，由于时间步的状态转移复用了变换矩阵Whh，在递推公示中体现为Whh的次幂形式，在时间步T较大时，越靠前的时间步的倒数计算会出现数值问题（爆炸or消失），体现在模型效果上就是无法距离较远的时间步的相互影响无法顺畅地流通。

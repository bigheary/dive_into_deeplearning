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

# 深度学习板块默认网页

# 训练踩坑

## 损失函数
![损失函数](https://github.com/ChinVision/Docs/raw/master/docs/media/loss.jpg)
因为取值是按次数取的，在batch结束后，没有将模型设置为训练模式。而取值又是随机的，所以训练才可以进行


## 验证集的loss小于训练集的loss
一般都是因为代码逻辑上的失误，导致这个结果
对应检查下面三种：
1. 查看结果的标签搞错了
2. 在训练中应用正则化，但在验证中未应用正则化
3. 训练loss是在每个epoch测量的，而验证loss是在每个epoch后测量的

可以适当降低Dropout或者其他正则化约束

# 记录比赛思路

1. 检测可以用U-net去做
2. domain adaptation可以用cyclegan的结合去做
3. 找其他比赛的思路



我的思路 

1. 首先对数据集进行增广

- 手术器械的分布非常不平衡；可通过data resampling 缓解
- 视频中有的帧有artifacts；可使用time filtering techniques缓解
- 不均匀的光照、运动模糊等问题可以通过数据增广得到很好的解决；
- 相邻帧使用的手术器械较为接近；
- 手术器械的使用通常遵循precedence rules，rarest tools通常在特别的事件中使用；
- 基于NASNet-A网络架构获得了top-performance

2. 使用关键点检测算法结合分割算法找到点的坐标
   1. 第一步，直线检测算法，找到粗略的点的位置
   2. 第二步，直接用Integrating spatial configuration into heatmap regression based CNNs for landmark localization的方法，之前唯一的疑惑就是点数不一样怎么办，现在初步思路就是直接预测大于所有点数量的heatmap，然后用算法筛选即可
   3. 参考代码 https://github.com/christianpayer



3. 使用cyclegan的方法做domain adaptation； 另外一个思路是用Domain Adversarial Training of Nerural Networks





# 作者介绍的思路

- 最关键的思想就是使用image-to-image translation
- 主要的挑战就是detect points of interest on these endoscopic images，传统的landmark可能不好使
- 寻找细胞检测的思路
- 用GAN和explicit density modeling by VAE





# 其他的比赛

- MICCAI 2019 VerSe 2019. 这个比赛也有定位，值得参考  https://zhuanlan.zhihu.com/p/90971011 

比赛地址：https://verse2019.grand-challenge.org

- MICCAI 2020 内窥镜图像分析 非常值得参考 https://zhuanlan.zhihu.com/p/120297988
- SurgVisDom - Surgical Visual Domain Adaptation 2020 刚好是一个domain adaptation的比赛https://surgvisdom.grand-challenge.org



![image-20210512174202466](https://cdn.jsdelivr.net/gh/nekomiao123/pic/img/image-20210512174202466.png)



## 比赛思路

1. 处理数据集

参考CATARACTS: Challenge on automatic tool annotation for cataRACT surgery这篇论文的总结部分，其中对内窥镜图像的的增广进行了详细的分析

2. 使用关键点检测算法找出关键点

参考一篇TMI的论文 Deep Learning-Based Regression and Classification for Automatic Landmark Localization in Medical Images

参考一篇MIA的论文 Integrating spatial configuration into heatmap regression based CNNs for landmark localization

还有之前VERSE比赛的关键点检测方法

3. 使用cyclegan做domain adaptation

参考之前比赛的结果 Surgical Visual Domain Adaptation: Results from the MICCAI 2020 SurgVisDom Challenge

参考ECCV论文 COCO-FUNIT: Few-Shot Unsupervised Image Translation with a Content Conditioned Style Encoder论文
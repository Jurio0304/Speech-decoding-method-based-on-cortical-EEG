# 题目：基于皮层脑电图的语音解码方法
## 原创性声明
## 摘要
* 研究目的及重要性：
* 研究的主要内容：
* 获得的基本结论、研究成果以及研究意义：
  * **基于LSTM的长短期记忆特性对于在时间序列数据分类、处理和预测的优越性，构建了基于LSTM的sEEG-Mel谱解码器；以及基于AutoEncoder这样一种无监督的数据维度压缩和数据特征表达方法，同时结合解码Mel谱的特征搭建了深度稀疏AutoEncoder作为Mel谱优化器。二者一起构成脑电-语音梅尔谱解码网络。**
  * **基于MelGAN在语音梅尔谱反演重建高质量语音上的优越表现[2]，在原始MelGAN架构基础上做了一定改进后将其作为语音梅尔谱-语音声码器网络。**
### 关键词：sEEG，语音解码，LSTM，AutoEncoder，MelGAN

## Abstract
### key words

## 目  录
## 1  绪论
* 1.1 背景及意义：
* 1.2 研究现状：
* 1.3 现存问题/研究难点：
* 1.4 本文的研究目标：
* 1.5 本文的组织结构
  * 第一章：**（概括绪论内容）**
  * 第二章：**（概括脑电-语音解码基础知识）**
  * 第三章：**（概括脑电-语音梅尔谱解码网络结构及实验）**
  * 第四章：**（概括MelGAN语音梅尔谱-语音声码器及实验）**
  * 第五章：**（总结展望）**

## 2  脑电-语音解码方法基础介绍
* 2.1 脑电信号（EEG）：**多种形式如sEEG，ECoG，LFP，spike等；基于文献对比差异，引出本研究采用脑电数据为sEEG并阐明该选择的原因**
* 2.2 音频梅尔谱：**介绍Mel谱的理论基础，可以作为音频特征的原理，以及基于文献说明Mel谱在音频信号处理中的地位和普适性**
* 2.3 脑电-语音解码的基础框架：**以2-3篇主要参考文献的解码框架为例，画出框架图进行讲解**
* 2.4 脑电-语音梅尔谱解码结果评估方法：
  * 2.4.1 传统评估方法：**基于Mel频段的Pearson相关系数。存在一定的局限性，对于时间轴上少数相关性差异巨大的时间箱样本感知能力较差，但这些“坏样本”对最终的语音重建又存在很大影响，如突然的转音或者较多的中断等**
  * 2.4.2 基于传统评估方法的改进方案：**在传统方法的基础上加入对基于时间箱样本的Pearson相关系数的考虑，![](https://latex.codecogs.com/svg.image?r=\lambda*r_{mel}&plus;(1-\lambda)*r_{time})，![](https://latex.codecogs.com/svg.image?\lambda\in[0,1])**
* 2.5 语音梅尔谱-语音重建结果评估方法：
  * 2.5.1 PSEQ：**评估语音质量高低的主要算法**
  * 2.5.2 ESTOI：**扩展短时客观可懂度（Extended short-time objective intelligibility）[3]，如今评估语音客观可懂度的主流算法**
* 2.6 本研究关于脑电-语音解码的整体框架（~~不确定这一节是否需要以及其位置是否合理~~）：**解码流程框图**
* 2.7 本章小结：

## 3  基于LSTM与AutoEncoder的脑电-语音梅尔谱解码网络
* 3.1 基于LSTM的脑电-语音梅尔谱谱解码器
  * 3.1.1 LSTM：
  * 3.1.2 解码器结构：
* 3.2 脑电-语音梅尔谱解码实验
  * 3.2.1 实验数据：**sEEG-荷兰语公开数据集[1]**
  * 3.2.2 实验设置：**包括sEEG和音频信号预处理方法和结果，实验设备详情**
  * 3.2.3 实验结果分析：**解码Mel谱的评估结果，与文献[1]结果进行对比**
* 3.3 基于AutoEncoder的语音梅尔谱优化器
  * 3.3.1 AutoEncoder：**传统AutoEncoder，Stack AutoEncoder，Sparse AutoEncoder**
  * 3.3.2 优化器结构：**基于SAE的Mel谱优化器，主要的栈式结构，兼具去噪、稀疏限制、Encoder输出维度限制等特性**
* 3.4 基于传统训练策略的语音梅尔谱优化实验
  * 3.4.1 实验数据：**解码器输出的预测Mel谱与其对应的原始Mel谱数据**
  * 3.4.2 传统训练策略：**传统训练策略来源于惯性思维**
  * 3.4.3 实验结果分析：**对该结果进行评估，并与解码器解码的结果进行对比得出结论，表明相关性几乎没有任何提升，且现存问题仍未得到解决**
* 3.5 基于改进训练策略的语音梅尔谱优化实验
  * 3.5.1 改进训练策略：**训练策略的改进方式、灵感来源、理论基础、定性分析、预测结果**
  * 3.5.2 实验结果分析：**评估结果，与解码器结果进行对比，得出改进训练策略的可行性与优越性，以及一定程度上解决了部分现存的问题，并且提供了一种高质量Mel谱优化器的可行性方案**
* 3.6 本章小结：

## 4  基于MelGAN的语音梅尔谱-语音声码器
* 4.1 生成对抗网络（GAN）：
* 4.2 MelGAN声码器：
* 4.3 实验
  * 4.3.1 实验数据：**sEEG-荷兰语公开数据集[1]中的音频数据训练网络，利用解码器和优化器得到的Mel谱结果进行测试**
  * 4.3.2 实验设置：**音频预处理，重要超参数设置，以及实验设备详情（实验室服务器）**
  * 4.3.3 实验结果分析：**基于PESQ、ESTOI等语音评估方法**
* 4.4 本章小结：

## 5  总结与展望
* 5.1 工作总结：
* 5.2 研究展望：

### 致谢
## 参考文献：
```
[1] Angrick, M., Ottenhoff, M.C., Diener, L. et al. Real-time synthesis of imagined speech processes from minimally invasive recordings of neural activity. Commun Biol  4, 1055 (2021). https://doi.org/10.1038/s42003-021-02578-0
[2] Kumar, Kundan Kumar, Rithesh de Boissiere. et al. MelGAN: Generative Adversarial Networks for Conditional Waveform Synthesis. arXiv:1910.06711
[3] J. Jensen and C. H. Taal, "An Algorithm for Predicting the Intelligibility of Speech Masked by Modulated Noise Maskers," in IEEE/ACM Transactions on Audio, Speech, and Language Processing, vol. 24, no. 11, pp. 2009-2022, Nov. 2016, doi: 10.1109/TASLP.2016.2585878.
```


# 大纲
## 原创性声明
## 摘要：
* 研究目的及重要性：**1-2句话介绍研究背景，包括国内外研究现状，主要是几篇主要期刊参考文献中关于语音解码脑机接口的现阶段进展以及存在的共性问题——基于EEG解码得到的Mel谱相关性不高，从而导致重建语音无法理解**
* 研究的主要内容：**提高基于sEEG解码得到Mel谱与真实Mel谱的相关性，探究解码出高质量可懂语音的可行性**
* 获得的基本结论、研究成果以及研究意义：
  * **基于LSTM的长短期记忆特性对于在时间序列数据分类、处理和预测的优越性，构建了基于LSTM的sEEG-Mel谱解码器网络。利用该解码器网络对“sEEG-荷兰语公开数据集”[1]进行了Mel谱解码的十折交叉验证测试，基于Mel谱频段的Pearson相关系数评估结果相较于原文献有较大的提升（原文献：r=0.62±0.15，LSTM结果：r=0.73）**
  * **基于AutoEncoder这样一种无监督的数据维度压缩和数据特征表达方法，同时结合解码Mel谱的特征搭建了深度稀疏AutoEncoder作为Mel谱优化器网络。依据解码Mel谱与真实Mel谱之间在时间轴上相关性波动起伏大且存在不连续问题，而二者在Mel频段上相关性较高且非常稳定的直观表现和特点，在优化器的训练中提出了一种新的训练策略——以Mel谱频段为样本，单个音频的Mel谱时间箱为特征进行训练，解决了传统训练策略下优化器无法学习到Mel谱重要特征而一直处于欠拟合状态的难题，同时一定程度上进一步提高了解码Mel谱的相关性，为端到端EEG-高质量Mel谱的解码网络提供了一定理论和实践上的指导意义**
  * **基于MelGAN在Mel谱反演重建高质量语音上的优越表现[2]，在原始MelGAN架构基础上做了一定改进后将其作为Mel谱-语音声码器网络。在荷兰语单词数据集上经过较大批量的训练后，该声码器模型可以从高质量Mel谱图中反演重建出可以理解的高质量音频，（ESTOI和PESQ评估结果···），并在优化器过拟合后的训练集输出Mel谱结果上得到验证。该普适、高效的声码器网络有望与前面提到的EEG-高质量Mel谱解码网络结合构成端到端的EEG-高质量语音的解码网络**
### 关键词：**sEEG，语音解码，LSTM，AutoEncoder，MelGAN**
## Abstract
### key words
## 目  录
## 1  绪论：
* 1.1 背景及意义：**（1-2段）脑机接口系统发展背景引出语音脑机接口系统，而作为语音脑机接口系统的技术核心——脑电-语音解码算法的开发研究尤为重要**
* 1.2 研究现状：**（2-3段）简要介绍3-5篇国外关于脑电-语音解码算法上的研究，并对其基于数据形式、核心算法、结果与评估方法以及最终结论进行列表比较**
* 1.3 现存问题/研究难点：**总结目前国内外研究现状，肯定现有成果，列出目前脑电-语音解码系统的共性问题——作为语音解码中间介质的Mel谱的解码相关性较低，导致重建语音尚无法理解**
* 1.4 本文的研究目标：**以提升脑电-语音解码系统解码语音的质量与可懂度为出发点和主要目标，分别从构建脑电-Mel谱解码器、解码Mel谱优化器和Mel谱反演重建高质量音频声码器三个方面进行研究**
* 1.5 本文的组织结构：
  * 第一章：**（概括绪论内容）**
  * 第二章：**构建了基于LSTM的sEEG-Mel谱解码器网络，经过一定条件下的实验得出结果，以及与原文献结果进行对比，得出该解码器在解码问题上的有效性且提升了一部分的性能**
  * 第三章：**构建了基于AutoEncoder的Mel谱优化器网络，经过一定条件下的实验得出结果，分别与原文献和解码器结果进行对比，得出优化器相比于二者均有一定程度上的性能提升，且为EEG-高质量Mel谱的端到端网络提供解决思路**
  * 第四章：**基于MelGAN训练得到一个部分荷兰语单词的Mel谱-语音声码器，在语音重建上取得较好效果，同时可以作为EEG-高质量语音解码系统中的重要一环提供高质量Mel谱-高质量语音重建的解决方案**
## 2  基于LSTM的sEEG-Mel谱解码器：
* 2.1 LSTM：**LSTM架构、特点、适用问题情境，以及在sEEG-Mel谱解码中的可行性**
* 2.2 解码器结构：**基于LSTM的解码器架构，重要参数设置以及根据等**
* 2.3 实验：
    * 2.3.1 实验数据：**sEEG-荷兰语公开数据集[1]**
    * 2.3.2 实验设置：**包括sEEG和音频信号预处理方法和结果，实验设备详情**
    * 2.3.3 实验结果分析：**解码Mel谱的评估结果，与文献[1]结果进行对比，说明解码性能提升较为明显。分析解码Mel性能提升原因，已经仍然存在的整体相关性不高以及细节上Mel谱频率轴断带、时间轴不连续等问题，并提出一定的解决思路或方案**
* 2.4 本章小结：**（1-2段）总结本章内容，总结实验结果、分析与结论，表明改进方向，为优化器做铺垫**

## 3  基于AutoEncoder的Mel谱优化器：
* 3.1 AutoEncoder：
    * 3.1.1 传统AutoEncoder：**结构、特点、功能、适用问题**
    * 3.1.2 Stack AutoEncoder：**深度/栈式自编码器结构、特点**
    * 3.1.3 Sparse AutoEncoder：**稀疏自编码器结构、特点**

* 3.2 优化器结构：**基于SAE的Mel谱优化器，主要的栈式结构，兼具去噪、稀疏限制、Encoder输出维度限制等特性**
* 3.3 基于传统训练策略的实验：
    * 3.3.1 实验数据：**解码器输出的预测Mel谱与其对应的原始Mel谱数据**
    * 3.3.2 实验设置：**传统训练策略作为baseline，以供后续改进策略进行比较。**
    * 3.3.3 实验结果分析：**对该baseline结果进行评估，与解码器解码的结果进行对比得出结论，表明相关性几乎没有任何提升，且现存问题仍未得到解决**

* 3.4 基于改进训练策略的实验：
    * 3.4.1 改进训练策略：**训练策略的改进方式、灵感来源、理论基础、定性分析预测**
    * 3.4.2 实验结果分析：**对改进训练策略后的优化器结果进行评估，与解码器结果进行对比，得出改进训练策略的可行性与优越性，以及一定程度上解决了部分现存的问题，并且提供了一种高质量Mel谱优化器的可行性方案**

* 3.5 本章小结：**（1-3段）总结本章内容，，总结实验结果、分析与结论，思考改进方向以及其他理论上存在可行性的训练策略，与前一章内容结合讨论表明为端到端EEG-高质量Mel谱的解码网络提供了一定理论和实践上的指导意义**

## 4  基于MelGAN的Mel谱-语音声码器
* 4.1 GAN：**GAN的基本架构，特点，功能，应用前景**
* 4.2 MelGAN：**MelGAN的架构，特点，以证明在高质量Mel谱上重建高质量音频的可行性与其相比于传统声码器如GriffinLim算法等具有更加优越的性能**
* 4.3 实验：
    * 4.3.1 实验数据：**sEEG-荷兰语公开数据集[1]中的音频数据训练网络，利用解码器和优化器得到的Mel谱结果进行测试**
    * 4.3.2 实验设置：**音频预处理，重要超参数设置，以及实验设备详情（实验室服务器）**
    * 4.3.3 实验结果分析：**基于PESQ、ESTOI等语音评估方法对重建音频的质量以及客观可懂度进行评估，阐明性能不太好的主要原因（参数、训练时长）。同时测试解码器和优化器二者得到的Mel谱重建音频的可行性**


## 5  Mel谱和语音解码结果的评估方法（位置：不清楚是放在绪论里，还是在第2/3/4章里分别提到，还是单独作为一章比较好）
* 5.1 Mel谱解码结果评估方法：
  * 5.1.1 传统评估方法：**基于Mel频段的Pearson相关系数。存在一定的局限性，对于时间轴上少数相关性差异巨大的时间箱样本感知能力较差，但这些“坏样本”对最终的语音重建又存在很大影响，如突然的转音或者较多的中断等**
  * 5.1.2 评估方法的改进方案：**在传统方法的基础上加入对基于时间箱样本的Pearson相关系数的考虑，r = \lambda \ast r_{mel} + (1-\lambda) \ast r_{time}, \lambda \in [0, 1]**

* 5.2 语音重建结果评估方法：
  * 5.2.1 PSEQ：**作为评估语音质量高低的主要算法，PESQ(Perceptual Evaluation of Speech Quality)将两个待比较的语音信号经过电平调整、输入滤波器滤波、时间对准和补偿、听觉变换之后, 分别提取两路信号的参数, 综合其时频特性, 得到PESQ分数, 最终将这个分数映射到主观平均意见分(MOS)。PESQ得分范围在-0.5~4.5之间，得分越高表示语音质量越好**
  * 5.2.2 ESTOI：**扩展短时客观可懂度（Extended short-time objective intelligibility），在384ms分析窗口内对子带信号时间包络进行分析，依赖于STOI所做的加性可理解性跨频率假设，计算频谱相关系数，然后在384ms内对时间进行平均，这使ESTOI 能够更好地捕捉时间调制噪声掩蔽器的效果，其中通常保留“在下降”中的频谱相关性，特别地适用于STOI表现较差的高度波动的加性噪声源。ESTOI在近几年语音解码研究中多次作为主要语音评估方法应用在结果评估中。ESTOI得分在-1~1之间，得分越高表明语音可懂度越高**


### 致谢
## 参考文献：
```
[1] Angrick, M., Ottenhoff, M.C., Diener, L. et al. Real-time synthesis of imagined speech processes from minimally invasive recordings of neural activity. Commun Biol  4, 1055 (2021). https://doi.org/10.1038/s42003-021-02578-0
[2]Kumar, Kundan Kumar, Rithesh de Boissiere. et al. MelGAN: Generative Adversarial Networks for Conditional Waveform Synthesis. arXiv:1910.06711
```
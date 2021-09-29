# MobileNet
* MobileNet特性--小型，低延遲，低功耗
    1. 較小的模型，引數數量更少
    2. 較低的複雜度，運算中乘法和加法更少
* 使用深度可分離卷積來建構輕量級深度神經網路
## 深度可分離卷積
* 可分為: 深度卷積(depthwise  convolution)、逐點卷積(pointwise convolution)

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/1.png)

* 深度卷積--將卷積核拆分成單通道形式，在不改變輸入特徵影象的深度的情況下，對每一通道進行卷積操作，就會得到和輸入特徵圖通道數一致的輸出特徵圖

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/3.png)

* 逐點卷積--就是1*1卷積，主要作用就是對特徵圖進行升維和降維

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/4.png)

* 標準卷積與深度可分離卷積的過程對比:

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/5.png)

* 深度可分離卷積夠讓用更少的引數，更少的運算，達到差不多的結果

### 引數量與計算量差異
* 標準卷積的引數量與計算量

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/6.png)

* 深度可分離卷積的引數量與計算量

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/12.png)

* 對比

![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/7.png)

## MobileNet V1
* MobileNet v1 的網路結構如下圖所示。除了第一層使用一般的卷積層，剩下的卷積層都是使用 Depthwise Separable Convolution
![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/11.png)
![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/8.png)

* 雖然MobileNet網路結構和延遲已經比較小了，但是很多時候在特定應用下還是需要更小更快的模型，為此引入了寬度因子alpha，為了控制模型大小，引入了分辨因子rho
* 寬度因子 alpha (Width Mutiplier)，在每一層的輸入輸出通道進行縮減，原本的輸入通道從 M 變為 alpha x M，輸出通道從 N 變為 alpha x N，變換後的計算量為
![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/9.png)
* alpha 介於 (0, 1] 區間，典型的設定值為 1, 0.75, 0.5, 0.25，可以使計算量和參數量降低 (alpha)**2 倍

* 分辨率因子 (Resolution Multiplier)，用來控制輸入圖像的分辨率，也就是說 Rho 越小、輸入圖像就越小，變換後的計算量為
![PICTURE](https://github.com/victor0520/MyNote/blob/main/%E5%B0%88%E9%A1%8C/bitmap/10.png)
* Rho 介於 (0, 1] 區間，典型的設定值為 224、192、160、128，可以使計算量降低 (alpha)**2 x ρ x ρ 倍

# 參考資料
* [卷積神經網路學習筆記——輕量化網路MobileNet系列（V1，V2，V3）](https://www.gushiciku.cn/pl/gxFx/zh-tw)
* [MobileNetV1 論文閱讀](https://medium.com/ching-i/mobilenetv1-%E8%AB%96%E6%96%87%E9%96%B1%E8%AE%80-1e7568096e8b)
* [深度学习论文翻译解析（十七）：MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications](https://www.cnblogs.com/wj-1314/p/14318311.html)
# 第4讲课后作业
## 1. 随机产生100个候选视频，有对应的embedding和相关分s。产生8个DPP打散后的结果。
见[作业](https://github.com/GGsimidaRazer/TikTok-summer-school/blob/main/%E7%AC%AC%E5%9B%9B%E8%AE%B2%E8%AF%BE%E5%90%8E%E4%BD%9C%E4%B8%9A.ipynb)
## 2. 实现DPP greedy search算法
见[作业](https://github.com/GGsimidaRazer/TikTok-summer-school/blob/main/%E7%AC%AC%E5%9B%9B%E8%AE%B2%E8%AF%BE%E5%90%8E%E4%BD%9C%E4%B8%9A.ipynb)
## 3. 实现DPP beam search 算法
见[作业](https://github.com/GGsimidaRazer/TikTok-summer-school/blob/main/%E7%AC%AC%E5%9B%9B%E8%AE%B2%E8%AF%BE%E5%90%8E%E4%BD%9C%E4%B8%9A.ipynb)
## 4. 重复1w次模拟实验比较不同beam size下beam search算法和greedy算法的异同（统计计算复杂度，准确度）。
  首先对于算法复杂度，可以直接计算 greedy search 在DPP计算中的时间复杂度为$O(MN^2)$，其中$N$表示返回的物品数量，$M$表示总物品数量，显然这是因为在初始化时需要遍历整个物品集合，并在之后取出物品时进行$N^2$次遍历。而对于 beam Search ,可以推算出在 greedy search 的基础上需要对物品进行$B$次比对($B$表示 BeamSize 束的大小)，并从所有结果中取出前$B$个结果，因此时间复杂度总计为$O(BMN^2log(B))$。而空间复杂度上由于 beam search 需要维护$B$个信息表，因此空间复杂度是 greedy search 的$B$倍。
根据[时间统计结果](https://github.com/GGsimidaRazer/TikTok-summer-school/blob/main/times100.csv)(其中 Beamsize 束的大小由1到10，每次取20个结果，重复进行100次)也可以看出，随着束的大小的上升运行时间也随其线性上升。理论上当束大小为1时其算法复杂度与 greedy search 等价，但在实际运行中 beam search 的运算时间要稍久一些，认为可能是在计算中 beam search 需要额外进行一次条件概率的计算以及对额外信息的维护导致时间稍久一些。  
<img src="https://github.com/GGsimidaRazer/TikTok-summer-school/blob/main/fig.png?raw=true" width=48> ![多次实验的运行时间](https://github.com/GGsimidaRazer/TikTok-summer-school/blob/main/pic1.png?raw=true)  
  对于准确度，首先可以认为 BeamSize 为1时其与 greedy search 等价，实验结果可以验证这一点。而随着 BeamSize 的增大，在最初几个打散结果取值往往会产生差异，但是随着候选物品的减少， greedy search 与 beam Search 逐渐收敛到同一物品集。根据理论推导， beam Search 实际上是对 greedy search 的一定程度的改进，可以考虑到多个候选，放宽了选择门槛，可以更多地考虑全局信息，因此 beam Search 的准确度应当更高。  

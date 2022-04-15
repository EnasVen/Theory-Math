我們將以線代和統計學的觀點來解析PCA的原理：  
# 線性代數觀點 - Part1  
下圖是線性代數內二維向量投影的基本資訊，而PCA做的正是找出最大變異的投影向量!  
  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/PCA/PCA_img01.png)  
我們可以很清楚看到資料點X1與X2投影在V1與V2會得到不同的變異量，很明顯地，藍色的投影所得變異更大。  
  
# 線性代數觀點 - Part2  
假設我們有:  
n個觀察值：<img src="https://latex.codecogs.com/gif.image?\dpi{110}x_{1}...x_{n}" title="https://latex.codecogs.com/gif.image?\dpi{110}x_{1}...x_{n}" />  
m個特徵維度：<img src="https://latex.codecogs.com/gif.image?\dpi{110}x_{i}=\begin{bmatrix}x_{i1}...x_{im}\end{bmatrix}" title="https://latex.codecogs.com/gif.image?\dpi{110}x_{i}=\begin{bmatrix}x_{i1}...x_{im}\end{bmatrix}" />  
欲最大化投影後的變異量，我們需要計算每一筆資料的投影點:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\left\|x_{i}&space;\right\|*cos(\theta&space;)=\left\|x_{i}&space;\right\|*\frac{\left<x_{i},v\right>}{\left\|x_{i}&space;\right\|\left\|v&space;\right\|}=\frac{\left<x_{i},v\right>}{\left\|v&space;\right\|}" />  
  
當v是單位向量時，我們得到投影點為:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\left<x_{i},v\right>"/>
  
假設各特徵已scale過，也就是平均為0；我們可以得到總變異為: <img src="https://latex.codecogs.com/svg.image?\sum=\frac{1}{n}\sum_{i=1}^{n}(v^{T}x_{i})(v^{T}x_{i})^{T}=\frac{1}{n}\sum_{i=1}^{n}v^{T}x_{i}x_{i}^{T}v=v^{T}(\frac{1}{n}\sum_{i=1}^{n}x_{i}x_{i}^{T})v=v^{T}Cov_{x}v" />  
  
而我們要做的就是找到一個v使得總變異最大!用數學來說就是:  
<img src="https://latex.codecogs.com/svg.image?v=\underset{\left\|v\right\|=1,v\in&space;\mathbb{R}^{m}}{argmax}v^{T}Cov_{x}v" />  



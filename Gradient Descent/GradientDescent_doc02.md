梯度下降的方法，常見的有6種，各自介紹如下:  

# Vanilla Gradient Descent
最基礎的Gradient Descent，形式如上一份markdown文件所述:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;w_{t&plus;1}&space;=&space;w_t&space;-&space;\eta_t&space;*&space;g_t&space;\;&space;,&space;\;&space;where&space;\;&space;g_t&space;=&space;\frac{\partial&space;L}{\partial&space;w}"/>

# Adaptive Gradient Descent
學習率會隨著時間逐漸減小，且當前梯度會參考過去歷史梯度。  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;w_{t&plus;1}&space;=&space;w_t&space;-&space;\eta_t&space;*&space;\frac{g_t&space;}{\sigma_t}\;&space;,&space;\;&space;where&space;\;&space;\sigma_t&space;=&space;\sqrt{\frac{\sum_{i=1}^{t-1}g_i^2}{t&plus;1}}&space;\;&space;,&space;\eta_t&space;=&space;\frac{\eta}{\sqrt{t&plus;1}&space;"/>

# Stochastic Gradient Descent (SGD)
不同於傳統梯度下降，傳統梯度下降使用所有訓練樣本進行；而SGD就是一次跑1個樣本或mini-batch後計算單次梯度或是mini-batch梯度的平均後就更新一次參數。  
樣本或mini-batch是隨機抽取的，所以才會稱為隨機梯度下降法!  

# RMA Prop
為了解決error surface太過複雜，導致傳統梯度下降收斂太慢，學習率更新太慢而新增的方法。  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;w_{t&plus;1}&space;=&space;w_t&space;-&space;g_t&space;*&space;\frac{\eta}{\sigma_t}\;&space;,&space;\;&space;where&space;\;&space;\sigma_t&space;=&space;\sqrt{\alpha&space;(\sigma_{t-1})^2&plus;(1-\alpha)(g_t)^2}&space;\;&space;,&space;\sigma_0&space;=&space;g_0&space;" title="w_{t+1} = w_t - g_t * \frac{\eta}{\sigma_t}\; , \; where \; \sigma_t = \sqrt{\alpha (\sigma_{t-1})^2+(1-\alpha)(g_t)^2} \; , \sigma_0 = g_0 " />

注意到當前sigma值為上一期的sigma平方與當前梯度平方的線性組合!  

# Momentum
類似物理慣性現象，套用到梯度下降的參數更新模式。  
下圖綠色線條為前次參數更新方向，在參考負梯度方向後，將兩向量進行加法得到新的參數更新方向!  
由於考慮了前次參數更新方向，此行為類似物理的慣性運動，因此被稱為Momentum。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Gradient%20Descent/Momentum.png)

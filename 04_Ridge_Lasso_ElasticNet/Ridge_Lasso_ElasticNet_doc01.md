# 共線性  
在模型中，當資料變數 (e.g.血氧濃度、PM2.5數值、國民GDP…等等) 之間具有高度相關時，即為共線性。  
在多元迴歸之中，變數之間過高的相關性將會使估計參數的variance變大，並且使迴歸係數無法精確估計，進而影響模型在解釋以及計算信賴區間上的困難。  
  
# VIF(變異數膨脹因子)  
VIF值用來偵測共線性是否存在於變數之間，其定義為:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}VIF_{j}=\frac{1}{1-R_{j}^2}" />  
其中Rj代表使用第j個變數作為Y，其餘變數作為X所得的R-square。  
通常VIF值超過4，我們會認為存在共線性問題，值越大，共線性問題越嚴重!  
  
# 正則化(Regularization)  
在訓練資料過少或模型overtraining的時候，容易產生過度配適的現象(overfitting)。  
為了抑制overfitting，我們會在模型加入懲罰項(penalty)來避免模型在訓練資料表現良好；在測試資料卻有極大的誤差。  
(例如:評估模型的AIC & BIC指標即使用了penalty的概念；AIC = -2 ln(L) + 2k)  
  
下圖即為過擬和的結果是意圖:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Ridge_Lasso_ElasticNet/Regularization01.png)  
  
# L2 - Regularization  
在cost function後面加上平方和懲罰項即為L2-Regularization的作法:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}C&space;=&space;C_{0}&plus;\frac{\lambda&space;}{2n}\sum_{\omega&space;}^{}\omega&space;^2" />  
  
我們將上式對參數微分可以得到以下:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\frac{\partial&space;C}{\partial&space;w}=\frac{\partial&space;C_0}{\partial&space;w}&plus;\frac{\lambda&space;}{n}w"/>  
  
w參數更新過程可以寫成:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}w&space;\rightarrow&space;w-\eta&space;\frac{\partial&space;C_0}{\partial&space;w}-\frac{\eta&space;\lambda&space;}{n}w=(1-\frac{\lambda}{n})w-\eta&space;\frac{\partial&space;C_0}{\partial&space;w}" />  
  
在過擬合的模型內，參數係數通常都會特別大，可直觀理解為fit函數必須在極小的區間內擬合每一個資料點，因此w必須非常大。  
  
# L1 - Regularization  
在cost function後面加上絕對值懲罰項即為L1-Regularization的作法:    
<img src="https://latex.codecogs.com/gif.image?\dpi{110}C=C_0&plus;\frac{\lambda&space;}{n}\sum_{w}^{}\left|w&space;\right|" />  
  
我們將上式對參數微分可以得到以下:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\frac{\partial&space;C}{\partial&space;w}=\frac{\partial&space;C_0}{\partial&space;w}&plus;\frac{\lambda&space;}{n}sgn(w)" />  
  
w參數更新過程可以寫成:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}w\to&space;w-\frac{\eta&space;\lambda&space;}{n}sgn(w)-\eta&space;\frac{\partial&space;C_0}{\partial&space;w}" />  
  
L1正則化的效果可以把參數往0點縮減，如下圖:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Ridge_Lasso_ElasticNet/Regularization02.png)  
  

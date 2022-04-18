有了正則化的基本認識，以下將列出三種線性迴歸模型的重點特性:  
  
# Ridge Regression  
1.加入L2-Regualrization使迴歸係數收縮 => 迴歸係數數值變小，但不會快速收斂至0(無變數選擇功能)  
2.計算公式較L1-Regularization簡易，可得解析解    
3.以增大參數估計量的bias為代價，換取較小的variance(如下圖，後面會有數學解釋來證明這個說法!)  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Ridge_Lasso_ElasticNet/Regularization03.png)    
  
Ridge的數學式子如下:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\hat{\beta&space;}_{Ridge}=\underset{\beta&space;}{arg&space;min}\sum_{i=1}^{N}(y_i-\beta_0-\sum_{j=1}^{p}x_{ij}\beta&space;_j)^2" />  
同時必須滿足:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\sum_{i=1}^{p}(\beta_j)^{2}\leq&space;t" />  
用直白的話語來說，就是找到一個beta參數使得Loss Function達到最小。  
有了限制式，尋找極值的方法便可使用Lagrange Multiplier來做。  
  
# Lasso Regression(Least Absolute Shrinkage and Selection Operator)  
1.加入L2-Regualrization使迴歸係數收縮 => 迴歸係數數值快速收斂至0(有變數選擇功能)  
2.相對於L2，無法透過微分得到解析解。
3.sparsity特性可以加速運算效率!
  
Lasso的數學式子和Ridge類似，差別只在限制式不同:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\sum_{i=1}^{p}\left|\beta_j&space;\right|\leq&space;t"  />  
由於絕對值無法微分，計算上會比較複雜。  
  
# Elastic Net  
1.同時具備消除共線性以及變數選擇能力。  
2.同時具備Ridge預測結果穩定性以及Lasso的快速運算效率。  
  
Elastic Net其實就是綜合Ridge與Lasso的混合方法，它的數學式如下:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\beta&space;\hat{\beta}_{elastic}=\underset{\beta&space;}{argmin}(&space;\left\|y-X\beta&space;\right\|^2&space;&plus;&space;\lambda(&space;(1-\alpha)\left\|\beta&space;\right\|^2&plus;\alpha\left\|\beta&space;\right\|_1&space;)&space;)"  />  
  
等於是把L1與L2懲罰項做一個線性組合!  
將L1,L2與Elastic Net在圖形上做比較:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Ridge_Lasso_ElasticNet/Regularization06.png)   

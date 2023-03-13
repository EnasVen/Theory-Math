# 參數更新
在這一章節內，我們會推導Logistic Regression內如何使用gradient descent去更新參數!  

首先recall一下logistic regression的結果:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}ln\frac{P(Y=1|x,\omega)}{P(Y=0|x,\omega)}=ln\frac{p}{1-p}=\omega^{T}x&space;\\\Rightarrow&space;p=\frac{1}{1&plus;e^{-\omega^Tx}}&space;"  />  

我們可以把 general形式如下表達:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(y|x,\omega)=f(x,\omega)^y(1-f(x,\omega))^{1-y}&space;\&space;\&space;where&space;\&space;f(x,\omega)=P(Y=1|x,\omega)=p&space;" />  

假設數據有n筆資料，那麼log-liklihood可得:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}L=p(y|\mathbf{x},\omega)=\prod_{i=1}^{n}p(y_i|x_i,\omega)=\prod_{i=1}^{n}f(x_i,\omega)^{y_i}(1-f(x_i,\omega))^{1-y_i}" />  

取ln，相乘轉相加:  

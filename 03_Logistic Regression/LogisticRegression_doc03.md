# 參數更新
在這一章節內，我們會推導Logistic Regression內如何使用gradient descent去更新參數!  

首先recall一下logistic regression的結果:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}ln\frac{P(Y=1|x,\omega)}{P(Y=0|x,\omega)}=ln\frac{p}{1-p}=\omega^{T}x&space;\\\Rightarrow&space;p=\frac{1}{1&plus;e^{-\omega^Tx}}&space;"  />  

我們可以把 general形式如下表達:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(y|x,\omega)=f(x,\omega)^y(1-f(x,\omega))^{1-y}&space;\&space;\&space;where&space;\&space;f(x,\omega)=P(Y=1|x,\omega)=p&space;" />  

假設數據有n筆資料，那麼log-liklihood可得:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}L=p(y|\mathbf{x},\omega)=\prod_{i=1}^{n}p(y_i|x_i,\omega)=\prod_{i=1}^{n}f(x_i,\omega)^{y_i}(1-f(x_i,\omega))^{1-y_i}" />  

取ln，相乘轉相加:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\\&space;ln(w)\\&space;=lnL\\=\sum_{i=1}^{n}y_i&space;lnf(x_i,\omega)&plus;(1-y_i)ln(1-f(x_i,\omega))\\=\sum_{i=1}^{n}y_i&space;lnf(x_i,\omega)-y_i&space;ln(1-f(x_i,\omega))&plus;ln(1-f(x_i,\omega))\\=\sum_{i=1}^{n}y_i&space;ln(\frac{lnf(x_i,\omega)}{1-lnf(x_i,\omega)})&plus;ln(1-f(x_i,\omega))\\=\sum_{i=1}^{n}y_i&space;\omega^Tx_i&plus;ln(1-f(x_i,\omega))&space;&space;&space;\\=\sum_{i=1}^{n}y_i&space;\omega^Tx_i-ln(1&plus;e^{\omega^Tx_i})&space;" />  

由於我們要做loss的minimize，所以將上式加上負號並取平均(因為有n個樣本):  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}ln(w)=\frac{-1}{n}\sum_{i=1}^{n}&space;\left&space;[&space;y_i&space;\omega^Tx_i-ln(1&plus;e^{\omega^Tx_i})&space;\right&space;]" />  

接著對w的分量偏微:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\frac{\partial&space;l(\omega)}{\partial&space;\omega_j}&space;\\&space;=&space;\frac{-1}{n}\sum_{i=1}^{n}y_ix_{ij}-\frac{1}{1&plus;e^{\omega^Tx_i}}e^{\omega^Tx_i}x_ij&space;\\=&space;\frac{-1}{n}\sum_{i=1}^{n}\left&space;[&space;y_i-f(x_i,\omega)&space;\right&space;]x_ij&space;" />  

上式即為gradient descent的下降量!

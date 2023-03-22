# 迴歸係數估計
對於每一個beta，我們要怎麼去估計它的值呢?  
答案就是利用最小平方法(OLS)進行估計!  

首先我們知道在樣本迴歸線中，epsilon代表殘差，那麼讓殘差盡可能的小，就是OLS的精神了:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_i=\hat{\beta_0}&plus;\hat{\beta_1}x_1&plus;...&plus;\hat{\beta_p}x_p&plus;\varepsilon_i&space;\\\Rightarrow&space;L=\sum_{i=1}^{n}&space;(y_i-\hat{y_i})^2" />  
在進行偏微分之前，我們要先改寫一下原式，我們知道每一個y都可以被表示成x和beta的線性組合再加殘差，那麼寫成向量就會是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Y=\begin{pmatrix}y_1&space;\\...&space;\\y_n\end{pmatrix}" />  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}x_{i}^{'}=(1,&space;x_{i1},&space;x_{i2},&space;...&space;,&space;x_{ip})&space;\\\Rightarrow&space;X=\begin{pmatrix}x_{1}^{'}&space;\\...&space;\\x_{n}^{'}\end{pmatrix}&space;" />  
而一個y就會對應一個epsilon，也可以用向量表示:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\varepsilon&space;=\begin{pmatrix}\varepsilon_1&space;\\...&space;\\\varepsilon_n\end{pmatrix}&space;" />  
與x對應的beta也可以用向量表示:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\beta&space;&space;=\begin{pmatrix}\beta_0&space;\\...&space;\\\beta_p\end{pmatrix}&space;" />  

注意一下beta是從0開始到p結束!(有p個feature)  

因此整個多元線性回歸模型可以用矩陣型態來表示:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Y_{n&space;\cdot&space;&space;1}=X_{n&space;\cdot&space;&space;(p&plus;1)}\beta_{(p&plus;1)&space;\cdot&space;&space;1}&space;&plus;&space;\varepsilon_{n&space;\cdot&space;&space;1}&space;" />  
底下特別標註矩陣的維度，方便理解。  

有了這個表示法，原先的Loss就可以很輕鬆地用矩陣來表達:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}L=(Y-X\beta)^{'}(Y-X\beta)&space;" />  
接著我們對beta進行向量微分就能得到beta估計量:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\frac{\partial&space;L}{\partial&space;\beta&space;}\\=&space;\frac{\partial&space;}{\partial&space;\beta&space;}(y'y-y'X\beta&space;-\beta'X'y&plus;\beta'X'X\beta&space;)\\=\frac{\partial&space;}{\partial&space;\beta&space;}(y'y-2y'X\beta&space;&plus;&space;\beta'X'X\beta)\\&space;=-2X'y\beta&space;&plus;&space;2X'X\beta&space;\\\Rightarrow&space;\hat{\beta}=&space;(X'X)^{-1}X'y" />  

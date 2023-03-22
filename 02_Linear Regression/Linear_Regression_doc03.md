# 估計量的抽樣分布
在理論假設下(epsilon為iid常態)，我們將推導每一個參數估計量之抽樣分布。  
在殘差常態假設下，我們可以推得y的分布也是常態:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\varepsilon_1...\varepsilon_n&space;\overset{iid}{\sim&space;}&space;N(0,\sigma^2)&space;\\i.e.&space;\&space;\varepsilon&space;\sim&space;&space;N(O_{n&space;\cdot&space;n},\sigma^2I_{n&space;\cdot&space;n})&space;" />  

而y|X這個常態分佈的mean和variance寫成矩陣形式就會是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_i|x_i\sim&space;N(x_{i}'\beta&space;,&space;\sigma^2)&space;\\\Rightarrow&space;E(y|X)=X\beta&space;\&space;&space;;&space;\&space;Cov(y|X)=\sigma^2&space;I_{n&space;\cdot&space;n}" />  

這時候我們可推導出beta的分布也會是常態:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\\\because&space;\hat{\beta}=(X'X)^{-1}X'y&space;\\\therefore&space;\hat{\beta}&space;\sim&space;Normal&space;\&space;Distribution" />  
理由是beta hat為y的線性組合，而y又是常態分布，因此根據機率論，我們知道常態隨機變數的線性組合仍然還是常態!  
這時候我們剩下的就是求出mean和covariance，找到後就能確定它的分布。  

首先是mean，從下面的結果我們知道beta估計量(也就是beta hat)是不偏的(unbiased):  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E(\hat{\beta})=(X'X)^{-1}X'E(y)=(X'X)^{-1}X'X\beta&space;=\beta&space;" />  

接著是covariance矩陣，利用到Cov(a+BZ)=BCov(Z)B'的性質:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Cov(\hat{\beta&space;})=(X'X)^{-1}X'Cov(y)((X'X)^{-1}X')'=\sigma^2(X'X)^{-1}" />  

綜合以上，我們得到beta的分布為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\hat{\beta}&space;\sim&space;N_{p&plus;1}(\beta,&space;\sigma^2(X'X)^{-1})" />  

注意到下標我加上了p+1，代表這是p+1維的random vector。(因為feature有p+1個!)  

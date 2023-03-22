# 估計量的抽樣分布 : beta
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

# 估計量的抽樣分布 : sigma平方 
雖然模型內的beta參數我們成功地找到其估計量與對應的抽樣分布。  
但模型內仍然還有一個未知參數待估計: sigma平方，也就是原先的殘差假設內常態分布的variance!  
要估計sigma平方，我們先給出最終的定義式:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Let&space;\&space;e&space;=&space;y&space;-&space;X&space;\hat{\beta&space;}&space;\\&space;\Rightarrow&space;\hat{\sigma}^2=\frac{n-(p&plus;1)}{1}e'e=&space;\frac{n-(p&plus;1)}{1}\sum(y_i-x_i\hat{\beta})^2" />  

同樣的我們可以證明sigma平方hat在取期望值後仍然是不偏的(unbiased):  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E(\hat{\sigma}^2)=E(\frac{e'e}{n-(p&plus;1)})&space;\\\because&space;e&space;\\&space;=y-X\hat{\beta}&space;\\&space;=y-X(X'X)^{-1}X'y&space;\\=(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')(X\beta&space;&plus;\varepsilon)&space;\\=(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')\varepsilon&space;&space;\\\therefore&space;E(e'e)&space;\\&space;=tr(E(e'e))\\&space;=E(tr(e'e))\\&space;=&space;E&space;tr(\varepsilon'(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X'))\varepsilon)&space;\\&space;=&space;tr(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X'))E(\varepsilon&space;\varepsilon')&space;\\=&space;\sigma^2&space;tr(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X'))"/>  
tr裡面那一包矩陣可以各自拆解(trace運算有linearity):  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sigma^2&space;\left&space;(&space;tr(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X'))&space;\right&space;)&space;\\=\sigma^2&space;\left&space;(&space;tr(I_{n&space;\cdot&space;n})&space;-&space;tr(X(X'X)^{-1}X')&space;\right&space;)&space;\\=\sigma^2&space;\left&space;(&space;n&space;-&space;tr((X'X)^{-1}X'X)&space;\right&space;)&space;\\=\sigma^2&space;\left&space;(&space;n&space;-&space;tr(I_{(p&plus;1)&space;\cdot&space;(p&plus;1)})&space;\right&space;)&space;\\=\sigma^2&space;\left&space;(&space;n&space;-&space;(p&plus;1)&space;\right&space;)&space;" />  

所以我們就得到了此估計量具備不偏性!  
接著我們要證明這個估計量的分布是卡方，自由度是n-(p+1)。  
在證明之前需要用到一個小性質:  
```
當Z是一個k維的standard Normal random vector且B是任一rank為r的idempotent矩陣，則Z'BZ的分布會是卡方，自由度為r。  
```
這個定理證明起來也不會太難，我之後會放到附錄內，這邊我們就暫時先拿來用吧~

首先我們知道sigma平方的不偏估計量可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sigma&space;\frac{n-(p&plus;1)}{\sigma^2}&space;\hat{\sigma}^2&space;=&space;\frac{1}{\sigma^2}\varepsilon'(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')\varepsilon&space;=&space;\left&space;(&space;\frac{\varepsilon&space;}{\sigma&space;}&space;\right&space;)'(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')\left&space;(&space;\frac{\varepsilon&space;}{\sigma&space;}&space;\right&space;)" />  
化簡成這個形式，目的就是為了要套用上面的定理小工具。  

我們可以確認看看中間那一包矩陣是不是idempotent:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')&space;\\&space;=I_{n&space;\cdot&space;n}-2X(X'X)^{-1}X'&plus;X(X'X)^{-1}X'X(X'X)^{-1}X'&space;\\&space;=I_{n&space;\cdot&space;n}-2X(X'X)^{-1}X'&plus;X(X'X)^{-1}X'&space;\\&space;=I_{n&space;\cdot&space;n}-X(X'X)^{-1}X'" />  
上面就是利用定義進行運算，發現自身互乘後仍為自己，即idempotent。  
接著我們利用idempotent矩陣的性質，也就是它的rank會等於trace:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}rank(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')=tr(I_{n&space;\cdot&space;n}-X(X'X)^{-1}X')=n-(p&plus;1)&space;" />

而我們知道epsilon在前提假設下是常態分布，除一個sigma後，其variance就被標準化了。  
這時候套用上面的小定理就可以知道sigma平方的估計量會是卡方，自由度為n-(p+1)!  

# Time Series Data
對於時間序列數據，除了使用深度學習LSTM、Transformer...等類神經網絡建模外，ARIMA是很泛用的統計模型。  
在講解模型之前，需要先了解資料與模型假設。  
首先要使用ARIMA模型之前，我們的時序資料必須是穩態的(stationary)，也就是白噪音。而辨別資料是否stationary在統計上有兩種檢定可以做:  
1. Kwiatkowski-Phillips-Schmidt-Shin (簡稱KPSS)
2. Augement Dicky-Fuller (簡稱ADF)

兩種檢定不同的是，H0的假設相反，KPSS假設H0為穩態，ADF假設H0是非穩態。  
那麼穩態的好處是什麼呢?  
具備穩態的時序資料能有穩定的mean和variance，讓模型的殘差能夠均衡地在0附近散布，就像迴歸對於殘差的假設一樣。  
當檢定結果非穩態時，我們可以透過一些手法對資料進行轉換，最常用的是Box-Cox變換:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_{transformed}=\left\{\begin{matrix}\frac{y^\lambda-1}{\lambda}\;,\;if\;\lambda\neq&space;1\\ln(y)\;,\;if\;\lambda=0\end{matrix}\right." />  

可能會有人問，為什麼lambda=0要用ln呢?  
其實這個問題對定義取極限就能得到了:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\displaystyle\lim_{\lambda\to&space;0}\frac{y^\lambda-1}{\lambda}\\=\displaystyle\lim_{\lambda\to&space;0}\frac{lny*y^\lambda}{1}\\=lny"/>  

實務上還是有可能做了Box-Cox之後，時序資料仍非穩態，這時候就要考慮資料是否有季節性(Seasonal Effect)。  
季節性影響如果明顯的話，看原數據趨勢或觀察PACF與ACF圖大致上就能看出。  

# Lag Operator
又叫做延遲算子，是用來簡化表示ARIMA模型的運算符號，通常使用B。  
假設原始時序數據為y，那麼對於時間點t來說，上一個時間點的資料可以被表示成當前時間點t的資料apply一個B:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_{t-1}=By_{t}"/>  
依此類推，t-2時間點就可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_{t-2}=B^{2}y_{t}"/>  

而時序中常見的差分(diff)，以一階差分為例可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_{t}-y_{t-1}=(1-B)y_{t}"/>  
依此類推，二階差分可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}(y_{t}-y_{t-1})-(y_{t-1}-y_{t-2})=y_{t}-2y_{t-1}&plus;y_{t-2}=(1-2B&plus;B^2)y_{t}=(1-B^2)y_{t}" />  
推廣到d階差分，就會是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}(1-B^d)y_{t}"/>  

如果將一般差分與季節性差分組合起來就會是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}(1-B)(1-B^m)y_{t}=(1-B-B^m-B^{m&plus;1})y_t=y_t-y_{t-1}-y_{t-m}-y_{t-m-1}"/>  

注意到一般差分和季節性差分先後順序所得結果是相同的，但如果有季節性的影響，通常會先消除季節性再做ARIMA建模。  




# Ridge Regression 收縮迴歸係數
我們知道在L2正則化之下，迴歸模型的loss為:  
$\left\||y-X\beta  \right\||^2+\lambda \left\|| \beta \right\||^2=(y-X\beta)^T(y-X\beta)+\lambda \beta^T\beta $  

因此我們可推得: 
$\hat{\beta}(\lambda )=(X'X+\lambda I)^{-1}X'y$  

根據奇異值分解(SVD)，我們可以把實矩陣分解為: $X=UDV'$  
其中U和V為orthogonal矩陣 ; D為對角矩陣，上面的元素稱為奇異值。  
(Note: 非0的奇異值個數即為矩陣X的rank!)  

接著我們分別看一下OLS和Ridge的解:  
$OLS(\hat{\beta})=(X'X)^{-1}X'y=(VDU'UDV')^{-1}VDU'y=VD^{-2}V'VDU'=VD^{-2}DU'y$  
$Ridge(\hat{\beta})=(X'X+\lambda I)^{-1}X'y=(VDU'UDV'+\lambda VIV')^{-1}VDU'y=V(D+\lambda I)^{-2}V'VDU'=V(D+\lambda I)^{-2}DU'y$  

我們只需要關注對角線上的值，也就是那些 $d_{ii} $  
注意到Ridge的對角線奇異值在分母多加了一個 $\lambda$，也就是說:  
$(D+\lambda I)^{-2}D \Rightarrow  \frac{d_{ii}}{d_{ii}^{2} + \lambda } \leq \frac{d_{ii}}{d_{ii}^{2}}$  

不難看出當分母變大，而分子不變，那麼係數自然就會縮減囉!  

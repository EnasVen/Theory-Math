# 統計學觀點 - Part1  
延續原先的初始假設，資料集與共變異矩陣為:  
<img src="https://latex.codecogs.com/svg.image?X^{T}&space;=&space;[x_{1}...x_{m}]&space;;&space;Cov(X)=\Sigma&space;" />  
  
將原始特徵進行線性組合，得到新變數Y:  
<img src="https://latex.codecogs.com/svg.image?Y_{1}&space;=&space;a_{1}^{T}X&space;=&space;a_{11}x_{1}&plus;...&plus;a_{1m}x_{m}"/>  
<img src="https://latex.codecogs.com/svg.image?Y_{2}&space;=&space;a_{2}^{T}X&space;=&space;a_{21}x_{1}&plus;...&plus;a_{2m}x_{m}"/>  
...  
<img src="https://latex.codecogs.com/svg.image?Y_{m}&space;=&space;a_{m}^{T}X&space;=&space;a_{m1}x_{1}&plus;...&plus;a_{mm}x_{m}"/>  
  
根據上面的資訊，我們可以計算出:  
<img src="https://latex.codecogs.com/svg.image?Var(Y_{i})=Var(a_{i}^{T}X)=Cov(a_{i}^{T}X&space;,&space;a_{i}^{T}X)=a_{i}^{T}\Sigma&space;a_{i}" />  
<img src="https://latex.codecogs.com/svg.image?Cov(Y_{i}&space;,&space;Y_{k})=Cov(a_{i}^{T}X,a_{k}^{T}X)=a_{i}^{T}\Sigma&space;a_{k}" />  
  
接著我們定義一套方法來尋找主成分:  
第1主成分 : 找到一組正交a1使得線性組合的variance最大。  
第2主成分 : 找到一組正交a2使得線性組合的variance最大，且與a1的線性組合Covariance為0。  
...  
第j主成分 : 找到一組正交aj使得線性組合的variance最大，且與其餘線性組合Covariance為0。  
  
  
# 統計學觀點 - Part2  
假設共變異矩陣具備scale後的特徵值與特徵向量數對:  
<img src="https://latex.codecogs.com/svg.image?(\lambda_{1},e_{1})...(\lambda_{m},e_{m})"/>  
  
第i個主成分可以表示為: 
<img src="https://latex.codecogs.com/svg.image?Y_{i}=e_{i}^{T}X=e_{i1}x_{1}&plus;...&plus;e_{im}x_{m}"/>  
第i個主成分的變異量為: 
<img src="https://latex.codecogs.com/svg.image?Var(Y_{i})=e_{i}^{T}\Sigma&space;e_{i}=e_{i}^{T}\lambda_{i}e_{i}=\lambda_{i}"/>  
第i個主成分與第j個主成分的共變異量為: 
<img src="https://latex.codecogs.com/svg.image?Cov(Y_{i},Y_{j})=e_{i}^{T}\Sigma&space;e_{j}=e_{i}^{T}(\lambda_{j}e_{j})=0"/>  
  
根據先前結果，我們知道總變異其實就是eigenvalue的和:  
<img src="https://latex.codecogs.com/svg.image?diag(\Sigma)=\lambda_{1}&plus;...&plus;\lambda_{m}=\sum_{i=1}^{m}var(Y_{i})=\sigma_{11}&plus;\sigma_{22}&plus;...&plus;\sigma_{mm}=\sum_{i=1}^{m}var(X_{i})" />  
  
對於第k個主成分，我們可以知道他佔整體變異的比例: <img src="https://latex.codecogs.com/svg.image?\frac{\lambda_{k}}{\lambda_{1}&plus;...&plus;\lambda_{m}}" />  
  
也可以計算第k個特徵和第i個主成分的相關係數:
<img src="https://latex.codecogs.com/svg.image?\rho_{Y_{i},x_{k}}=&space;\frac{e_{ik}\lambda_{i}}{\sqrt{\sigma_{kk}}}" />  
其中eik為因素負荷量(factor loading)，代表該主成分與特徵k的相關性大小!!  

  



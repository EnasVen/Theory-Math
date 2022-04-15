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

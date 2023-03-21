# 如何選取最好的k?
由於分群數需要預先指定，因此實務上通常會run一定數量的k在來判別。  
那麼判別的標準是什麼呢?  

常用的方法: Elbow Method以及Gap Statistic  

# Elbow Method
我們可以透過計算群內每個點兩兩之間的距離，加總起來衡量分群效果:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}D_k=\sum_{x_i\in&space;C_k}&space;\sum_{x_j\in&space;C_k}&space;\left\|x_i-x_j&space;\right\|^2" />  
上式為第k群的群內相互距離，可化簡為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}D_k=2*n_k\sum_{x_i\in&space;C_k}&space;\left\|x_i-\mu_k&space;\right\|^2" />  
標準化後得到:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}W_K=\sum_{k=1}^{K}\frac{1}{2n_k}D_k" />  

這個就是Elbow Method圖表在y軸的計算指標。  
當然，回顧之前階層式分群的markdown，我們也可以利用Silhoutte做為分群依據。  
不過這邊要介紹另一個用統計技巧獲得的指標: Gap Statistic!  

# Gap Stastic
Gap Statistic定義為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Gap_n(k)=E_{n}^{*}logW_k-logW_k" />  
而  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E_{n}^{*}logW_k=\frac{1}{B}\sum_{b=1}^{B}log(W_{kb}^{*})" />  

意思就是先透過Boostrap產生和原始數據相同shape的資料，接著對這份資料做KMeans。  
重複B次後逼近真實值，即蒙地卡羅手法。  

同時需要計算sk來修正MC方法的誤差:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\\&space;w'=\frac{1}{B}\sum_{b=1}^{B}logW_{kb}^{*}&space;\\sd(k)=\sqrt{\frac{1}{B}\sum_{b=1}^{B}(logW_{kb}^{*}-w')^2}&space;\\s_k&space;=&space;\sqrt{\frac{B&plus;1}{B}}sd(k)&space;" />  

選擇滿足 <img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Gap(k)\geq&space;Gap(k&plus;1)-s_{k&plus;1}" title="https://latex.codecogs.com/png.image?\inline \dpi{110}Gap(k)\geq Gap(k+1)-s_{k+1}" /> 的k值做為分群數量即可。  


# GMM模型初探
GMM會用到EM演算法去估計隱含變量，還沒看過EM演算法的讀者可以先去上一章節觀看。  

首先我們要知道GMM的模型怎麼來的，根據資料，我們已知有k個feature。  
GMM的流程就是從k個高斯模型中，根據權重選出一個模型，然後針對此模型進行抽樣，進而產生新資料。  

所以我們先把這樣的流程數學化，看得比較清楚:  
每一個高斯模型都會有一個權重，我們把這k個權重集合起來，成為一個list，叫做z  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}z=[z_1,&space;z_2,&space;...,&space;z_k]"  />

對於z，我們定義如下:
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}z_i&space;=&space;0&space;\&space;\forall&space;i\neq&space;k&space;"  />  
也就是說當第k個模型被選中的時候，它對應的k-t分量才會是1，其餘非k的位置都是0，有一點類似one-hot encoding的感覺。  

由於Z是隱含變量，我們無法直接觀測，其先驗機率(prior)為: 
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(z_i=1)=\alpha&space;_i&space;,&space;\&space;\forall&space;i=1,2...,k"  />  
這個值就是每個高斯分布的權重!  

我們可以接著得到Z的pdf為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(z)=\prod_{i=1}^{k}p(z_i=1)^{z_i}=\prod_{i=1}^{k}\alpha_{k}^{z_k}"  />  

並且能推出X|Z的pdf:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(x|z_k=1)=p(x|\mu_k,&space;\Sigma_k)&space;\Rightarrow&space;p(x|z)=\prod_{i=1}^{k}p(x|z_k=1)^{z_k}=p(x|\mu_k,&space;\Sigma_k)^{z_k}" />

那麼有了條件pdf，是不是就能得到joint pdf呢?  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(x,z,\mu&space;,\Sigma)\\&space;=\sum_{Z}&space;p(X|Z)*p(Z)\\&space;=\sum_{i=1}^{k}&space;p(x|z_i=1)*p(z_i=1)\\&space;=\sum_{i=1}^{k}\alpha_i&space;*p(x|\mu_i,&space;\Sigma_i)&space;" />

注意這裡的u和sigma(cov. matrix)各有k個!

把高斯分布的pdf置換後就能得到GMM模型的理論形式:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(x,z,\mu&space;,\Sigma)=\sum_{i=1}^{k}\alpha_i&space;*&space;N(x|\mu_i,&space;\Sigma_i)&space;\\N(x|\mu_i,&space;\Sigma_i)=\frac{1}{\sqrt{(2\pi)^d&space;|\Sigma_i|}}exp{-\frac{1}{2}(x-\mu_i)^T\Sigma_{i}^{-1}(x-\mu_i)}&space;&space;\\subject\&space;to&space;:&space;\&space;&space;\sum_{i=1}^{k}\alpha_i=1&space;\&space;,&space;\&space;&space;0\leq&space;\alpha_i<1"  />

重點來了，當我們已經預先假設初始參數u和sigma(cov. matrix)時，我們就能透過後驗分布(posterior)的計算得到樣本來自第i個高斯模型的機率:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}p(z_i=1|x)=\frac{p(x|z_i=1)p(z_i=1)}{p(x)}=\frac{\alpha_iN(x|\mu_i,\Sigma_i)}{\sum_{t=1}^{k}N(x|\mu_t,\Sigma_t)}" />



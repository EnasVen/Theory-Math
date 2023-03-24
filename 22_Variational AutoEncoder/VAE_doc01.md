# 模型精神
傳統的AutoEncoder會將input資料壓縮成embedding vector後再利用上採樣(Up-Sampling)還原。  
但是這樣一來一往的過程由於經過非線性的運算，decode出來的圖像未必能完整呈現原始資訊。  
於是VAE透過加入noise(N(0,1))來讓decoder在noise附近也能很好地還原最初的圖像。  

和傳統AE不同的是，VAE在Encoder階段會產出高斯分布所需要的mean和variance，並試著讓這些資料點逼近Standard Noraml。  
最後給Decoder生成新的mean和variance，透過GMM產生圖像與原圖比較(算cross-entropy)。  

因此整體loss就包含兩塊: encoder階段和標準常態的KLD；以及生成圖像和原始圖像的loss!!  

# 架構
假設X為已知數據、Z為隱含變量(假設為標準常態分布)，VAE的流程圖如下:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/22_Variational%20AutoEncoder/VAE_pic00.png)  

# 理論推演
首先我們知道數據X的log-liklihood可以被寫成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}L=ln\left&space;(&space;\prod_{x}p(x)&space;\right&space;)=\sum_{x}lnp(x)" />  
而lnp(x)可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}lnp(x)\\&space;=\int_{z}q(z|x)lnp(x)dz&space;\\&space;=&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z,x)}{p(z|x)}&space;\right&space;)dz&space;\\&space;=&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z,x)}{q(z|x)}\frac{q(z|x)}{p(z|x)}&space;\right&space;)dz&space;\\&space;=&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z,x)}{q(z|x)}&space;\right&space;)dz&space;&plus;&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{q(z|x)}{p(z|x)}&space;\right&space;)dz&space;\\&space;=&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z,x)}{q(z|x)}&space;\right&space;)dz&space;&plus;&space;KLD(q(Z|X)&space;||&space;p(Z|X))&space;\\&space;\geq&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z,x)}{q(z|x)}&space;\right&space;)dz" />  

所以要最大化log-liklihood，等價於最大化上面的理論下界。  
當q(z|x)=p(z|x)時，我們得到的KLD會是0，也就是說調整q(z|x)可以讓我們的理論下界逼近真實數據X!  

我們把上式的理論下界整理一下會得到:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z,x)}{q(z|x)}&space;\right&space;)dz&space;\\&space;=&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(x|z)p(z)}{q(z|x)}&space;\right&space;)dz&space;\\&space;=&space;\int_{z}q(z|x)ln\left&space;(&space;\frac{p(z)}{q(z|x)}&space;\right&space;)dz&space;&plus;&space;\int_{z}q(z|x)ln\left&space;(&space;p(x|z)&space;\right&space;)dz&space;\\&space;=&space;-KLD(q(Z|X)&space;||&space;p(Z))&space;&plus;&space;\int_{z}q(z|x)ln\left&space;(&space;p(x|z)&space;\right&space;)dz" />  

也就是說，要讓它逼近原始數據logP(X)，我們必須讓第一項的負KLD越小越好。  
那越小越好意思就是我們的Z|X分布要與Z越近越好。  
這句話的意思，就是**根據輸入至Encoder所得到的輸出，要和標準常態分布越接近越好!!**  

接著看後面那一項，它其實可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\int_{z}q(z|x)ln\left&space;(&space;p(x|z)&space;\right&space;)dz&space;=&space;E_{Z|X}\left&space;[&space;lnp(X|Z)&space;\right&space;]" />  

也就是說，透過Encoder產生的z|x，餵給Decoder之後，讓我們的lnP(X|Z=z)越接近原始圖像越好!(也就是lnP(X))   

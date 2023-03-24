# 程式碼內的KLD運算
在demo code中，我們可以看到KLD loss那邊是使用這個:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/22_Variational%20AutoEncoder/VAE_pic01.png)  

這一份markdown會推導一次如何證明最小化KLD等價於最小化上面那個式子!  

首先我們有兩個分布，一個是透過資料X經過Encoder生成的z|x；另一個則是假設的標準常態分布Z~N(0,1)。  
w.o.l.g 我們先推一下計算兩常態分布的KLD(mean和var分別指定為u1 u2以及sigma1 sigma2):  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}KLD(P(X)||Q(X))=\int&space;p(x)ln\frac{p(x)}{q(x)}dx=\int&space;(lnp(x)-lnq(x))p(x)dx&space;\\\because&space;p(x)=\frac{1}{\sqrt{2\pi}\sigma_1}e^{-\frac{(x-\mu_1)^2}{2\sigma_{1}^2}}&space;\&space;and&space;\&space;q(x)=&space;\frac{1}{\sqrt{2\pi}\sigma_2}e^{-\frac{(x-\mu_2)^2}{2\sigma_{2}^2}}&space;\\\therefore&space;KLD(P(X)||Q(X))=&space;\int&space;p(x)\left&space;[&space;-\frac{1}{2}ln2\pi&space;-ln\sigma_1-\frac{1}{2}\left&space;(&space;\frac{x-\mu_1}{\sigma_1}&space;\right&space;)^2&space;&plus;&space;\frac{1}{2}ln2\pi&space;&plus;ln\sigma_2&plus;&space;\frac{1}{2}\left&space;(&space;\frac{x-\mu_2}{\sigma_2}&space;\right&space;)^2&space;\right&space;]dx&space;\\=&space;\int&space;p(x)\left&space;[&space;ln\frac{\sigma_2}{\sigma_1}&plus;\frac{1}{2}\left&space;(&space;\left&space;(&space;\frac{x-\mu_2}{\sigma_2}&space;\right&space;)^2-\left&space;(&space;\frac{x-\mu_1}{\sigma_1}&space;\right&space;)^2&space;\right&space;)&space;\right&space;]dx" />  

上式其實就對P取期望值:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E_{P}\left&space;[&space;ln\frac{\sigma_2}{\sigma_1}&plus;\frac{1}{2}\left&space;(&space;\left&space;(&space;\frac{X-\mu_2}{\sigma_2}&space;\right&space;)^2-\left&space;(&space;\frac{X-\mu_1}{\sigma_1}&space;\right&space;)^2&space;\right&space;)&space;\right&space;]&space;\\&space;=&space;ln\frac{\sigma_2}{\sigma_1}&plus;\frac{1}{2\sigma_{2}^2}E_{p}(X-u_2)^2-\frac{1}{2\sigma_{1}^2}E_{p}(X-u_1)^2&space;\\&space;=&space;ln\frac{\sigma_2}{\sigma_1}&plus;\frac{1}{2\sigma_{2}^2}E_{p}(X-u_2)^2-\frac{1}{2}&space;\\&space;=&space;ln\frac{\sigma_2}{\sigma_1}&plus;&space;\frac{\sigma_{1}^2&plus;(\mu_1-\mu2)^2}{2\sigma_{2}^2}-\frac{1}{2}" />  

最後一列利用了加一項減一項的小手法，在X-u2中間加一個u1再減掉u1，然後平方展開後對p取期望值就可得到。  

而現在我們的Q分布就是N(0,1)，把u2=0 ; sigma2=1帶入後就能得到最一開始的圖內的code。  

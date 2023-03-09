# 運用EM演算法
先把符號定義清楚:  
X,Z以及theta分別為我們的數據、隱含變量以及隱含變量的參數:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\\X=(x_1,&space;x_2,&space;...,&space;x_N)&space;\\Z=(z_1,&space;z_2,&space;...,&space;z_N)&space;\\&space;\theta=(p,&space;\mu&space;,&space;\Sigma&space;)&space;\\\\p=(p_1,&space;p_2,&space;...,&space;p_k)\\\mu&space;=&space;(u_1,&space;u_2,&space;...,&space;u_k)\\\Sigma&space;=&space;(\Sigma_1,&space;\Sigma_2,&space;...,&space;\Sigma_k)&space;&space;" />

根據上章節EM演算法的結果，我們知道E-Step就是構造Q函數:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Q(\theta&space;,&space;\hat{\theta^{(t)}})=E_{Z|X,\theta^{(i)}}[logP(X,Z|\theta)]"  />

由於每個樣本都是iid，所以log-liklihood可以寫成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}logP(X,Z|\theta&space;)=log(\prod_{i=1}^{N}P(x_i,&space;z_i|\theta))=\sum_{i=1}^{N}logP(x_i,&space;z_i|\theta)" />  

而Z的posterior dist. 如下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}P(Z|X,\theta^{(t)})=\prod_{i=1}^{N}P(z_i|x_i,\theta^{(t)})" />  

所以我們可以把Q函數化簡:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sum_{Z}\left&space;[&space;\left&space;(&space;\sum_{i=1}^{N}logP(x_i,z_i|\theta)&space;\right&space;)P(Z|X,\theta^{(t)})&space;\right&space;]&space;\\=&space;\sum_{Z}[logP(x_1,z_1|\theta)P(Z|X,\theta^{(t)}|)&plus;...&plus;logP(x_N,z_N|\theta)P(Z|X,\theta^{(t)}|)]" />

原式被拆成了N個part相加，我們focus在第一項規律:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sum_{Z}\left&space;(&space;logP(x_1,z_1|\theta&space;)P(Z|X,\theta^{(t)})&space;\right)&space;\\=&space;\sum_{z_1...z_N}\left&space;(&space;logP(x_1,z_1|\theta&space;)\prod_{i=1}^{N}P(z_i|x_i,&space;\theta^{(t)})&space;\right)\\=&space;\sum_{z_1...z_N}&space;logP(x_1,z_1|\theta&space;)P(z_1|x_1,&space;\theta^{(t)})\left&space;(&space;\prod_{i=2}^{N}P(z_i|x_i,&space;\theta^{(t)})&space;\right&space;)\\=&space;\sum_{z_1}\sum_{z_2...z_N}&space;logP(x_1,z_1|\theta&space;)P(z_1|x_1,&space;\theta^{(t)})\left&space;(&space;\prod_{i=2}^{N}P(z_i|x_i,&space;\theta^{(t)})&space;\right&space;)\\=&space;\sum_{z_1}&space;logP(x_1,z_1|\theta&space;)P(z_1|x_1,&space;\theta^{(t)})&space;*&space;\sum_{z_2...z_N}\left&space;(&space;\prod_{i=2}^{N}P(z_i|x_i,&space;\theta^{(t)})&space;\right&space;)" />  

後面那一項其實都是1在相乘:  

假設我們有數據 X 滿足: 
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}X&space;=&space;(x_1,&space;x_2,&space;...&space;,&space;x_n)" />  且各隨機變數均為iid

未知參數則為theta，那麼我們可以得到log-liklihood為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}l(\theta&space;|X)=log&space;P(X|\theta&space;)&space;=&space;log(\prod_{i=1}^{n}P(x_i|\theta&space;))=\sum_{i=1}^{n}logP(x_i|\theta&space;)" />

如果是沒有潛在變數z的情況(例如: K-Means)，那麼我們就可以透過MLE求得最佳的theta來最大化log-liklihood，也就是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\hat{\theta}_{MLE}=\underset{\theta}{argmax}\&space;\sum_{i=1}^{n}logP(x_i|\theta&space;)" />

假設Z是我們無法觀測到的變數，那麼原先的log-liklihood可以改寫成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}log&space;P(X|\theta)&space;=&space;log\sum_{Z}{}P(X,Z|\theta&space;)=log\sum_{Z}{}P(X|\theta,Z)P(Z|\theta)"/>

假設Z的分布為q(z)，那麼我們知道pdf總合為1，也就是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sum_{Z}q(z)=1"/>

所以我們會得到:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}P(X|\theta)=\frac{P(X,Z|\theta&space;)}{P(Z|X,\theta)/q(Z)}=\frac{P(X,Z|\theta&space;)/q(Z)}{P(Z|X,\theta)/q(Z)}" />

兩邊同時取log會得到:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}logP(X|\theta)=log\frac{P(X,Z|\theta&space;)/q(Z)}{P(Z|X,\theta)/q(Z)}" />  

接者左右兩邊同時對Z取期望值:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E_{Z}[logP(X|\theta)]=E_{Z}[log\frac{P(X,Z|\theta&space;)/q(Z)}{P(Z|X,\theta)/q(Z)}]" />  

LHS: 由於跟Z無關，所以仍然維持原式。  
RHS:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sum_{Z}q(z)log\frac{P(X,Z|\theta&space;)/q(z)}{P(Z|X,\theta&space;)/q(z))}&space;\\=&space;\sum_{Z}q(z)\frac{P(X,Z|\theta)}{q(z)}&space;-&space;\sum_{Z}q(z)\frac{P(Z|X,\theta&space;)}{q(z)}&space;\\=&space;\sum_{Z}q(z)\frac{P(X,Z|\theta)}{q(z)}&space;&plus;&space;KL_D(q(z)&space;||&space;P(Z|X,\theta&space;))&space;\\\geq&space;\sum_{Z}q(z)\frac{P(X,Z|\theta)}{q(z)}&space;"  />

# 理論推導

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
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\sum_{Z}q(Z)log\frac{P(X,Z|\theta&space;)/q(Z)}{P(Z|X,\theta&space;)/q(Z))}&space;\\=&space;\sum_{Z}q(Z)\frac{P(X,Z|\theta)}{q(Z)}&space;-&space;\sum_{Z}q(Z)\frac{P(Z|X,\theta&space;)}{q(Z)}&space;\\=&space;\sum_{Z}q(Z)\frac{P(X,Z|\theta)}{q(Z)}&space;&plus;&space;KL_D(q(Z)&space;||&space;P(Z|X,\theta&space;))&space;\\\geq&space;\sum_{Z}q(Z)\frac{P(X,Z|\theta)}{q(Z)}&space;"  />

至此，我們得到了LOG-LIKLIHOOD的最小下界，只有當KLD=0時，等號才成立!  
也就是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}q(Z)=&space;P(X,Z|\theta)"  />  

而因為q是無法觀測的，所以實務上我們會先讓q=P，然後進行後續運算。  
也就是給定初始的theta，然後計算P。

在初始theta之下，我們得到了q(z)。  
這也就意味著我們能透過MLE來尋找下一個theta了!  

<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\hat{\theta&space;}&space;\\=&space;\underset{\theta&space;}{argmax}&space;\sum_{Z}q(Z)log\frac{P(X,Z|\theta)}{q(Z)}&space;\\=&space;\underset{\theta&space;}{argmax}&space;\sum_{Z}P(Z|X,\theta^{(i)})log\frac{P(X,Z|\theta)}{P(Z|X,\theta^{(i)})}&space;\\=&space;\underset{\theta&space;}{argmax}&space;\sum_{Z}P(Z|X,\theta^{(i)})(logP(X,Z|\theta)-log&space;P(Z|X,\theta^{(i)})&space;\\=&space;\underset{\theta&space;}{argmax}&space;\sum_{Z}P(Z|X,\theta^{(i)})logP(X,Z|\theta)&space;\\=&space;\underset{\theta&space;}{argmax}&space;E_{Z|X,\theta^{(i)}}[logP(X,Z|\theta)]"  />

上面最後一式，就是E-Step在做的事情: 構造Q(theta, theta(i))  
而尋找新的theta這步，就是M-Step在做的事情。  

有了新的theta後，再帶回去原本的E-Step，把之前的初始theta換掉，再得到一次新的theta...循環下去。  
這就是EM演算法的流程: **E**xpectation + **M**aximization!  

# 理論推導
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Given&space;\&space;&space;data&space;:&space;\{x_1,...,x_N\}&space;\&space;with&space;\&space;r_{nk}\in&space;\{0,1\}&space;\&space;\forall&space;n=1,2,...N" />
這裡的rnk代表第n筆資料在第k群的判定，因此取值只能為0或1。  

同時，我們也定義每一群的中心為: u  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Define&space;\&space;cluster&space;\&space;mean&space;\&space;\mu_i&space;\&space;\forall&space;i=1,2,...,k" />  

我們可以推出第k群的中心為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}u_k&space;=&space;\frac{\sum_{i=1}^{N}r_{ik}x_i}{\sum_{i=1}^{N}r_{ik}}" />  

接著定義Loss Function，我們希望每一群內的差距越小越好。  
因此整體loss即為每一筆資料點對應每一群中心的SSE!  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}L=\sum_{i=1}^{N}\sum_{j=1}^{K}r_{ij}\left\|x_i-u_j&space;\right\|^2" />

由於這邊有兩個參數，無法直接透過微分求解，因此我們需要用到EM演算法來進行迭代!  

# E-Step: initialize cluster mean to update rnk
先給定每一群的初始參數(隨機指定群中心)，當然K值要預先指定。  
核心思想就是在給定群中心的前提下，每一群內的SSE要越小越好。  
也就是說我們要優化:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\left\|x_i-u_j&space;\right\|^2" />  
找到和第i個樣本距離最小的cluster j，然後將這個樣本的rij值設定為1，其餘rix設定為0。  
也就是:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}r_{ij}=&space;\left\{\begin{matrix}1&space;\&space;if&space;\&space;j=\underset{t}{argmin}\left\|&space;x_i-u_t\right\|^2&space;\\0&space;\&space;otherwise\end{matrix}\right." title="https://latex.codecogs.com/png.image?\inline \dpi{110}r_{ij}= \left\{\begin{matrix}1 \ if \ j=\underset{t}{argmin}\left\| x_i-u_t\right\|^2 \\0 \ otherwise\end{matrix}\right." />  

這麼做其實就已經把第i個樣本暫時歸到第j群。  

# M-Step: update cluster mean
當每一筆資料的rnk都確定時，我們就能透過微分獲得最佳的u使得各群的Loss最小:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\frac{\partial&space;L}{\partial&space;\mu_j}=2\sum_{i=1}^{N}r_{ij}(x_i-\mu_j)=0&space;\\\Rightarrow&space;&space;\mu_j&space;=&space;\frac{\sum_{i=1}^{N}r_{ij}x_i}{\sum_{i=1}^{N}r_{ij}}" title="https://latex.codecogs.com/png.image?\inline \dpi{110}\frac{\partial L}{\partial \mu_j}=2\sum_{i=1}^{N}r_{ij}(x_i-\mu_j)=0 \\\Rightarrow \mu_j = \frac{\sum_{i=1}^{N}r_{ij}x_i}{\sum_{i=1}^{N}r_{ij}}" />  
此時已經完成對於u的更新，接著重複E-Step和M-Step直到收斂，即為KMeans演算流程!  



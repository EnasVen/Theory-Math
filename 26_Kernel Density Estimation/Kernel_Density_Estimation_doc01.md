# 核密度估計 v.s. 高斯混合模型
兩種手法都可以估計pdf，但本質上還是有很大的區別。  
* Non-Parametrized vs Parametrized:  
GMM為有母數手法，假定數據為多個常態分布組合而成，各自的mean、variance為需要估計的參數；KDE則為無母數手法，沒有對原始數據分布做假設。  
* Model Structure:  
GMM假設數據由多個高斯分布依照不同權重組合；KDE則對每一筆數據使用Kernel function平滑化後進行加總。  
* Estimation:  
GMM透過EM algorithm來估計參數；KDE則無需估計參數，只要選擇合適的Kernel function以及bandwidth。  

# 理論推演
給定N筆數據，均為iid分布且cdf為F:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}&space;X_{1},X_{2},...,X_{N}\overset{iid}{\rightarrow}F(x)"/>  
則對於f在x點的函數值(pdf取值)，我們可以用極限來表示:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}f(x)=\displaystyle\lim_{h\to&space;0}\frac{F(x&plus;h)-F(x-h)}{2h}"/>  
而f的估計函數可以被表示為:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\hat{f}(x)=\frac{1}{2h}\displaystyle\lim_{h\to&space;0}\frac{N(x_i\in[x-h,x&plus;h])}{N}"/>  
也就是說當h足夠小時，區間內的資料筆數佔整體資料之比例即為該點的pdf值。  
其中分子N代表落在[x-h,x+h]閉區間的資料個數，分母N即為總資料數。  

估計函數f可以用更數學的方式來表達:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\hat{f}(x)\\=\frac{1}{2hN}\displaystyle\lim_{h\to&space;0}\sum_{i=1}^{N}I(x_i\in[x-h,x&plus;h])\\=\frac{1}{hN}\displaystyle\lim_{h\to&space;0}\sum_{i=1}^{N}\frac{1}{2}I(\frac{|x-x_i|}{h}\leq&space;1&space;)"/>  
接著做一個變換，K即為我們的kernel function:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Let\;K(t)=\frac{1}{2}I(t\leq&space;1)\Rightarrow\hat{f}(x)=\displaystyle\lim_{h\to&space;0}\frac{1}{Nh}\sum_{i=1}^{N}K(\frac{x-x_i}{h})"/>  

但是這個Kernel function是有限制的，限制條件怎麼獲得?  
透過機率密度函數積分為1的特性:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\int\hat{f}(x)dx=1\\\Rightarrow\displaystyle\lim_{h\to&space;0}\frac{1}{Nh}\sum_{i=1}^{N}\int&space;K(\frac{x-x_i}{h})dx=\frac{1}{N}\sum_{i=1}^{N}\int&space;K(t)dt=\int&space;K(t)dt=1"/>  
(上面用到變數變換，所以1/h可以被收進去積分式內!)  

也就是說Kernel function只要滿足積分值為1即可。所以常見的Gaussian Kernel其實就是Normal pdf，那當然是滿足這個條件。  

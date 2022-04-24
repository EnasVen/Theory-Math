# 梯度下降法  
實務上大多問題的最初方向都是最佳化，例如尋找最便宜的餐鼟、最快的行車路線、最省時的方案...etc  

<img src="https://latex.codecogs.com/png.image?\dpi{110}L:loss&space;function&space;;&space;\theta:parameters"/>  
我們想找到一個未知參數，它能讓損失函數(loss)達到最小!  
用數學語言來說，就是:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\theta^*&space;=&space;\underset{\theta&space;}{argmin}L(\theta&space;)"/>  

而梯度下降法就是一套尋找最佳參數的過程。  
以2維參數舉例，我們定義梯度(Gradient)為:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\bigtriangledown&space;L(\theta&space;)=\begin{bmatrix}\frac{\partial}{\partial&space;\theta_1}&space;L(\theta&space;)\\\frac{\partial}{\partial&space;\theta_2}&space;L(\theta&space;)\end{bmatrix}"/>  
   
參數的更新過程可以寫成:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\theta_{new}&space;=&space;\theta_{old}&space;-\eta*\bigtriangledown&space;L(\theta&space;)"  />  
 
梯度下降會根據給定的學習率(learning rate)逐漸修正參數，一般來說這個值會很大地影響整個梯度下降優化的結果。(太大容易過早收斂不好的結果;太小容易發散)  
因此Adaptive Learning Rate就誕生了!  
這類方法在每一次的iteration調整learning rate，初始給予較大的值，之後漸漸降低。  
這樣能夠讓收斂速度更平滑，下圖為Adaptive Learning Rate的一種形式:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\eta_t=\frac{\eta&space;}{\sqrt{t&plus;1}}" />  
 
其中一種有名的方法叫做AdaGrad(Adaptive Gradient Descent):  
<img src="https://latex.codecogs.com/png.image?\dpi{110}w_{t&plus;1}=w_t&space;-&space;\eta_t*\frac{g_t}{\sigma_t}\\g_t&space;=&space;\frac{\partial&space;L(\theta_t)}{\partial&space;\omega&space;}&space;;\\\sigma_t&space;=&space;\sqrt{\frac{\sum_{i=1}^{t}g_{i}^2}{t&plus;1}}&space;" />  
(分母為了避免出現0的情況，嚴謹一點會加上一個常數項!)  

另一種較常見的稱為隨機梯度下降法(SGD,stochastic gradient descent):  
這個方法和普通gradient descent不同的地方在於更新參數時所使用的訓練數據大小。  
傳統gradient descent會使用全部訓練資料集，運算後更新一次參數。  
而SGD每一次只使用隨機1個或小部分的數據進行訓練，訓練後隨即更新參數。(這個小部分的數據就是mini-batch)  
這種方法的運算速度較傳統GD來的快，但學習率較大時，容易造成參數收斂過程變得鋸齒化(例如:極端大與極端小交互產生)  
  
另一個在GD需要注意的重點是Feature Scaling:  
沒有做數據標準化的GD，由於loss func. contour不規則，其梯度方向可能多變，造成收斂困難。  
而有做數據標準化的GD，loss func. contour較像同心圓，其梯度方向朝向圓心，收斂速度更快。  

# 負號的理由:  
首先我們先回顧一下，若函數h(x)在x=x0無窮可微，則h在x0的泰勒展開可以被寫成:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}h(x)=\sum_{k=0}^{\infty&space;}\frac{h^{(k)}(x_0)}{k!}(x-x_0)^k" />  
如果我們假設2次項後的數值都非常小，小到可以忽略，那麼h(x)就可以被簡寫成:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\displaystyle&space;\lim_{x\to&space;x_0}h(x)&space;=&space;h(x_0)&space;&plus;&space;h^{(1)}(x_0)(x-x_0)&space;" />  
  
接著我們把情境拓展到2維參數:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}h(x,y)&space;\approx&space;&space;h(x_0,y_0)&space;&plus;&space;\frac{\partial&space;h}{\partial&space;x}|_{x=x_0}(x-x_0)&space;&plus;&space;\frac{\partial&space;h}{\partial&space;y}|_{y=y_0}(y-y_0)"/>  
  
回到目前的loss function L，假設有兩個參數theta1&theta2，那麼L在(a,b)的泰勒展開可以寫成:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}L(\theta&space;)&space;\approx&space;&space;L(a,b)&space;&plus;&space;\frac{\partial&space;L(a,b)}{\partial&space;\theta_1}(\theta_1-a)&space;&plus;&space;\frac{\partial&space;L(a,b)}{\partial&space;\theta_2}(\theta_2-b)&space;=&space;s&plus;u(\theta_1-a)&space;&plus;&space;v(\theta_2-b)" />  
原先的問題也就變成:在(a,b)的open disk內找到一個點(theta1 , theta2)使得L達到最小!!  
<img src="https://latex.codecogs.com/png.image?\dpi{110}(\theta_1-a)^2&space;&plus;&space;(\theta_2-b)^2&space;\leq&space;&space;d^2" />  

上上式第一項s為常數，所以我們專注在後2項上。  
不難看出這個其實就是(u,v)向量和(theta1 , theta2)至(a,b)向量得內積!  
而根據線性代數，要讓內積的值最小，唯一解就是與反方向的向量做內積。  

因此(theta1 , theta2)至(a,b)向量的選擇就會是(u,v)向量的倍數，這個倍數我們給它加上負號，和(u,v)做反向內積。  
我們把這個倍數較做eta，根據上面的敘述可以推出(theta1 , theta2)這個點的形式:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\begin{bmatrix}\theta_1\\\theta_2\end{bmatrix}&space;=&space;\begin{bmatrix}a&space;\\b\end{bmatrix}&space;-\eta&space;\begin{bmatrix}u&space;\\v\end{bmatrix}"/>  

而這個形式正是一開始定義gradient descent所呈現的形式，這也是使用負號的原因!!  

還沒完，最後我們要在回顧一件事情，那就是原先假設泰勒展開只做到1次項，2次項後面都當作近似0。  
這個假設要成立的條件，必須是open disk要足夠小 => (theta1 , theta2)不能離(a,b)太遠 => 也就是說eta不能太大。  

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


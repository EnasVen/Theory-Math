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
 


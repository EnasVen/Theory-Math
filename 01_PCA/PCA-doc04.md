# 補充資訊  
延續先前的假設，令各特徵的平均值向量為  <img src="https://latex.codecogs.com/svg.image?u&space;=&space;(u_{1},u_{2},...,u_{m})"/>  
  
我們對數據X進行標準化會得到:  
<img src="https://latex.codecogs.com/svg.image?X_{normalized}=\begin{bmatrix}(x_{1}-u)^{T}\\...\\(x_{n}-u)^{T}\\\end{bmatrix}\begin{bmatrix}s_{1}^{-1}\\s_{2}^{-1}\\...\\s_{m}^{-1}\\\end{bmatrix}^{T}=\begin{bmatrix}\frac{(x_{11}-u_{1})}{s_{1}}&...&\frac{(x_{1m}-u_{m})}{s_{m}}\\...&&space;&space;&&space;&space;&&space;&space;\\\frac{(x_{n1}-u_{1})}{s_{1}}&...&\frac{(x_{nm}-u_{m})}{s_{m}}\\\end{bmatrix}"/>  
  
<img src="https://latex.codecogs.com/svg.image?\sum=\frac{1}{n-1}\sum_{i=1}^{n}(x_{i}-O_{mx1})(x_{i}-O_{mx1})^{T}=\frac{1}{n-1}X_{normalized}^{T}X_{normalized}"/>  

經過標準化的樣本共變異矩陣即為樣本相關矩陣(Correlation Matrix)，且對角線上的值為1。  
  
根據線代學到的理論，實對稱矩陣一定可正交對角化:  
<img src="https://latex.codecogs.com/svg.image?\exists&space;H&space;\Rightarrow&space;&space;\Sigma&space;=H\Lambda&space;H^{T}" />  
其中H為正交向量組成的矩陣，其自我相乘為單位矩陣!  
中間的lambda矩陣為對角矩陣，對角線上的值即為特徵值(eigenvalue)。  
  
這邊就能推出一個有趣的性質:  
<img src="https://latex.codecogs.com/svg.image?\sum_{i=1}^{m}\lambda_{i}=tr(\Lambda)=tr(H^{T}\Sigma&space;H)=tr(\Sigma&space;HH^{T})=tr(\Sigma)=m" />  
也就是說，特徵值的總和即為維度總數量。  

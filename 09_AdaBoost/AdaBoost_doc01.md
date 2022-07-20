# 定義
根據Adaptive Boosting建構定義，每一個子分類器均為弱分類。  
所謂弱分類就是準確率和random guess差不多(也就是0.5左右)!  

假設樣本i在第1個分類器的權重為u_i1，同時定義loss function，分對為0，分錯為1。  
loss的定義是根據演算法核心精神: 針對分錯的樣本在下一個分類器提高權重加強訓練  

接著我們來計算第一次的分類error rate:  
<img src="https://latex.codecogs.com/svg.image?\varepsilon_1&space;=&space;\frac{\sum_{wrong}^{&space;}u_{i1}*l(f(x_i)\neq&space;y_i)}{\sum_{all}^{&space;}u_{i1}}&space;<&space;0.5" title="\varepsilon_1 = \frac{\sum_{wrong}^{ }u_{i1}*l(f(x_i)\neq y_i)}{\sum_{all}^{ }u_{i1}} < 0.5" />  
上面的結果可理解為透過分錯樣本的加權平均來計算整體的error。  


根據上述定義，我們可以推出第二次分類的error rate。  
由於每一個分類器都是弱分類，不失一般性假設第二個分類器準確率為0.5:  
<img src="https://latex.codecogs.com/svg.image?\varepsilon_2&space;=&space;\frac{\sum_{wrong}^{&space;}u_{i2}*l(f(x_i)\neq&space;y_i)}{\sum_{all}^{&space;}u_{i2}}&space;=&space;0.5" title="\varepsilon_2 = \frac{\sum_{wrong}^{ }u_{i2}*l(f(x_i)\neq y_i)}{\sum_{all}^{ }u_{i2}} = 0.5" />  

但此時我們必須變更每一筆樣本的權重:  
<img src="https://latex.codecogs.com/svg.image?\left\{\begin{matrix}if&space;\&space;f(x_i)\neq&space;y_i&space;\Rightarrow&space;u_i2&space;=&space;u_i1&space;*&space;d_1&space;\\if&space;\&space;f(x_i)=&space;y_i&space;\Rightarrow&space;u_i2&space;=&space;u_i1&space;/&space;d_1\end{matrix}\right." title="\left\{\begin{matrix}if \ f(x_i)\neq y_i \Rightarrow u_i2 = u_i1 * d_1 \\if \ f(x_i)= y_i \Rightarrow u_i2 = u_i1 / d_1\end{matrix}\right." />  
這裡的d1為一個>1的數，我們預期將**上次分錯的樣本權重調高；而分對的樣本權重調低!**  

因此上式可以改寫為:  

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
<img src="https://latex.codecogs.com/svg.image?0.5&space;=&space;\frac{\sum_{wrong}u_i1*d_1}{\sum_{wrong}u_i1*d_1&space;&plus;&space;\sum_{correct}u_i1/d_1}" title="0.5 = \frac{\sum_{wrong}u_i1*d_1}{\sum_{wrong}u_i1*d_1 + \sum_{correct}u_i1/d_1}" />  

將等式兩邊取倒數:  
<img src="https://latex.codecogs.com/svg.image?2&space;=&space;\frac{\sum_{wrong}u_i1*d_1&space;&plus;&space;\sum_{correct}u_i1/d_1}{\sum_{wrong}u_i1*d_1}&space;=&space;1&plus;\left&space;(&space;\frac{\sum_{correct}u_i1/d_1}{\sum_{wrong}u_i1*d_1}&space;\right&space;)&space;\\\Rightarrow&space;&space;\sum_{wrong}u_i1*d_1&space;=&space;\sum_{correct}u_i1/d_1&space;\\Let&space;\&space;&space;z_1&space;=&space;&space;\sum_{correct}&space;&plus;&space;\sum_{wrong}&space;\Rightarrow&space;\varepsilon_1&space;=&space;\frac{\sum_{wrong}u_i1}{\sum_{wrong}u_i1&space;&plus;&space;\sum_{correct}u_i1}&space;=&space;\frac{\sum_{wrong}u_i1}{z_1}&space;\\\Rightarrow&space;\sum_{wrong}u_i1&space;=&space;\varepsilon_1&space;*&space;z_1&space;\&space;;&space;\sum_{correct}u_i1&space;=&space;(1-\varepsilon_1)&space;*&space;z_1" title="2 = \frac{\sum_{wrong}u_i1*d_1 + \sum_{correct}u_i1/d_1}{\sum_{wrong}u_i1*d_1} = 1+\left ( \frac{\sum_{correct}u_i1/d_1}{\sum_{wrong}u_i1*d_1} \right ) \\\Rightarrow \sum_{wrong}u_i1*d_1 = \sum_{correct}u_i1/d_1 \\Let \ z_1 = \sum_{correct} + \sum_{wrong} \Rightarrow \varepsilon_1 = \frac{\sum_{wrong}u_i1}{\sum_{wrong}u_i1 + \sum_{correct}u_i1} = \frac{\sum_{wrong}u_i1}{z_1} \\\Rightarrow \sum_{wrong}u_i1 = \varepsilon_1 * z_1 \ ; \sum_{correct}u_i1 = (1-\varepsilon_1) * z_1" />  
  
所以有了上面的結果，我們可以求解d1:  
<img src="https://latex.codecogs.com/svg.image?\\(\varepsilon_1&space;z_1)d_1&space;=&space;(1-\varepsilon_1)z_1\frac{1}{d_1}&space;\\\Rightarrow&space;d_{1}^{2}&space;=&space;&space;\frac{1-\varepsilon_1}{\varepsilon_1}&space;\\\Rightarrow&space;d_1&space;=&space;\sqrt{\frac{1-\varepsilon_1}{\varepsilon_1}}&space;\\&space;...\Rightarrow&space;d_t&space;=&space;\sqrt{\frac{1-\varepsilon_t}{\varepsilon_t}}" title="\\(\varepsilon_1 z_1)d_1 = (1-\varepsilon_1)z_1\frac{1}{d_1} \\\Rightarrow d_{1}^{2} = \frac{1-\varepsilon_1}{\varepsilon_1} \\\Rightarrow d_1 = \sqrt{\frac{1-\varepsilon_1}{\varepsilon_1}} \\ ...\Rightarrow d_t = \sqrt{\frac{1-\varepsilon_t}{\varepsilon_t}}" />  

上式就是AdaBoost的權重修正係數!! 

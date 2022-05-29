#  Lagrange Multiplier
在處理限制式的最佳化問題，這個方法很常被拿來使用。  
但使用限制在於處理的函數要是convex:  

<img src="https://latex.codecogs.com/png.image?\dpi{110}\frac{f(x_1)&plus;f(x_2)}{2}\geq&space;f(\frac{(x_1&plus;x_2)}{2})&space;" />

約束條件只會有種情形: 大於/等於/小於，而透過移向和變號，我們只需討論等於和小於(或大於)的情況。  
一般性的不等式約束條件，稱為KKT condition。  

# 理論基礎
以2維數據做例子，假設我們有n筆觀察值:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\{(x_i,y_i)\}&space;,&space;\forall&space;i&space;=&space;1,2,...n&space;,&space;\bold&space;x_i\in&space;\Re^d&space;,&space;\bold&space;y_i&space;=&space;\pm&space;1"  />

考慮數據線性可分(不混在一起)，我們希望兩種類別的資料(+1 & -1)能夠被清楚分開。  
因此我們的2維斜直線如下:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}[w_1&space;,&space;w_2]\begin{bmatrix}x_1&space;\\x_2\end{bmatrix}&space;&plus;b&space;=&space;0&space;\\\Rightarrow&space;w_1&space;x_1&space;&plus;&space;w_2&space;x_2&space;&space;=&space;-b&space;\\\Rightarrow&space;x_2&space;=&space;-\frac{w_1}{w_2}x_1&space;-&space;b&space;,&space;&space;(w_2&space;\neq&space;0)" />

在分隔線左下方的資料點為 y=-1，也就是w'x+b < 0 的區域 ; 而右上方的資料點為 y=+1，也就是w'x+b >0 的區域。  
我們分別將中心分隔線慢慢往左下/右上推進，，每次推進一定距離，直到碰觸第一個資料點為止。  

假設推進距離為h，那麼我們可以得到2條分隔線如下:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\left\{\begin{matrix}w'x&space;&plus;&space;b&space;\geq&space;&space;h&space;\\w'x&space;&plus;&space;b&space;\leq&space;&space;-h&space;\end{matrix}\right.\Rightarrow&space;\left\{\begin{matrix}w'x&space;&plus;&space;b&space;\geq&space;&space;1&space;\\w'x&space;&plus;&space;b&space;\leq&space;&space;-1&space;\end{matrix}\right.&space;(b&space;=&space;\frac{b}{h})"  />

其實就是透過同除h讓最右邊的常數為正負1，滿足y值域的初始假設。  

根據上面的式子，我們知道樣本點分類正確的情況會是:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}y_i(\bold&space;w'&space;x_i)&space;\geq&space;&space;1" />  

而SVM的目標就是在上式條件下，盡可能讓2條分隔線越寬越好。  
給定2條分隔線上的2點p(+側),q(-側)，這2條平行線的距離可以透過以下方式得到:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}width&space;=&space;\overrightarrow{pq}&space;*&space;\frac{\overrightarrow{w}}{\left\|\overrightarrow{w}\right\|}&space;\\&space;=&space;\frac{1}{\left\|w\right\|}*&space;[w'(x_q-x_p)&space;]&space;\\=&space;\frac{1}{\left\|w\right\|}*&space;[w'x_q&space;-&space;w'x_p]&space;\\&space;=&space;\frac{1}{\left\|w\right\|}*&space;(1-b-(-1-b))&space;\\=&space;\frac{2}{\left\|w\right\|}&space;" />

要讓這個寬度最大，等價於讓w的norm越小越好，也等價於讓w的norm平方除以2越小越好(除以2是方便後續運算，不影響方向)。  

我們可以透過Lagrange Multiplier，對各參數偏微分求解最佳化模型:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\underset{\alpha&space;}{arg&space;min}&space;L&space;=&space;\frac{1}{2}\left\|w\right\|^2&space;-&space;\sum_{i=1}^{n}\alpha_i[y_i(w'x_i&plus;b)-1]"  />

分別對b,w偏微分後可得:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\left\{\begin{matrix}\sum_{i=1}^{n}\alpha_i&space;y_i&space;=&space;0\\\sum_{i=1}^{n}\alpha_i&space;y_i&space;x_i&space;=w\end{matrix}\right."  />
此即SVM的KKT Condition!  

而根據KKT Condition的理論，求解最佳化模型有一個條件:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\alpha_i&space;[y_i(w'x_i&plus;b)-1]&space;=&space;0&space;" />  
依照Lagrange Multiplier的假設，我們的每一個alpha是大於等於0的常數，也就是說:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\alpha_i&space;=&space;\left\{\begin{matrix}0&space;,&space;&space;y_i(w'x_i&plus;b)&space;>&space;1&space;\\>0&space;,&space;y_i(w'x_i&plus;b)&space;=&space;1\end{matrix}\right.&space;" />

因此，當樣本點落在2條分隔線上的時候，其對應的alpha才會有非0的值。  
跟上面w推導的結果，w向量其實完全依賴邊線上的點才能形成。  
也可以說這些點支撐了2條分隔線(Hyper-Plane)，這些點被稱為支持向量(support vector)  
SVM便是以這些support vector建立分類線!!  

# 進階情況
實務上不可能像上面那樣所有資料都是完美分成2個明顯的區塊讓我們切割，一定有某些類別的點較靠近不屬於自己的類別群。  
這些情況通常發生在邊界區，因此我們需要將原始情況做一些調整:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\left\{\begin{matrix}w'x_i&space;&plus;&space;b&space;\geq&space;&space;1-\xi_i&space;,&space;\forall&space;y_i&space;=&space;&plus;1\\w'x_i&space;&plus;&space;b&space;\leq&space;&space;-1&plus;\xi_i&space;,&space;\forall&space;y_i&space;=&space;-1&space;,&space;\xi_i&space;\geq&space;0&space;,&space;\forall&space;i\end{matrix}\right."/>  

其實就是對原先width做了一點妥協: 好吧，一些模糊的點我就暫時放過，把它當作分對的情況好了!  
但這個調整的誤差項不能太大，因此我們需要給予penalty修正!(手法類似L1/L2那樣加在loss後面)  
<img src="https://latex.codecogs.com/png.image?\dpi{110}min&space;\&space;\frac{1}{2}\left\|w&space;\right\|^2&space;&plus;&space;C(\sum_{i}\xi_i)\\subjec&space;\&space;to&space;\left\{\begin{matrix}y_i(w'x_i&plus;b)-1&plus;\xi_i&space;\geq&space;&space;0&space;,&space;\forall&space;i&space;\\\xi_i&space;\geq&space;&space;0&space;,&space;\forall&space;i&space;\end{matrix}\right."  />

後續要做的就是對各別參數偏微分，得到新的KKT Condition。

SVM是由二元分類出發，如果要做多元分類，假設有k個類別，那麼有下面兩種方法:  
1. one-against-one : 須建立 k 個 model
2. one-against-all : 須建立 k(k-1)/2 個 model

SVM 調參的方法為Grid Search + CV，給定不同組合的參數下去try，像網格一樣，故名思義Grid。  

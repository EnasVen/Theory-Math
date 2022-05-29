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
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\left\{\begin{matrix}w'x&space;&plus;&space;b&space;\geq&space;&space;h&space;\\w'x&space;&plus;&space;b&space;\leq&space;&space;h&space;\end{matrix}\right.\Rightarrow&space;\left\{\begin{matrix}w'x&space;&plus;&space;b&space;\geq&space;&space;1&space;\\w'x&space;&plus;&space;b&space;\leq&space;&space;1&space;\end{matrix}\right.&space;(b&space;=&space;\frac{b}{h})" />

其實就是透過移項讓最右邊的常數為正負1，滿足y值域的初始假設。  


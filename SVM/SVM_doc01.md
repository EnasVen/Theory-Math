#  Lagrange Multiplier
在處理限制式的最佳化問題，這個方法很常被拿來使用。  
但使用限制在於處理的函數要是convex:  

<img src="https://latex.codecogs.com/png.image?\dpi{110}\frac{f(x_1)&plus;f(x_2)}{2}\geq&space;f(\frac{(x_1&plus;x_2)}{2})&space;" />

約束條件只會有種情形: 大於/等於/小於，而透過移向和變號，我們只需討論等於和小於(或大於)的情況。  
一般性的不等式約束條件，稱為KKT condition。  

# 理論基礎
假設我們有n筆觀察值:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}\{(x_i,y_i)\}&space;,&space;\forall&space;i&space;=&space;1,2,...n&space;,&space;\bold&space;x_i\in&space;\Re^d&space;,&space;\bold&space;y_i&space;=&space;\pm&space;1"  />







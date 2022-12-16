# GBDT的改良
在GBDT的基礎上，我們將往下探討XGBoost的原理。(尚未了解GBDT的讀者可以回到上一頁觀看GBDT的原理!)  

不同於原始GBDT，XGBoost加入了regularization，這個penalty是針對歷史總和模型，避免overfit所造成。  
我們的目標函數(Loss function + Penalty)的形式如下:  

<img src="https://latex.codecogs.com/png.image?\dpi{110}Obj&space;=&space;\sum_{i=1}^{n}L(y_i,&space;F(x_i))&space;&plus;&space;\Omega&space;(F(x_i))"/>  
前面的大寫L函數是loss finction，omega那一項則是penalty，裡面放入F函數代表要針對歷史加法模型作限制。  

根據boosting tree模型，我們在第t次迭代的目標函數可以寫成以下的形式:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}Obj^{(t)}&space;=&space;\sum_{i=1}^{n}L(y_i,&space;F_{t-1}(x_i)&plus;f_t(x_i))&space;&plus;&space;\Omega&space;(f_t(x_i))&space;&plus;&space;constant" />  
這時優化目標函數等價於優化當前的tree模型f，這也呼應了boosting的精神:改善前一次分類錯誤的樣本。  

我們將上面第t次迭代的函數在F_t-1(xi)的地方做泰勒展開:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}Obj^{(t)}&space;=&space;\sum_{i=1}^{n}L(y_i,&space;F_{t-1}(x_i))&space;&plus;&space;L^{(1)}(y_i,&space;F_{t-1}(x_i))f_t(x_i)&space;&plus;\frac{1}{2}L^{(2)}(y_i,&space;F_{t-1}(x_i))" /> <img src="https://latex.codecogs.com/png.image?\dpi{110}&plus;&space;\Omega&space;(f_t(x_i))&space;&plus;&space;constant"/>  

這邊為什麼可以寫成這樣是因為:  
f(x)在x=a的泰勒展開如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\sum_{n=0}^{\infty&space;}\frac{f^{(n)}(a)(x-a)^n}{n!}" />  
那麼現在的x=F + f (看一下Obj裡面L的引數)；a=我們在t-1時的F，所以x-a不就只剩下f了嗎?  

接著替換一下notation:  

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
<img src="https://latex.codecogs.com/png.image?\dpi{110}g_i=L^{(1)}(y_i,&space;F_{t-1}(x_i))&space;\&space;;&space;\&space;h_i=\frac{1}{2}L^{(2)}(y_i,&space;F_{t-1}(x_i))&space;"/>  

由於L(y, F_(t-1))這一項是常數(前面的歷史模型已經確定)，於是移掉常數的項目後，目標函數可以寫成:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}Obj^{(t)}=\sum_{i=1}^{n}[g_if_t(x_i)&plus;h_if_t(x_i)^2]&plus;\Omega(f_t(x_i))&space;" />

根據上式，優化Obj等價於優化f_t!  

# 正則化
假設tree模型有T個葉節點(leaf)，每個葉節點對應的值w可表示為T維實數向量。  
由於決策樹的特性，每一個葉節點的對應值都會相同，所以我們會得到:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}q&space;:&space;\mathbb{R}^T&space;\rightarrow&space;{1,2,...,T}" />  
也就是說，只要知道預測值，就知道該元素在第幾片葉節點上!  

更進一步來看，f可以被表示成:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f_t(x)&space;\Rightarrow&space;&space;w_{q(x)}" />  
其中q(x)代表樣本x在哪一個葉節點上，而w則代表那個葉節點的對應值是多少。  

回到小節主題，我們定義一個tree模型的複雜度如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\Omega(f_t(x_i))=\gamma&space;T&space;&plus;&space;\frac{1}{2}\lambda&space;\sum_{j=1}^{T}w_{j}^2&space;" />  

也就是說，tree的複雜度可以被寫成葉節點數量和對應值的實數向量的L2 norm!!  
關鍵的來了，我們假設第j個葉子的樣本index集合如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}I_j&space;=&space;\{i|q(x_i)=j&space;\}"/>  

I這個集合代表的意思是收集"那些"i，哪些i呢?  
使得第i個樣本屬於第j個葉節點的"那些"i。  
所以你會收集到一堆index，例如: 第10,07,99,...個樣本屬於某個葉節點。  

那我們就可以根據這個定義置換掉原先的summation from 1 to n (n個樣本)。  
為什麼可以置換呢?  
原本計算是每一個樣本的f值，由於每一個樣本最終都會存在於某個葉節點內。  
所以我們把葉節點內的元素全部起來，啊不就跟原本by樣本逐一計算的結果是一樣的嗎?  





施工中...

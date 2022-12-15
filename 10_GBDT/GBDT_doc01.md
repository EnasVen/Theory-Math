# 基本概念
GBDT，全名是 Gradient Boosting  Decision Tree。  
我們就不廢話太多，直接切入正題，來看看這個 ensemble 演算法後面的原理到底是什麼鬼。  
(reference CSDN大神: https://blog.csdn.net/quiet_girl/article/details/88756843 )  

首先boosting tree的概念就是加法模型；也就是當前的decision tree會想辦法預測上一棵樹的殘差(residual)，並將當前的tree加入歷史的trees成為新模型。  
而gradient的意思是GBDT會將loss的gradient當作是殘差(residual)的近似值，想辦法讓當前的模型能夠準確預測這個gradient。  

我們先來看一下loss function L在xi這個樣本點的負梯度是什麼形式:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}-[\frac{\partial&space;L(y_i,&space;F_{m-1}(x_i))}{\partial&space;F_{m-1}(x_i)}]" />  

當loss function是square loss的時候，我們可以得到:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}L(y,&space;F(x))=\frac{1}{2}\sum_{i=0}^{n}(y-F(x_i))^2&space;\Rightarrow&space;\frac{\partial&space;L}{\partial&space;F(x_i)}=&space;-(y-F(x_i))" />

可以很清楚地看到，負梯度(negative gradient)即為殘差(residual)。(注意這裡的殘差和regression內的定義是相同的東西!)  
那麼GBDT的loss function只能使用square loss嗎? No!  

GBDT的核心精神就是將負梯度視為殘差的近似值，並作為新模型擬合用!  
有了這個概念之後，我們就能繼續往下探討。  

# 梯度下降
GBDT的優化仍然是使用gradient descent進行，所以我們先recall一下梯度下降的經典形式。  
(忘記的朋友可以回上一頁觀看Gradient Descent章節)    
<img src="https://latex.codecogs.com/png.image?\dpi{110}\theta^{(t)}&space;=&space;\theta&space;^{(t-1)}&space;-&space;\eta&space;\frac{\partial&space;L}{\partial&space;\theta^{(t-1)}}&space;"  />  

我們可把後面那一項看作是第t次iteration的增量(increment)，由於boosting特性，我們只要收集所有的increment，把它全部加在一起，再與初始值相加就是最終結果。  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\theta_{increment}^{(t)}&space;=&space;-&space;\eta&space;\frac{\partial&space;L}{\partial&space;\theta^{(t-1)}}&space;" />  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\theta_{final}&space;=&space;\theta^{(0)}&space;&plus;&space;\sum_{t=1}^{T}\theta_{increment}^{(t)}&space;" />  

我們將這個概念套用到函數空間上，將theta換成F(x)，這個大寫F就是每一次迭代累積的決策樹模型之和。(因為我們說過boosting模型是加法模型!)  
形式如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}F^{(t)}(x)&space;=&space;F^{(t-1)}(x)&space;&plus;&space;f_t(x)&space;"  />  
這個小寫的f就是剛剛的increments，大寫F就是最終輸出，我們給他x，他output預測類別y:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f_t(x)&space;=&space;-\eta&space;\frac{\partial&space;L}{\partial&space;F^{(t-1)}(x)}&space;\&space;,&space;F(x)&space;=&space;\sum_{t=0}^{T}f_t(x)" title="https://latex.codecogs.com/png.image?\dpi{110}f_t(x) = -\eta \frac{\partial L}{\partial F^{(t-1)}(x)} \ , F(x) = \sum_{t=0}^{T}f_t(x)" />  

後續模型的演算過程，就是把這個負梯度當作真實值y，當前的決策樹模型想辦fit它。(呼應開頭的gradient核心精神)  

# Pseudo Code
我們先列出 GBDT 這個boosting tree加法模型:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}F(x;w)&space;=&space;\sum_{t=0}^{T}f_t(x;w_t)&space;=&space;\sum_{t=0}^{T}\alpha_t&space;h^{(t)}(x;w_t)&space;" />  
右邊的alpha其實就是對應到梯度下降的學習率(learning rate)eta，而我們的目標就是找到一組參數w使得tree h的結果會是負梯度。  

所以整體演算法流程如下:  

input訓練資料集: T = {(x1,y1)...(xN, yN)}，損失函數L(y, F(x))  
output預測類別: F(x)  

**Step 1** - 初始化f0(x)  
**Step 2** - 迴圈  

for t in range(1, T+1):  

  計算負梯度  
  <img src="https://latex.codecogs.com/png.image?\dpi{110}\hat{h}^{(t)}(x_i)=-[\frac{\partial&space;L(y_i,&space;F^{(t-1)}(x_i))}{\partial&space;F^{(t-1)}(x_i)}]&space;,&space;\&space;i=1,2,...,N"  />  
  
  尋找最佳的w參數來建立第t顆樹，注意這裡的目的是要讓h結果與負梯度越相近越好!  
  <img src="https://latex.codecogs.com/png.image?\dpi{110}w^*&space;=&space;\underset{w}{argmin}\sum_{i=1}^{N}(\hat{h}^{(t)}(x_i)-h^{(t)}(x_i))^2"  />  
  
  利用剛剛找到的最佳w建立樹模型並且依據loss function找到最佳的learning rate!  
  <img src="https://latex.codecogs.com/png.image?\dpi{110}\rho^*&space;=&space;\underset{\rho&space;}{argmin}&space;\sum_{i=1}^{N}&space;L(h^{(t)}(x_i),&space;F^{(t-1)}(x_i)&plus;\rho&space;h^{(t)}(x_i,&space;w^*))"  />  
  
  當前模型可以寫成:  
  <img src="https://latex.codecogs.com/png.image?\dpi{110}f_t(x)&space;=&space;\rho^*&space;h^{(t)}(x,&space;w^*))&space;\Rightarrow&space;F^{(t)}(x)&space;=&space;F^{(t-1)}&plus;f_t(x)"/>  
  
**Step 3** - 輸出最新模型F  

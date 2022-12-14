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


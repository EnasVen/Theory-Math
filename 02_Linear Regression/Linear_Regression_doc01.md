# 母體迴歸線與樣本迴歸線
首先要知道母體和樣本迴歸線的差異，在母體中的迴歸線，所有的參數(迴歸係數)都是已知:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E(Y)=\beta_0&plus;\beta_1x_1" />  
上式即為母體迴歸線的描述(也可以寫成E(Y|x))，可以看到beta係數並沒有hat符號(因為已知所以不用估計!)  
每一筆y可以被寫成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_i=\beta_0&plus;\beta_1x_1&plus;e" />  
也就是說真實的y可以被母體迴歸線再加上一個誤差(error)來表示。  
```
特別注意到，在很多書上會把誤差(e)和殘差(epsilon)混淆，e是指母體迴歸線誤差；而epsilon則是樣本迴歸線殘差。  
兩個是不一樣的東西，切記切記!  
```

而樣本迴歸線就不一樣了，由於我們只能夠從部分樣本去推測母體迴歸線，因此就有了估計的環節:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}E(Y|x)=\hat{\beta_0}&plus;\hat{\beta_1}x_1" />  
上式即為樣本迴歸線的描述，可以看到beta係數都有一個hat，代表它是被估計出來的。  
**被什麼估計出來? 被已知數據(樣本)利用統計手法估計出來!**  
這時候每一筆y可以被寫成:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_i=\hat{\beta_0}&plus;\hat{\beta_1}x_1&plus;\varepsilon_i" />  
也就是說真實的y我們"期望"它能被樣本迴歸線再加上一個殘差(epsilon)來表示。  
而epsilon前面那一包beta和x的線性組合，就是E(Y|x)，不過我們會更常用y hat來表示，意思就是這個y值是被估計出來的!  

# 簡單線性迴歸 vs 多元線性迴歸
上面的線性迴歸模型只有1個feature，也就是說只有一個x。  
這時候稱為簡單線性迴歸(simple Linear Regression)。  
而當變數x有多個的時候(假設有p個)，則稱為多元線性迴歸(Multiple Linear Regression):  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_i=\hat{\beta_0}&plus;\hat{\beta_1}x_1&plus;...&plus;\hat{\beta_p}x_p&plus;\varepsilon_i" />  

對於每一個epsilon，我們會假設它服從常態分布，並具備固定的variance:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}\varepsilon_1...\varepsilon_n&space;\overset{iid}{\sim&space;}&space;N(0,\sigma^2)" />

這也是我們實務上在做迴歸的時候，為什麼會去檢測殘差是否常態以及在0附近震盪的原因。  

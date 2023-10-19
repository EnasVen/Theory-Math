為了決定ARIMA(p,d,q)三個參數，通常會透過ACF與PACF圖形做診斷。  

# ACF 自相關函數
ACF代表t時間點與t-k時間點的相關性，公式如下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}ACF(k)=\frac{Cov(X_t,X_{t-k})}{Var(X_t)}"/>  
k=0的時候就是ACF值為1，接著會逐漸遞減，當然值有可能是負的。  
需要注意的一點是，分母原先是t時間與t-k時間的std相乘，又因為時序資料在穩態假設下，所以variance固定，兩個std相乘自然就會是variance。  
通常我們會觀察ACF圖形找到cut point來決定MA(q)需要幾階，這是因為ACF能顯示t時間與各個歷史時間點之間的相關性。  

# PACF
PACF代表t時間點和t-k時間點的絕對相關性，公式如下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}PACF(k)=\frac{Cov(X_t,X_{t-k})-\sum_{i=1}^{k-1}PACF(i)*Cov(X_{t-i},X_{t-k})}{1-\sum_{i=1}^{k-1}PACF(i)*PACF(i)}"/>  
因為ACF沒辦法排外中間時間點的影響力，舉個例子，時間點t和t-k的相關性有可能是中間的t-k+n所貢獻，因此公式會把1~k-1的PACF都扣掉。  
通常我們會觀察PACF圖形找到cut point來決定AR(p)需要幾階。  

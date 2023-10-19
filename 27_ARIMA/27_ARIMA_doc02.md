# AR model
AR代表自迴歸(Auto-Regressive)，代表使用過去時間點當作變量來預測當前時間點，一個AR(p)模型可以被表示成以下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_t=c&plus;\phi_1&space;y_{t-1}&plus;\phi_2&space;y_{t-2}&plus;...&plus;\phi_p&space;y_{t-p}&plus;\epsilon_t"/>  
代表t時間的y可以被表示成前p的時間點的線性組合，再加上offset constant與t時間的誤差項epsilon。  

# MA model
MA代表移動平均(Moving-Average)，但不是使用t時間往前往後q時間單位來做平均，這種作法稱為平滑化，是對於歷史時序資料的循環趨勢；而MA model則是用於預測未來值。  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_t=c&plus;\theta_1\epsilon_{t-1}&plus;\theta_2\epsilon_{t-2}&plus;...&plus;\theta_q\epsilon_{t-q}&plus;\epsilon_t"/>  
代表t時間的y可以被表示成歷史預測誤差的線性組合，再加上offset constant與t時間的誤差項epsilon。  

# AR Integreted MA 
ARIMA模型具備三個參數: p、d、q，分別對應AP 、diff、MA三種模型的參數。通常以ARIMA(p,d,q)表示，寫成數學式子如下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y'_t=c&plus;\phi_1'y_{t-1}'&plus;...&plus;\phi_p'y_{t-p}'&plus;\theta_1\epsilon_{t-1}&plus;...&plus;\theta_q\epsilon_{t-q}&plus;\epsilon_t"/>  
這裡的y'代表原始的數據y經過差分(有可能不只一次)後的結果。  

透過上一份Markdown的延遲算子B，我們可以將式子簡化如下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}(1-\phi_1B-...-\phi_pB^p)(1-B)^dy_t=c(1&plus;\theta_1B&plus;...&plus;\theta_qB^q)\epsilon_t"/>  
其實就是把AR項移到左邊相減，右邊保留MA項，並且把epsilon的時間項套用延遲算子B。  



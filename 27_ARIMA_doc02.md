# AR model
AR代表自迴歸(Auto-Regressive)，代表使用過去時間點當作變量來預測當前時間點，一個AR(p)模型可以被表示成以下:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_t=c&plus;\phi_1&space;y_{t-1}&plus;\phi_2&space;y_{t-2}&plus;...&plus;\phi_p&space;y_{t-p}&plus;\epsilon_t"/>  
代表t時間的y可以被表示成前p的時間點的線性組合，再加上offset constant與t時間的誤差項epsilon。  

# MA model
MA代表移動平均(Moving-Average)，但不是使用t時間往前往後q時間單位來做平均，這種作法稱為平滑化，是對於歷史時序資料的循環趨勢；而MA model則是用於預測未來值。  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}y_t=c&plus;\theta_1\epsilon_{t-1}&plus;\theta_2\epsilon_{t-2}&plus;...&plus;\theta_p\epsilon_{t-p}&plus;\epsilon_t"/>  
代表t時間的y可以被表示成歷史預測誤差的線性組合，再加上offset constant與t時間的誤差項epsilon。  


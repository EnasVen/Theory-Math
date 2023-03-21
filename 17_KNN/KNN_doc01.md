# 理論推導
KNN的概念非常簡單，透過尋找數據內臨近的點來進行分類。  
只要定義metric、k值後，對k個樣本內的多數類別進行投票就完事了!  

<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Given&space;\&space;data&space;\&space;&space;:&space;\{&space;(x_1,y_1),...,(x_N,y_N)\}&space;\&space;y_i\in&space;\{1,2,...C\}&space;\&space;\forall&space;i=1,2,...,N" title="https://latex.codecogs.com/png.image?\inline \dpi{110}Given \ data \ : \{ (x_1,y_1),...,(x_N,y_N)\} \ y_i\in \{1,2,...C\} \ \forall i=1,2,...,N" />  

對於選定的資料點t，我們可以找到k個與他距離最近的資料點:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}N_k=\{(x_i,y_i)\}&space;\&space;i=1,2,...r&space;\&space;r\leq&space;N" title="https://latex.codecogs.com/png.image?\inline \dpi{110}N_k=\{(x_i,y_i)\} \ i=1,2,...r \ r\leq N" />  

則對於該資料點t，我們透過多數決的方式來判定它的類別:  
<img src="https://latex.codecogs.com/png.image?\inline&space;\dpi{110}Y_t=\underset{c_j}{argmax}\sum_{x_i\in&space;N_k}I(y_i=c_j)&space;\&space;where&space;\&space;i=1,2,...,k&space;\&space;j=1,2,...,C" />  
需注意上式的I為indicator function!  

# 如何選取最好的k?
由於k值的選擇會大幅影響分類效果，如果選太小(k=1)，當臨近樣本為噪音時會產生分類錯誤；如果選太大(k=N)，距離較遠的樣本又會影響分類正確性。  
所以實務上通常使用cross-validation來驗證最佳k值。  

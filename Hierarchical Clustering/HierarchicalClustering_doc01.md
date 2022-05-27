# 分群 vs 分類  
**分群**:從一片未知(no prior)找尋相似的群體(small distance)  
(例如:K-means、Density-based clustering、Model-based clustering...等等)  

**分類**:從已知的資訊(labeled )找尋最佳的分類法，用以預測(predict)新物件  
(例如:Logistic Regression、SVM、Random Forest...等等)  

# 階層式分群種類  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Hierarchical%20Clustering/Hie_Img01.png)  

# 點距限制
給定多維空間兩點x和y，我們認為一個好的距離度量應該具備以下性質 :  
<img src="https://latex.codecogs.com/png.image?\dpi{110}x^T=[x_1,...,x_p]&space;;&space;y^T=[y_1,...,y_p]"/>  
1.<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)=d(y,x)" />  
2.<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)>0&space;,&space;\forall&space;x\neq&space;y"/>  
3.<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)=0&space;,&space;\forall&space;x&space;=&space;y"/>  
4.<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)\leq&space;d(x,z)&plus;d(z,y)"/>  
上述其實就是數學對metric的定義!  

# 常用點距量測  
Euclidean距離:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)=\sqrt{(x-y)^T(x-y)}"/>  
Minkowski 距離:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)=\sum_{i=1}^{p}((\left|x_i-y_i\right|)^m)^{\frac{1}{m}}"/>  
Manhattan距離:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}d(x,y)=\sum_{i=1}^{p}\left|x_i-y_i\right|"/>  
  
# Linkage  
在階層式分群內，Linkage為測量群距的度量方法。常用的有3種:  
**single linkage**:採用最小距離  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Hierarchical%20Clustering/Hie_Img02.png)  
**complete inkage**:採用最大距離  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Hierarchical%20Clustering/Hie_Img03.png)  
**average linkage**:採用平均距離  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Hierarchical%20Clustering/Hie_Img04.png)  
  
# Example  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Hierarchical%20Clustering/Hie_Img05.png)  

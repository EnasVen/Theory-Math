# Entropy(熵)  
簡易解釋 : 將資訊量化，代表一個「事件」所包含的訊息量。  
數學解釋 : 衡量資料(隨機變數)的凌亂程度(資訊量/不確定性)。  
定義 : 隨機變數X的Entropy定為  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}H(X)=E(I(X))=E(-ln(P(X)))=\sum_{i}^{}-P(x_i)ln(P(x_i))"/>  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/05_Information%20Theory/Information_Img01.png)  

下面我會將Information Theory內相關的指標定義列出來!  
  
# Joint Entropy  
數學解釋 : 多個隨機變數的不確定性；或者說量測聯合分布的不確定性。  
定義:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}H(X,Y)=\sum_{x&space;\in&space;X}\sum_{y&space;\in&space;Y}-p(x,y)ln(p(x,y))=E(ln\frac{1}{p(X,Y)})" />  
  
# Conditional Entropy  
數學解釋 : 已知隨機變數X下，期望隨機變數Y的不確定性。  
定義:  
  
<img src="https://latex.codecogs.com/png.image?\dpi{110}H(X,Y)=H(X,Y)-H(X)&space;\\&space;=-\sum_{xy}p(x,y)ln(p(x,y))&plus;\sum_{x}p(x)ln(p(x))&space;\\&space;=&space;-\sum_{xy}p(x,y)ln(p(x,y))&plus;\sum_{x}(\sum_{y}p(x,y))&space;ln(p(x,y)))&space;\\&space;=&space;-\sum_{xy}p(x,y)[ln(p(x,y)-ln(p(x)))]&space;\\&space;=&space;-\sum_{xy}p(x,y)ln(p(y|x|))" />  
  
第一式可以透過Joint Entropy的定義推得!  

# Relative Entropy  
在機器學習稱作KLD(Kullback-Leibler divergence) 。
簡易解釋 : 量測兩個隨機變數的距離。  
數學解釋 : 用來衡量當真實機率分布為P(x)時，和機率分布Q(x)的差異。  
定義:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}D_{KL}(P||Q)=\sum_{x}-p(x)*ln(\frac{q(x)}{p(x)})"  />  

補充 : information gain(資訊增益):  
<img src="https://latex.codecogs.com/png.image?\dpi{110}I(X,Y)=D_{KL}(P(X,Y)||P(X)P(Y))=&space;H(Y)&space;-&space;H(Y|X|)" />  
(在已知X的情況下觀察到Y的不確定性減少了多少)  
# Cross Entropy  
簡易解釋 : 在機器學習中用來衡量真實分布與預測分布之間的差異。  
數學解釋 : 由KLD變化得到，實務上使用Cross Entropy較多。(因為容易計算!)  
定義:  
  
<img src="https://latex.codecogs.com/png.image?\dpi{110}D_{KL}(P||Q)&space;\\=\sum_{x}-p(x)ln(\frac{q(x)}{p(x)})\\=\sum_{x}p(x)ln(\frac{p(x)}{q(x)})\\=\sum_{x}p(x)ln(p(x))-\sum_{x}p(x)ln(q(x))&space;\\=&space;-H(X)&space;&plus;&space;CrossEntropy(P,Q)" />
  
因此量測KLD等價於量測 CrossEntropy !!  

# Gini Impurity  
數學解釋 : 用來描述資料集獲系統的混亂程度(不純度高低)，越大代表資料越混雜。  
定義:  
假設資料集S含有n個類別，pi為各類別比例。  
<img src="https://latex.codecogs.com/png.image?\dpi{110}Gini(S)=\sum_{i=1}^{n}p_i(1-p_i)=1-\sum_{i=1}^{n}p_i^2"/>
# Gini Gain  
數學解釋 : 用來計算分類的好壞程度(不純度差距)，越大越好(代表分類越純)。
定義:  
假設資料集S使用某個特徵A來進行分類，共分成多個子集Si  
<img src="https://latex.codecogs.com/png.image?\dpi{110}GiniGain(S,A)=Gini(S)-Gini(S,A)=Gini(S)-\sum_{i=1}^{n}\frac{len(S_i)}{len(S)}*Gini(S_i)"/>
  
下面提供兩個例子計算Gini Impurity 與 Entropy:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/05_Information%20Theory/Information_Img02.png)  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/05_Information%20Theory/Information_Img03.png)  

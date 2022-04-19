# Entropy(熵)  
簡易解釋 : 將資訊量化，代表一個「事件」所包含的訊息量。  
數學解釋 : 衡量資料(隨機變數)的凌亂程度(資訊量/不確定性)。  
定義 : 隨機變數X的Entropy定為  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}H(X)=E(I(X))=E(-ln(P(X)))=\sum_{i}^{}-P(x_i)ln(P(x_i))"/>  
  
下面我會將Information Theory內相關的指標定義列出來!  
  
# Joint Entropy  
數學解釋 : 多個隨機變數的不確定性；或者說量測聯合分布的不確定性。
定義 :
  
# Conditional Entropy  
數學解釋 : 已知隨機變數X下，期望隨機變數Y的不確定性。
定義 :
  
# Relative Entropy  
在機器學習稱作KLD(Kullback-Leibler divergence) 。
簡易解釋 : 量測兩個隨機變數的距離。
數學解釋 : 用來衡量當真實機率分布為P(x)時，和機率分布Q(x)的差異。
定義 :
補充 : information gain(資訊增益) ：  
  
# Cross Entropy  
簡易解釋 : 在機器學習中用來衡量真實分布與預測分布之間的差異。
數學解釋 : 由KLD變化得到，實務上使用Cross Entropy較多。(因為容易計算!)
定義 :
  
# Gini Impurity  


# Gini Gain  

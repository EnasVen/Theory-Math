PCA為Principle Component Analysis的縮寫，意即主成分分析。  
透過變數之間的線性組合解釋整體共變異矩陣，找出占比最多的主成分以達到維度縮減的目的。  
那麼，為何要做維度縮減的動作呢?  
主要原因是當維度上升(例如:feature爆多)，資料空間會變得相當稀疏(sparse)，使模型預測能力下降。  
  
舉例:  
假設我們有10筆資料，分別是貓狗的圖片；我們想要找到一個分類器(model)能夠辨識貓狗。  
現在有3個特徵，其特徵範圍均為5。  
當使用1個特徵進行分類時，效果很差，貓狗都混在x軸上難以區分。  
當使用2個特徵進行分類時，效果好些，但我們仍找不到一條直線將貓狗數據完美區隔。  
當使用3個特徵進行分類時，效果最好，我們可以找到一個超平面將貓狗數據在3維空間區隔開來。  
  
看起來維度越高，預測能力越好，但樣本在特徵空間的密度開始大幅下降：  
使用1個特徵時：樣本密度 10/5=2  
使用2個特徵時：樣本密度 10/25=0.4  
使用3個特徵時：樣本密度 10/125=0.08  
...  
當特徵越多，樣本密度趨近於0，因此，我們可以很容易在特徵空間找到一個超平面將貓狗數據區分開。  
也就是說，分類器在訓練的時候表現都會相當良好(因為很難分錯)。  
  
然而，當我們將高維的超平面投影到低維時，會發現數據並非呈現線性可分。  
這是因為模型學習了過多樣本數據的異常特徵(噪音)，整體泛化能力很差。  
這個結果在機器學習中被稱為過擬合(over-fitting)，也是維度災難的表現。  
  
以下計算避免資料過於稀疏，所需要的數據量：  
假設第1個特徵的範圍為(0,1)，我們希望訓練資料的特徵值範圍佔整體特徵值範圍的20%。  
那麼在1維的case下，訓練樣本的數量為整體數量的20%。  
而在2維的case下，所需訓練樣本數量則為44.72%。(因為 <img src="https://latex.codecogs.com/gif.image?\dpi{110}\sqrt{0.2}\doteq&space;0.4472" title="https://latex.codecogs.com/gif.image?\dpi{110}\sqrt{0.2}\doteq 0.4472" />)  
在3維的case下，所需訓練樣本數量則為58.48%。(因為 <img src="https://latex.codecogs.com/gif.image?\dpi{110}0.2^{\frac{1}{3}}\doteq&space;0.5848" title="https://latex.codecogs.com/gif.image?\dpi{110}0.2^{\frac{1}{3}}\doteq 0.5848" />)  
  
也就是說，當訓練樣本數量固定時，貿然增加特徵數量會導致維度災難。  
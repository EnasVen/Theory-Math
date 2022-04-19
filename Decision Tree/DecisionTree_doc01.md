# 類型(Types)
決策樹分為以下兩種型態:  
1.迴歸樹:用來預測實際數值(例如：消費者年齡、廣告點擊率…)  
2.分類樹:用來分類標籤資料(例如：垃圾郵件、貸款信用…)  
  
兩者具有以下的差異:  
第1個差異：迴歸樹在每一個葉節點都會得到預測值，代表該節點之平均。  
第2個差異：迴歸樹在衡量最佳切割屬性和切割值使用平方誤差而非Gini Impurity。(忘記Gini Index的可以先閱讀Information Theory~)  
 
決策樹常使用Entropy、Gini Impurity和MSE計算分割的criterion。  
根據分割前後，下降最多的指標值就是最佳分割屬性!  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Decision%20Tree/DecisionTree_Img03.png)  
  
# 發展史(History)
決策樹一路改良的歷史過程如下:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Decision%20Tree/DecisionTree_Img01.png)  
目前最常用的是CART。  
  
# 修剪(Prune)  
由於決策樹在分裂上採取貪婪擴張的策略，導致模型容易過擬合(overfitting)。因此修剪(pruning)變成一個重要的步驟，降低過度配適訓練資料的情況。  
預修剪(pre-pruning)：提前設定閥值(**註1**)讓決策樹停止過度生長。  
後修剪(post-pruning)：讓決策樹完全生長後再根據error rate(**註2**)進行修剪。  
  
  
我整理了一張表格，可以清楚看到各歷程演算法的主要手法:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Decision%20Tree/DecisionTree_Img02.png)  
(註1) 預剪枝的條件如:樹的深度、節點類別個數…等。  
(註2) errror rate有其閥值(顯著水準0.25)，使用z檢定來判斷是否需要修剪。  
(註3) ID3使用資訊增益會造成獨立指標的過度分類情形。(例如:產品序號)  
(註4) C5.0使用boosting手法，其演算法未公開。  
  
 # Example  
 以下自行建構了一個例子供參考，我們選用的分割指標為Gini Impurity:  
 ![Image](https://github.com/EnasVen/Theory-Math/blob/main/Decision%20Tree/DecisionTree_Img04.png)  

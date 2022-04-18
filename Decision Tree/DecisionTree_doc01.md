# 決策樹
決策樹分為以下兩種型態:  
1.迴歸樹:用來預測實際數值(例如：消費者年齡、廣告點擊率…)  
2.分類樹:用來分類標籤資料(例如：垃圾郵件、貸款信用…)  
  
兩者具有以下的差異:  
第1個差異：迴歸樹在每一個葉節點都會得到預測值，代表該節點之平均。  
第2個差異：迴歸樹在衡量最佳切割屬性和切割值使用平方誤差而非Gini。  
 
決策樹常使用Entropy、Gini Impurity和MSE計算分割的criterion。  
根據分割前後，下降最多的指標值就是最佳分割屬性!  
![Image]("https://github.com/EnasVen/Theory-Math/blob/main/Decision%20Tree/DecisionTree_Img03.png")  
  

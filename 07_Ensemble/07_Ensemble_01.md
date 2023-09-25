# 集成手法
Ensemble Learning是一種機器學習的技術，目的通過結合多個不同模型，提高整體模型預測力和泛化能力。  
核心思想是將多個弱學習器組合成一個強學習器，以降低過擬合風險，提高模型robustness。  
以下會簡介Ensemble常用的三種手法：bagging、boosting以及stacking。  

# Bagging (Boostrap Aggregating)
透過Boostrap手法對原始數據重複取樣(取後放回)成相同size的數據集，並訓練多個弱學習器透過平均、投票的方式進行預測、迴歸。  
最有名的Bagging演算法即為隨機森林(Random Forest)，不過RF除了對row進行resample，對column也進行resample(抽一部分feature建tree)。  

# Boosting
Boosting是一種迭代的方法，整體模型會關注上一次的sub-tree結果進行修正，放大錯誤樣本的權重，好讓下一次的模型能夠針對分類或預測誤差較大的樣本重點改善。  
最有名的當屬AdaBoost和Gradient Boosting。而GBDT後又延伸很多現代ML模型，例如: 改良GBDT的XGBoost、擊敗XGB的LightGBM...等等。  

# Stacking
上述兩種是Ensemble的入門款，更高級的技術就要提到Stacking了。  
透過將不同基礎模型的預測整合，並使用高階模型將這些基礎模型的輸出當成輸入，進行預測。  
這樣的方法讓高階模型能夠從基礎模型的預測中學到更好的組合策略。  


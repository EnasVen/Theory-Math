# Ward’s Hierarchical Clustering Method  
Ward提出使用error sum of square來提高分群準確度:  
1.給定群數k  
<img src="https://latex.codecogs.com/png.image?\dpi{110}ESS_k=\sum_{i=1}^{N_k}(x_i-\bar{x})^T(x_i-\bar{x})"/>  
2.Nk為第k群的觀察值數量;xi為每一個觀察值，而x-bar為群平均
  
# Example  
下面實際使用ess來做階層式分群:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/Hierarchical%20Clustering/Hie_Img06.png)  

# 最佳化  
有了分群規則，我們肯定會想知道: **到底要分幾群才是最好的呢?**  
核心的概念是:最大組間的變異，同時最小化組內的變異。  
這個概念有一個專有名詞叫 Wilk’s Lambda: (with-in) / (with-in) + (with-out)  
  
而整體ess的指標可以用這個來表示:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}ESS_{Total}=\sum_{i=1}^{K}\sum_{i=1}^{N_k}(x_{ki}-\bar{x_k})^T(x_{ki}-\bar{x_k})" />  
  
那麼，有沒有更好的指標呢?  有的!  
Silhouette值用來衡量每一點的分群效果:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}s_i=\frac{(b_i-a_i)}{max(a_i,b_i)}"/>  
a值表示點i到群內每一個點的平均距離。  
b值表示點i到所有群的最小距離。  
Silhouette的值會在[-1,1]之間，越靠近-1表示該點分得越差。  

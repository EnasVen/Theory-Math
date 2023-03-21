## Density-Based Spatial Clustering of Applications with Noise
這個演算法顧名思義，就是用密度去做分群，把密度大(較密集)的歸類在同一個cluster。  
聽起來也挺合理的，畢竟越靠近的點簇歸屬在同一族群直覺上也make sense!  
而名稱後面的Noise，則是在雜訊點的加入仍能做出效果不錯的分群，並能標示出雜訊。  

下圖比較一下density base和KMeans的差異，可以看到對KMeans無法偵測離群值，對每一點都會進行分群。  
而且KMeans除了要指定K之外，它的泛用性被資料分布侷限。  
反而是density base的算法更robust。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/18_DBSCAN/DBSCAN_pic05.png)

## 名詞解析
在DBSCAN內有一些名詞需要先被定義，後面才能順利進行:  
1. `metric`: 常用的距離函數，你可以選擇歐式距離、馬氏距離、曼哈頓距離...etc。  
2. `epsilon`: 實數，用來建立樣本點的鄰域(neighborhood)。  
3. `minimum point`:　整數，用來定義核心/邊界點。  
4. `core point`: 鄰域內的樣本數若大於minimum point，則稱為核心點。  
5. `border point`: 鄰域內的樣本數若小於minimum point，則稱為邊界點。  
6. `noise point`:　噪音點，不屬於任何鄰域之樣本。
7. `直達性質`: 當樣本X在核心樣本Y的鄰域內，則Y到X是有直達性質。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/18_DBSCAN/DBSCAN_pic01.png)
8. `傳導性質`: 當核心樣本Y到核心樣本P3具有直達性質；而P3又對**邊界樣本**P2有直達性質，則稱Y到P2有傳導性質。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/18_DBSCAN/DBSCAN_pic02.png)
9. `連接性質`: 當核心樣本O到邊界樣本Y以及X分別具有傳導性質，則稱X和Y具有連接性質。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/18_DBSCAN/DBSCAN_pic03.png)

有了以上的定義後，我們可以推論得到:  
對於一系列具備傳導性質的點來說，其鄰域範圍內的點都具備連接性質。  
這些具備連接性質的點所形成的集合在DBSCAN內會被歸屬到同一群內。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/18_DBSCAN/DBSCAN_pic00.png)

## 演算過程
DBSCAN會隨機挑選一個點作為核心點，接著利用minimum point和epsilon來獲得那些具備連接性質的點，接著給這些點集合一個cluster編號。  
接著尋找沒有被賦予cluster編號的樣本，在用同樣的方法進行，直到每一個樣本都獲得cluster(同時標記noise樣本點)。  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/18_DBSCAN/DBSCAN_pic04.png)

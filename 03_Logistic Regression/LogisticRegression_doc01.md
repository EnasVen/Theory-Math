# 相對風險(Relative Risk)
在生物統計內，有兩種知名的研究方法，分別為Cohort Study以及Case Control:  

![Image](https://github.com/EnasVen/Theory-Math/blob/main/03_Logistic%20Regression/CohortStudy.png)  

假設今天想研究吃維他命A是否會對死亡造成影響，我們分別隨機抽樣100人，分2組，一組有吃維他命A，另一組沒有。  
接著實驗持續10年，看看到底這些人當中死亡了幾個。  

因此我們定義相對風險的指標RR為:  
<img src="https://latex.codecogs.com/svg.image?Pr(Dead&space;|&space;VitA)&space;=&space;10/100&space;=&space;0.1&space;\\Pr(Dead&space;|&space;non-VitA)&space;=&space;20/100&space;=&space;0.2&space;\\\Rightarrow&space;\hat{RR}&space;=&space;\frac{Pr(Dead&space;|&space;VitA)}{Pr(Dead&space;|&space;non-VitA)}&space;&space;=&space;\frac{0.1}{0.2}&space;=&space;0.5" title="Pr(Dead | VitA) = 10/100 = 0.1 \\Pr(Dead | non-VitA) = 20/100 = 0.2 \\\Rightarrow \hat{RR} = \frac{Pr(Dead | VitA)}{Pr(Dead | non-VitA)} = \frac{0.1}{0.2} = 0.5" />  

我們推論: 有吃維他命A的死亡率比沒吃的低50%  

# 勝算比(Odds Ratio)
然而，世界上沒有這麼美好的事情。  
一個實驗如果要做10年才能拿到數據，太不切實際了。  
因此研究員決定從近10年內死亡與存活的數據中篩選有吃與沒吃維他命A的人。  
也就是抓100個已死亡的資料與100個存活的資料來篩選裡面有無吃維他命A的人數:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/03_Logistic%20Regression/CaseControl.png)  

但是現在的樣本抽取方法，就**不能**按照RR的方式來計算!  
理由是原先的RR為固定總試驗數(有吃維他命A的人數)下計算死亡(p)與存活(1-p)的次數，因此是一個二項分布。  
而現在有吃維他命A的人數是來自不同母體的數據，並不是fix。 

所以我們必須產生另一種指標來替代RR，首先我們計算:  
<img src="https://latex.codecogs.com/svg.image?p_1&space;=&space;Pr(Dead&space;|&space;VitA)&space;\&space;;&space;\&space;1-p_1&space;=&space;Pr(Alive&space;|&space;VitA)&space;\\p_2&space;=&space;Pr(Dead&space;|&space;nonVitA)&space;\&space;;&space;\&space;1-p_2&space;=&space;Pr(Alive&space;|&space;nonVitA)\\\Rightarrow&space;&space;Odds_1&space;=&space;\frac{p_1}{1-p_1}&space;\&space;&space;;&space;\&space;Odds_2&space;=&space;\frac{p_2}{1-p_2}&space;\\&space;\Rightarrow&space;&space;OddsRatio&space;=&space;\frac{p_1/1-p_1}{p_2/1-p_2}" title="p_1 = Pr(Dead | VitA) \ ; \ 1-p_1 = Pr(Alive | VitA) \\p_2 = Pr(Dead | nonVitA) \ ; \ 1-p_2 = Pr(Alive | nonVitA)\\\Rightarrow Odds_1 = \frac{p_1}{1-p_1} \ ; \ Odds_2 = \frac{p_2}{1-p_2} \\ \Rightarrow OddsRatio = \frac{p_1/1-p_1}{p_2/1-p_2}" />  

得到Odds Ratio等於兩個Odds相除。  
顯然地，RR的方向和Odds Ratio相同(RR大於/小於/等於 1的時候，OR也會大於/小於/等於 1)  

接著我們來測試一下這個新指標是否能夠勝任:  

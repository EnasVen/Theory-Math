# 向量投影解析
其實SVM在求點到超平面的距離，就用到向量投影的技巧!  
如下圖:  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/14_SVM/SVM_Img01.png)  

我們要求的是點B到超平面的距離就是圖內的虛線長度。  
由於向量可以平移，因此虛線長度其實就等於AB向量在超平面法向量上投影的長度。  
兩向量之間的夾角我們叫做theta，這個問題也就轉換成求解向量投影長度!!  

Recall 向量投影:  
<img src="https://latex.codecogs.com/svg.image?\\Projection&space;Length&space;=&space;\left\|&space;\vec{AB}&space;\right\|&space;cos(\theta&space;)&space;=&space;\frac{\left<&space;\vec{AB}&space;,&space;n&space;\right>}{\left\|&space;n&space;\right\|}&space;\\Projection&space;Vector&space;=&space;\frac{\left<&space;\vec{AB}&space;,&space;n&space;\right>&space;\bullet&space;&space;n}{\left\|&space;n&space;\right\|^{2}}&space;" title="\\Projection Length = \left\| \vec{AB} \right\| cos(\theta ) = \frac{\left< \vec{AB} , n \right>}{\left\| n \right\|} \\Projection Vector = \frac{\left< \vec{AB} , n \right> \bullet n}{\left\| n \right\|^{2}} " />

假設超平面為 px+qy+rz+d = 0，我們的法向量n即為(p,q,r)，因此:
<img src="https://latex.codecogs.com/svg.image?\left<&space;\vec{AB}&space;,&space;n&space;\right>&space;=&space;\left<&space;(b_x-a_x&space;,&space;b_y-a_y&space;,&space;b_z-a_z)&space;,&space;(p,q,r)&space;\right>&space;=&space;b_xp&plus;b_yq&plus;b_zr-(a_xp&plus;a_yq&plus;a_zr)&space;=&space;b_xp&plus;b_yq&plus;b_zr&space;-&space;(-d)&space;=&space;b_xp&plus;b_yq&plus;b_zr&space;&plus;&space;d&space;" title="\left< \vec{AB} , n \right> = \left< (b_x-a_x , b_y-a_y , b_z-a_z) , (p,q,r) \right> = b_xp+b_yq+b_zr-(a_xp+a_yq+a_zr) = b_xp+b_yq+b_zr - (-d) = b_xp+b_yq+b_zr + d " />

分母就是法向量n的長度，因此組合後我們就得到以前高中學到的「點到平面的距離」:  
<img src="https://latex.codecogs.com/svg.image?\frac{\left|b_xp&plus;b_yq&plus;b_zr&space;&plus;&space;d&space;\right|}{\sqrt{p^2&plus;q^2&plus;r^2}}" title="\frac{\left|b_xp+b_yq+b_zr + d \right|}{\sqrt{p^2+q^2+r^2}}" />

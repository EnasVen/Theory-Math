# What is BackPropagation ?
所有深度學習網絡的權重更新都基於反向傳播法，而說穿了就是微積分的連鎖率(Chain Rule)!  
推導過程如下:

定義符號:
1. Input Layer : x_1 , x_2 , ... , x_n  
2. Hidden Layer l : n_11 , n_12 , ... , n_lN(l)  
3. Output Layer O : O_1 , O_2 , ... O_N(m)  
4. Z_l = 第l層隱藏層的input  
5. a_l = 第l層隱藏層的output  

首先，對於隱藏層l(小寫L)來說，我們來看在這層上，每一個Neuron的input接收值Z會是多少:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\\z_{1}^{(l)}&space;=&space;w_{11}^{(l)}a_{1}^{(l-1)}&plus;w_{21}^{(l)}a_{2}^{(l-1)}&plus;...&plus;w_{N^{(l-1)}1}^{(l)}a_{N^{(l-1)}}^{(l-1)}&space;\\z_{2}^{(l)}&space;=&space;w_{12}^{(l)}a_{1}^{(l-1)}&plus;w_{22}^{(l)}a_{2}^{(l-1)}&plus;...&plus;w_{N^{(l-1)}2}^{(l)}a_{N^{(l-1)}}^{(l-1)}&space;\\&space;...&space;\\z_{N^{(l)}}^{(l)}&space;=&space;w_{1N^{(l)}}^{(l)}a_{1}^{(l-1)}&plus;w_{2N^{(l)}}^{(l)}a_{2}^{(l-1)}&plus;...&plus;w_{N^{(l-1)}N^{(l)}}^{(l)}a_{N^{(l-1)}}^{(l-1)}&space;" title="\\z_{1}^{(l)} = w_{11}^{(l)}a_{1}^{(l-1)}+w_{21}^{(l)}a_{2}^{(l-1)}+...+w_{N^{(l-1)}1}^{(l)}a_{N^{(l-1)}}^{(l-1)} \\z_{2}^{(l)} = w_{12}^{(l)}a_{1}^{(l-1)}+w_{22}^{(l)}a_{2}^{(l-1)}+...+w_{N^{(l-1)}2}^{(l)}a_{N^{(l-1)}}^{(l-1)} \\ ... \\z_{N^{(l)}}^{(l)} = w_{1N^{(l)}}^{(l)}a_{1}^{(l-1)}+w_{2N^{(l)}}^{(l)}a_{2}^{(l-1)}+...+w_{N^{(l-1)}N^{(l)}}^{(l)}a_{N^{(l-1)}}^{(l-1)} " />

這裡的w即為權重，而下標由左至右兩個數i,j分別代表l-1(前一層)層的第i個神經元連接到第l層(當層)的第j個神經元。  
N的上標(l)為第l層的神經元個數。  

上面的式子可以簡寫成矩陣型態：  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\begin{bmatrix}z_{1}^{(l)}\\...&space;\\z_{N^{(l)}}^{(l)}\\\end{bmatrix}&space;=&space;\begin{bmatrix}w_{11}^{(l)}&space;&&space;w_{21}^{(l)}&space;&&space;w_{31}^{(l)}&space;&&space;...&space;&&space;w_{N^{(l-1)}1}^{(l)}&space;\\...&space;&&space;&space;&&space;&space;&&space;&space;&&space;&space;\\w_{1N^{(l)}}^{(l)}&space;&&space;w_{2N^{(l)}}^{(l)}&space;&&space;w_{3N^{(l)}}^{(l)}&space;&&space;...&space;&&space;w_{N^{(l-1)}N^{(l)}}^{(l)}&space;\\\end{bmatrix}\begin{bmatrix}a_{1}^{(l-1)}\\...&space;\\a_{N^{(l-1)}}^{(l-1)}\\\end{bmatrix}&plus;\begin{bmatrix}b_{1}^{(l)}\\...&space;\\b_{N^{(l)}}^{(l)}\\\end{bmatrix}" title="\begin{bmatrix}z_{1}^{(l)}\\... \\z_{N^{(l)}}^{(l)}\\\end{bmatrix} = \begin{bmatrix}w_{11}^{(l)} & w_{21}^{(l)} & w_{31}^{(l)} & ... & w_{N^{(l-1)}1}^{(l)} \\... & & & & \\w_{1N^{(l)}}^{(l)} & w_{2N^{(l)}}^{(l)} & w_{3N^{(l)}}^{(l)} & ... & w_{N^{(l-1)}N^{(l)}}^{(l)} \\\end{bmatrix}\begin{bmatrix}a_{1}^{(l-1)}\\... \\a_{N^{(l-1)}}^{(l-1)}\\\end{bmatrix}+\begin{bmatrix}b_{1}^{(l)}\\... \\b_{N^{(l)}}^{(l)}\\\end{bmatrix}" />

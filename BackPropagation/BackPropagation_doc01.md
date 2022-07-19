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

# What is BackPropagation ?
所有深度學習網絡的權重更新都基於反向傳播法，而說穿了就是微積分的連鎖律(Chain Rule)!  
大神文獻參考: https://zhuanlan.zhihu.com/p/40761721  

# Proof
定義符號:
1. Input Layer : x_1 , x_2 , ... , x_n  
2. Hidden Layer l : n_11 , n_12 , ... , n_lN(l)  
3. Output Layer O : O_1 , O_2 , ... O_N(m)  
4. Z_l = 第l層隱藏層的input  
5. a_l = 第l層隱藏層的output  

首先，對於隱藏層l(小寫L)來說，我們來看在這層上，每一個Neuron的input接收值Z會是多少:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\\z_{1}^{(l)}&space;=&space;w_{11}^{(l)}a_{1}^{(l-1)}&plus;w_{21}^{(l)}a_{2}^{(l-1)}&plus;...&plus;w_{N^{(l-1)}1}^{(l)}a_{N^{(l-1)}}^{(l-1)}&space;\\z_{2}^{(l)}&space;=&space;w_{12}^{(l)}a_{1}^{(l-1)}&plus;w_{22}^{(l)}a_{2}^{(l-1)}&plus;...&plus;w_{N^{(l-1)}2}^{(l)}a_{N^{(l-1)}}^{(l-1)}&space;\\&space;...&space;\\z_{N^{(l)}}^{(l)}&space;=&space;w_{1N^{(l)}}^{(l)}a_{1}^{(l-1)}&plus;w_{2N^{(l)}}^{(l)}a_{2}^{(l-1)}&plus;...&plus;w_{N^{(l-1)}N^{(l)}}^{(l)}a_{N^{(l-1)}}^{(l-1)}&space;" title="\\z_{1}^{(l)} = w_{11}^{(l)}a_{1}^{(l-1)}+w_{21}^{(l)}a_{2}^{(l-1)}+...+w_{N^{(l-1)}1}^{(l)}a_{N^{(l-1)}}^{(l-1)} \\z_{2}^{(l)} = w_{12}^{(l)}a_{1}^{(l-1)}+w_{22}^{(l)}a_{2}^{(l-1)}+...+w_{N^{(l-1)}2}^{(l)}a_{N^{(l-1)}}^{(l-1)} \\ ... \\z_{N^{(l)}}^{(l)} = w_{1N^{(l)}}^{(l)}a_{1}^{(l-1)}+w_{2N^{(l)}}^{(l)}a_{2}^{(l-1)}+...+w_{N^{(l-1)}N^{(l)}}^{(l)}a_{N^{(l-1)}}^{(l-1)} " />

後面再加上l層的bias : b_1~b_N(l)即為輸入! (其實是因為上面打LaTex的時候忘記加上OAO)    

這裡的w即為權重，而下標由左至右兩個數i,j分別代表l-1(前一層)層的第i個神經元連接到第l層(當層)的第j個神經元。  
N的上標(l)為第l層的神經元個數。  

上面的式子可以簡寫成矩陣型態：  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\begin{bmatrix}z_{1}^{(l)}\\...&space;\\z_{N^{(l)}}^{(l)}\\\end{bmatrix}&space;=&space;\begin{bmatrix}w_{11}^{(l)}&space;&&space;w_{21}^{(l)}&space;&&space;w_{31}^{(l)}&space;&&space;...&space;&&space;w_{N^{(l-1)}1}^{(l)}&space;\\...&space;&&space;&space;&&space;&space;&&space;&space;&&space;&space;\\w_{1N^{(l)}}^{(l)}&space;&&space;w_{2N^{(l)}}^{(l)}&space;&&space;w_{3N^{(l)}}^{(l)}&space;&&space;...&space;&&space;w_{N^{(l-1)}N^{(l)}}^{(l)}&space;\\\end{bmatrix}\begin{bmatrix}a_{1}^{(l-1)}\\...&space;\\a_{N^{(l-1)}}^{(l-1)}\\\end{bmatrix}&plus;\begin{bmatrix}b_{1}^{(l)}\\...&space;\\b_{N^{(l)}}^{(l)}\\\end{bmatrix}" title="\begin{bmatrix}z_{1}^{(l)}\\... \\z_{N^{(l)}}^{(l)}\\\end{bmatrix} = \begin{bmatrix}w_{11}^{(l)} & w_{21}^{(l)} & w_{31}^{(l)} & ... & w_{N^{(l-1)}1}^{(l)} \\... & & & & \\w_{1N^{(l)}}^{(l)} & w_{2N^{(l)}}^{(l)} & w_{3N^{(l)}}^{(l)} & ... & w_{N^{(l-1)}N^{(l)}}^{(l)} \\\end{bmatrix}\begin{bmatrix}a_{1}^{(l-1)}\\... \\a_{N^{(l-1)}}^{(l-1)}\\\end{bmatrix}+\begin{bmatrix}b_{1}^{(l)}\\... \\b_{N^{(l)}}^{(l)}\\\end{bmatrix}" />

更簡潔地寫，可以呈現如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;z^{(l)}&space;=&space;w^{(l)}a^{(l-1)}&plus;b^{(l)}&space;\\Noted&space;\&space;&space;that&space;\&space;&space;&space;a^{(l)}&space;=&space;\sigma(z^{(l)})&space;=&space;\sigma(w^{(l)}a^{(l-1)}&plus;b^{(l)})&space;" title="z^{(l)} = w^{(l)}a^{(l-1)}+b^{(l)} \\Noted \ that \ a^{(l)} = \sigma(z^{(l)}) = \sigma(w^{(l)}a^{(l-1)}+b^{(l)}) " />

整個類神經網路可以用函數的形式來表示:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;f(x;\theta&space;)&space;=&space;\sigma(w^{(l)}&space;...&space;\sigma(w^{(2)}\sigma(w^{(1)}x&plus;b^{(1)})&plus;b^{(2)})&plus;...&space;)&plus;b^{(l)})" title="f(x;\theta ) = \sigma(w^{(l)} ... \sigma(w^{(2)}\sigma(w^{(1)}x+b^{(1)})+b^{(2)})+... )+b^{(l)})" />

考慮Output Layer輸出層上的每一個神經元，其loss為:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;C_{i}(\theta&space;)&space;=&space;\frac{1}{m}\sum_{r=1}^{m}\left\|&space;f(x^{(r)};\theta&space;)&space;-&space;y^{(r)}&space;\right\|&space;&space;\&space;&space;where&space;\&space;&space;m&space;\&space;is&space;\&space;data&space;\&space;cnts&space;" title="C_{i}(\theta ) = \frac{1}{m}\sum_{r=1}^{m}\left\| f(x^{(r)};\theta ) - y^{(r)} \right\| \ where \ m \ is \ data \ cnts " />

輸出層的整體loss其實就是把每一個神經元的loss加總起來並平均:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;C(\theta)&space;=&space;&space;\frac{1}{N^{(O)}}\sum_{i=1}^{N^{(O)}}C_{i}(\theta&space;)" title="C(\theta) = \frac{1}{N^{(O)}}\sum_{i=1}^{N^{(O)}}C_{i}(\theta )" />

輸出層的Error可以表示如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\delta_{j}^{(O)}&space;=&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;z_{j}^{(O)}}&space;=&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;a_j^{(O)}}\frac{\partial&space;a_j^{(O)}}{\partial&space;z_{j}^{(O)}}&space;=&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;a_j^{(O)}}\frac{\partial&space;\sigma(z_{j}^{(O)})}{\partial&space;z_{j}^{(O)}}&space;=&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;a_j^{(O)}}\sigma&space;'(z_{j}^{(O)})" title="\delta_{j}^{(O)} = \frac{\partial C(\theta )}{\partial z_{j}^{(O)}} = \frac{\partial C(\theta )}{\partial a_j^{(O)}}\frac{\partial a_j^{(O)}}{\partial z_{j}^{(O)}} = \frac{\partial C(\theta )}{\partial a_j^{(O)}}\frac{\partial \sigma(z_{j}^{(O)})}{\partial z_{j}^{(O)}} = \frac{\partial C(\theta )}{\partial a_j^{(O)}}\sigma '(z_{j}^{(O)})" />

寫成矩陣型態如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\delta^{(O)}&space;=&space;\begin{bmatrix}\delta_{1}^{(O)}&space;\\...&space;\\\delta_{N^{(O)}}^{(O)}\end{bmatrix}&space;=&space;\begin{bmatrix}\frac{\partial&space;C(\theta&space;)}{\partial&space;a_1^{(O)}}&space;\\...&space;\\\frac{\partial&space;C(\theta&space;)}{\partial&space;a_{N^{(O)}}^{(O)}}\end{bmatrix}&space;\bigodot&space;\begin{bmatrix}\sigma'(z_{1}^{(O)})\\...\\\sigma'(z_{N^{(O)}}^{(O)})\end{bmatrix}" title="\delta^{(O)} = \begin{bmatrix}\delta_{1}^{(O)} \\... \\\delta_{N^{(O)}}^{(O)}\end{bmatrix} = \begin{bmatrix}\frac{\partial C(\theta )}{\partial a_1^{(O)}} \\... \\\frac{\partial C(\theta )}{\partial a_{N^{(O)}}^{(O)}}\end{bmatrix} \bigodot \begin{bmatrix}\sigma'(z_{1}^{(O)})\\...\\\sigma'(z_{N^{(O)}}^{(O)})\end{bmatrix}" />

上面的運算符號為對應元素相乘，非一般數學的矩陣相乘!  

根據誤差反向傳播原理，當層誤差其實就是往後一層的誤差之線性組合!  
![Image](https://github.com/EnasVen/Theory-Math/blob/main/BackPropagation/ErrorBP.png)  

若l層後面並非輸出層，則l層的誤差可以表示為:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\\\delta_{j}^{(l)}&space;=&space;&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;z_{j}^{(l)}&space;}&space;\\&space;=&space;\sum_{k=1}^{N^{(l&plus;1)}}\frac{\partial&space;C(\theta&space;)}{\partial&space;z_{k}^{(l&plus;1)}&space;}\frac{\partial&space;z_{k}^{(l&plus;1)}}{\partial&space;a_{j}^{(l)}&space;}\frac{\partial&space;a_{j}^{(l)}}{\partial&space;z_{j}^{(l)}&space;}&space;\\=&space;\sum_{k=1}^{N^{(l&plus;1)}}&space;\delta_{k}^{(l&plus;1)}&space;\frac{\partial&space;\sum_{t=1}^{N^{(l)}}w_{tk}^{(l&plus;1)}a_{t}^{(l)}&plus;b_k^{(l&plus;1)}&space;}{\partial&space;a_{j}^{(l)}&space;}\frac{\partial&space;a_{j}^{(l)}}{\partial&space;z_{j}^{(l)}&space;}&space;\\&space;=&space;\sum_{k=1}^{N^{(l&plus;1)}}\delta_{k}^{(l&plus;1)}w_jk^{(l&plus;1)}\sigma'(z_{j}^{(l)})" title="\\\delta_{j}^{(l)} = \frac{\partial C(\theta )}{\partial z_{j}^{(l)} } \\ = \sum_{k=1}^{N^{(l+1)}}\frac{\partial C(\theta )}{\partial z_{k}^{(l+1)} }\frac{\partial z_{k}^{(l+1)}}{\partial a_{j}^{(l)} }\frac{\partial a_{j}^{(l)}}{\partial z_{j}^{(l)} } \\= \sum_{k=1}^{N^{(l+1)}} \delta_{k}^{(l+1)} \frac{\partial \sum_{t=1}^{N^{(l)}}w_{tk}^{(l+1)}a_{t}^{(l)}+b_k^{(l+1)} }{\partial a_{j}^{(l)} }\frac{\partial a_{j}^{(l)}}{\partial z_{j}^{(l)} } \\ = \sum_{k=1}^{N^{(l+1)}}\delta_{k}^{(l+1)}w_jk^{(l+1)}\sigma'(z_{j}^{(l)})" />

這個結果很明顯看出誤差反向傳播的事實!  
因此將第l層的誤差以矩陣表示如下:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\delta^{(l)}&space;=&space;&space;\begin{bmatrix}\delta_1^{(l)}&space;\\...&space;\\\delta_{N^{(l)}}^{(l)}\end{bmatrix}&space;=&space;\begin{bmatrix}\sum_{k=1}^{N^{(l&plus;1)}}\delta_{k}^{(l&plus;1)}w_{1k}^{(l&plus;1)}\sigma'(z_{1}^{(l)})&space;\\...&space;\\\sum_{k=1}^{N^{(l&plus;1)}}\delta_{k}^{(l&plus;1)}w_{N^{(l)}k}^{(l&plus;1)}\sigma'(z_{N^{(l)}}^{(l)})\end{bmatrix}&space;=&space;\begin{bmatrix}\sum_{k=1}^{N^{(l&plus;1)}}\delta_{k}^{(l&plus;1)}w_{1k}^{(l&plus;1)}&space;\\...&space;\\\sum_{k=1}^{N^{(l&plus;1)}}\delta_{k}^{(l&plus;1)}w_{N^{(l)}k}^{(l&plus;1)}\end{bmatrix}&space;\bigodot&space;&space;\begin{bmatrix}\sigma'(z_{1}^{(l)})&space;\\...&space;\\\sigma'(z_{N^{(l)}}^{(l)})\end{bmatrix}" title="\delta^{(l)} = \begin{bmatrix}\delta_1^{(l)} \\... \\\delta_{N^{(l)}}^{(l)}\end{bmatrix} = \begin{bmatrix}\sum_{k=1}^{N^{(l+1)}}\delta_{k}^{(l+1)}w_{1k}^{(l+1)}\sigma'(z_{1}^{(l)}) \\... \\\sum_{k=1}^{N^{(l+1)}}\delta_{k}^{(l+1)}w_{N^{(l)}k}^{(l+1)}\sigma'(z_{N^{(l)}}^{(l)})\end{bmatrix} = \begin{bmatrix}\sum_{k=1}^{N^{(l+1)}}\delta_{k}^{(l+1)}w_{1k}^{(l+1)} \\... \\\sum_{k=1}^{N^{(l+1)}}\delta_{k}^{(l+1)}w_{N^{(l)}k}^{(l+1)}\end{bmatrix} \bigodot \begin{bmatrix}\sigma'(z_{1}^{(l)}) \\... \\\sigma'(z_{N^{(l)}}^{(l)})\end{bmatrix}" />

接著計算一下Loss Function對權重的偏微分，根據連鎖律，我們得到:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;w_{kj}^{(l)}}&space;=&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;z_{j}^{(l)}}\frac{\partial&space;z_{j}^{(l)}}{\partial&space;w_{kj}^{(l)}}&space;=&space;\delta_j^{(l)}a_k^{(l-1)}" title="\frac{\partial C(\theta )}{\partial w_{kj}^{(l)}} = \frac{\partial C(\theta )}{\partial z_{j}^{(l)}}\frac{\partial z_{j}^{(l)}}{\partial w_{kj}^{(l)}} = \delta_j^{(l)}a_k^{(l-1)}" />

很明顯，要更新l層的權重，勢必要計算後面一層的誤差，而這樣拆解下去的結果，就是抵達輸出層。  
因此我們一開始才會先從輸出層開始討論!  

所以整個BP流程就會是:  
**1.訓練樣本輸入**  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;(x_1&space;,&space;y_1)&space;...&space;(x_m&space;,&space;y_m)" title="(x_1 , y_1) ... (x_m , y_m)" />

**2.Feed Forward**  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\\z^{(l)}&space;=&space;w^{(l)}a^{(l-1)}&space;&plus;&space;b^{(l)}&space;\\&space;a^{(l)}&space;=&space;\sigma(z^{(l)})&space;" title="\\z^{(l)} = w^{(l)}a^{(l-1)} + b^{(l)} \\ a^{(l)} = \sigma(z^{(l)}) " />  

**3.計算輸出層誤差**  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\delta^{(O)}&space;=&space;\bigtriangledown_{a^{(O)}}C(\theta&space;)&space;\bigodot&space;\sigma'(z^{(O)})" title="\delta^{(O)} = \bigtriangledown_{a^{(O)}}C(\theta ) \bigodot \sigma'(z^{(O)})" />  

**4.計算反向傳播誤差**  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;\delta^{(l)}&space;=&space;(w^{(l&plus;1)})^{T}&space;\delta^{(l&plus;1)}&space;\bigodot&space;\sigma'(z^{(l)})" title="\delta^{(l)} = (w^{(l+1)})^{T} \delta^{(l+1)} \bigodot \sigma'(z^{(l)})" />  
須注意這邊的l是從O-1層開始，一直到第2層!!  

**5.更新每一層的權重**  
<img src="https://latex.codecogs.com/png.image?\dpi{110}&space;w_kj^{(l)}&space;\Rightarrow&space;w_kj^{(l)}&space;-&space;\eta&space;&space;\frac{\partial&space;C(\theta&space;)}{\partial&space;w_{kj}^{(l)}}&space;=&space;w_kj^{(l)}&space;-&space;\eta&space;\&space;&space;&space;\delta_j^{(l)}a_k^{(l-1)}" title="w_kj^{(l)} \Rightarrow w_kj^{(l)} - \eta \frac{\partial C(\theta )}{\partial w_{kj}^{(l)}} = w_kj^{(l)} - \eta \ \delta_j^{(l)}a_k^{(l-1)}" />

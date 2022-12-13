# Information 理解
Cross-Entropy 在機器學習/深度學習都是常用的metric。要理解就必須回到entropy最初的定義。

我們都知道資訊量可以透過log進行量化:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}I(x)&space;=&space;-log_2p(x)" title="https://latex.codecogs.com/gif.image?\dpi{110}I(x) = -log_2p(x)" />

而這個資訊量(Self-Information)的單位叫做bits，我們知道 Shannon-Entropy代表隨機變數X的不確定性:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}H(x)&space;=&space;E_p[I(x)]&space;=&space;E_p[-log_2p(x)]" title="https://latex.codecogs.com/gif.image?\dpi{110}H(x) = E_p[I(x)] = E_p[-log_2p(x)]" />  
上面這個東西代表了Shannon-Entropy其實就是 Self-Information的期望值。  

假設今天資料集S內有3種類別，每一個類別的佔比分別為1/2, 1/4與1/4。  
根據Entropy定義我們可以得到這個系統(資料集S)的混亂程度:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}H(x)&space;=&space;-0.5*log_2(0.5)-0.25log_2(0.25)-0.25log_2(0.25)=&space;1.5" title="https://latex.codecogs.com/gif.image?\dpi{110}H(x) = -0.5*log_2(0.5)-0.25log_2(0.25)-0.25log_2(0.25)= 1.5" />  

在資訊界，Entropy代表資訊傳輸所需要的資源量(bits)。在實務上，我們則會使用自然對數作log的底數，也就是把log換成ln!  

套在這個例子的話就是:  
第一個類別的I(X)=1，所以傳輸第一個類別所需要的資源是 1 bits。  
第二和第三個類別的I(X)=2，所以傳輸這兩個類別個別所需 2 bits。  

因為類別個數越多代表越常見，也就是資訊量越低，所以傳輸所需的bits就越少。  
而類別個數越少則代表越不常見，資訊量較高，所以傳輸所需的bits就越多。  

因此這裡的1.5其實就是全部類別的加權平均(期望值)。  

我們得出一個結論:  
Entropy裡面的 -log 其實就是做編碼的動作。將系統或事件用0和1進行傳輸。  
根據Shannon的理論，-log(p(x)) 是最有效率的編碼方式，他可以得到最小的bits期望值，也就是最省資源。  
以數學上的語言來說，Shannon Entropy就是 bits期望值的下界。  

# 尋找讓資訊量最大的distribution
w.l.o.g，假設X是連續型隨機變數:  
<img src="https://latex.codecogs.com/gif.image?\dpi{110}H(X)&space;=&space;\int&space;-p(x)lnp(x)dx"  />  




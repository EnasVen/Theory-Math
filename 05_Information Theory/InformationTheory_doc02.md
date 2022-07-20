# Entropy vs Gini Impurity  
數學上可以證明: Entropy其實就是Gini Impurity的近似值!  
假設資料集S內有k個分類，個別比例為pk:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}H(S)=\sum_{i=1}^{k}-p_i*ln(p_i)&space;\\Gini(S)=&space;\sum_{i=1}^{k}&space;p_i*(1-p_i)"  />  
考慮 **f(x)=-lnx** 在 **x=1** 的泰勒展開:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f(x)=f(1)&plus;f'(1)(x-1)&plus;O(\bullet&space;)\cong&space;0&plus;(-1)(x-1)=1-x"  />  

將上面結果代回Entropy公式:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}H(S)=\sum_{i=1}^{k}-p_i*ln(p_i)=\sum_{i=1}^{k}p_i*ln(-p_i)\approx&space;\sum_{i=1}^{k}p_i*(1-p_i)&space;=&space;Gini(S)" />  

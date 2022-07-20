# Logistic 基礎模型
經過上一份Markdown的前置知識，我們知道了Odds Ratio指標。  
現在，我們想仿造線性迴歸模型，讓某事件發生與不發生的Odds表示成參數與觀察值的線性組合:  
<img src="https://latex.codecogs.com/svg.image?\frac{Pr(Y=1)}{Pr(Y=0)}&space;=&space;\beta_0&space;&plus;&space;\beta_1x_1&space;&plus;&space;...&space;&plus;&space;\beta_px_p&space;&space;" title="\frac{Pr(Y=1)}{Pr(Y=0)} = \beta_0 + \beta_1x_1 + ... + \beta_px_p " />  

但是這樣子寫，RHS的範圍在正負無限大；LHS則為0到無限大。  
因此我們選擇使用單調遞增函數的ln，也就是log transform，這樣一來LHS的範圍就會是正負無限大。  

而這也就成為Logistic Regression最原始的型態:    
<img src="https://latex.codecogs.com/svg.image?ln(\frac{Pr(Y=1)}{Pr(Y=0)})&space;=&space;\beta_0&space;&plus;&space;\beta_1x_1&space;&plus;&space;...&space;&plus;&space;\beta_px_p&space;&space;" title="ln(\frac{Pr(Y=1)}{Pr(Y=0)}) = \beta_0 + \beta_1x_1 + ... + \beta_px_p " />  

令 p = Pr(Y=1)，接著我們求解 p :  
<img src="https://latex.codecogs.com/svg.image?\frac{p}{1-p}&space;=&space;e^{\beta^T&space;\textbf{x}}&space;\\&space;\Rightarrow&space;p&space;=&space;(1-p)&space;e^{\beta^T&space;\textbf{x}}&space;\\\Rightarrow&space;(1&plus;e^{\beta^T&space;\textbf{x}})&space;p&space;=&space;e^{\beta^T&space;\textbf{x}}&space;\\\Rightarrow&space;p&space;=&space;\frac{e^{\beta^T&space;\textbf{x}}}{1&plus;e^{\beta^T&space;\textbf{x}}}&space;&space;\\\Rightarrow&space;p&space;=&space;\frac{1}{1&plus;e^{-\beta^T&space;\textbf{x}}}&space;" title="\frac{p}{1-p} = e^{\beta^T \textbf{x}} \\ \Rightarrow p = (1-p) e^{\beta^T \textbf{x}} \\\Rightarrow (1+e^{\beta^T \textbf{x}}) p = e^{\beta^T \textbf{x}} \\\Rightarrow p = \frac{e^{\beta^T \textbf{x}}}{1+e^{\beta^T \textbf{x}}} \\\Rightarrow p = \frac{1}{1+e^{-\beta^T \textbf{x}}} " />  

這個p也就是坊間教科書最常看見的logistic model。  

接著我們來看看係數所代表的意義。  
假設模型只使用1個feature X，在X平移1單位後，將模型相除:  
<img src="https://latex.codecogs.com/svg.image?\\ln(\frac{p_{x&plus;1}}{1-p_{x&plus;1}})&space;=&space;\beta_0&space;&plus;&space;\beta_1(x&plus;1)&space;\\ln(\frac{p_x}{1-p_x})&space;=&space;\beta_0&space;&plus;&space;\beta_1x&space;\\\Rightarrow&space;&space;ln(\frac{p_{x&plus;1}}{1-p_{x&plus;1}})&space;-&space;ln(\frac{p_x}{1-p_x})&space;=&space;\beta_1&space;\\&space;\Rightarrow&space;&space;ln(&space;\frac{\frac{p_{x&plus;1}}{1-p_{x&plus;1}})}{\frac{p_x}{1-p_x}}&space;)&space;=&space;\beta_1&space;\\&space;\Rightarrow&space;&space;\frac{&space;\frac{p_{x&plus;1}}{1-p_{x&plus;1}}}{\frac{p_x}{1-p_x}}&space;=&space;e^{\beta_1}&space;" title="\\ln(\frac{p_{x+1}}{1-p_{x+1}}) = \beta_0 + \beta_1(x+1) \\ln(\frac{p_x}{1-p_x}) = \beta_0 + \beta_1x \\\Rightarrow ln(\frac{p_{x+1}}{1-p_{x+1}}) - ln(\frac{p_x}{1-p_x}) = \beta_1 \\ \Rightarrow ln( \frac{\frac{p_{x+1}}{1-p_{x+1}})}{\frac{p_x}{1-p_x}} ) = \beta_1 \\ \Rightarrow \frac{ \frac{p_{x+1}}{1-p_{x+1}}}{\frac{p_x}{1-p_x}} = e^{\beta_1} " />  

上面的結果告訴我們: 羅吉斯迴歸的係數，其實就是該Feature增加一單位時，某事件發生的Odds Ratio!  

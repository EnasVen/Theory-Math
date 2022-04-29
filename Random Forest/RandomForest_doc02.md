# Exponential in math #
這篇主要解釋為何自然指數e的值約為2.718。  
在證明這件事之前，我們需要先證明推導e是怎麼出來的:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}y=f(x)=ln(x)\Rightarrow&space;y'=f'(x)=\frac{1}{x}&space;\&space;\&space;\&space;\forall&space;x&space;\neq&space;0&space;"/>  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f'(x)=1&space;" />  
根據導數的定義，我們可以得到:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f'(1)&space;\\&space;=\displaystyle&space;\lim_{h&space;\to&space;0}\frac{f(1&plus;h)-f(1)}{h}&space;\\&space;=\displaystyle&space;\lim_{x&space;\to&space;0}\frac{f(1&plus;x)-f(1)}{x}\\&space;=\displaystyle&space;\lim_{x&space;\to&space;0}\frac{ln(1&plus;x)-ln1}{x}&space;\\&space;=&space;\lim_{x&space;\to&space;0}\frac{1}{x}*ln(1&plus;x)&space;\\=&space;\lim_{x&space;\to&space;0}ln(1&plus;x)^\frac{1}{x}&space;\\&space;=&space;\lim_{x&space;\to&space;\infty}ln(1&plus;\frac{1}{x})^x" />  


# Exponential in math #
這篇主要解釋為何自然指數e的值約為2.718。  
在證明這件事之前，我們需要先證明e的形式是怎麼推導出來的:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}y=f(x)=ln(x)\Rightarrow&space;y'=f'(x)=\frac{1}{x}&space;\&space;\&space;\&space;\forall&space;x&space;\neq&space;0&space;"/>  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f'(x)=1&space;" />  
根據導數的定義，我們可以得到:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}f'(1)&space;\\&space;=\displaystyle&space;\lim_{h&space;\to&space;0}\frac{f(1&plus;h)-f(1)}{h}&space;\\&space;=\displaystyle&space;\lim_{x&space;\to&space;0}\frac{f(1&plus;x)-f(1)}{x}\\&space;=\displaystyle&space;\lim_{x&space;\to&space;0}\frac{ln(1&plus;x)-ln1}{x}&space;\\&space;=&space;\lim_{x&space;\to&space;0}\frac{1}{x}*ln(1&plus;x)&space;\\=&space;\lim_{x&space;\to&space;0}ln(1&plus;x)^\frac{1}{x}&space;\\&space;=&space;\lim_{x&space;\to&space;\infty}ln(1&plus;\frac{1}{x})^x" />  

<img src="https://latex.codecogs.com/png.image?\dpi{110}\because&space;f'(x)=1&space;\&space;\therefore&space;&space;\lim_{x&space;\to&space;0}ln(1&plus;x)^\frac{1}{x}&space;=&space;1&space;"  />  

<img src="https://latex.codecogs.com/png.image?\dpi{110}e&space;=&space;e^1&space;=&space;e^{\&space;\displaystyle&space;\lim_{x&space;\to&space;0}ln(1&plus;x)^{\frac{1}{x}}}&space;=&space;\displaystyle&space;\lim_{x&space;\to&space;0}&space;e^{ln(1&plus;x)^{\frac{1}{x}}}&space;=&space;\lim_{x&space;\to&space;0}(1&plus;x)^{\frac{1}{x}}" />  

至此，我們找到了e的形式，接著使用二項式定理將次方項展開:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}e&space;=&space;\lim_{x&space;\to&space;\infty&space;}(1&plus;\frac{1}{x})^x&space;\\=\lim_{x&space;\to&space;\infty&space;}&space;\left&space;(\sum_{k=0}^{x}&space;\binom{x}{k}&space;\frac{1}{x^k}&space;&space;\right&space;)\\=&space;\lim_{x&space;\to&space;\infty&space;}[\&space;\binom{x}{0}\frac{1}{x^0}&plus;\binom{x}{1}\frac{1}{x^1}...]&space;\\&space;=&space;\lim_{x&space;\to&space;\infty&space;}[\&space;\frac{1}{0!}&plus;\frac{x}{1!}*\frac{1}{x}&plus;\frac{x(x-1)}{2!}*\frac{1}{x^2}&plus;...]&space;\\&space;=&space;\lim_{x&space;\to&space;\infty&space;}[\&space;\frac{1}{0!}&plus;\frac{1}{1!}&plus;\frac{(1-\frac{1}{x})}{2!}&plus;...]&space;\\&space;=&space;&space;\frac{1}{0!}&plus;\frac{1}{1!}&plus;\frac{1}{2!}&plus;...\\&space;=&space;\sum_{n=0}^{\infty&space;}&space;\frac{1}{n!}"/>  

而將這個無窮級數的前7項加起來大約為2.718，也就是自然指數e的概略值!  

那麼，我們如何推廣到一般形式呢?  

<img src="https://latex.codecogs.com/png.image?\dpi{110}lnx=log_{e}x&space;\Rightarrow&space;a^x=e^{xlna}&space;\\\frac{da^x}{dx}=\frac{d}{d(xlna)}e^{xlna}*\frac{d}{dx}xlna&space;=&space;lna*e^{xlna}&space;=&space;a^xlna"/>  

同樣利用導數的定義:  
<img src="https://latex.codecogs.com/png.image?\dpi{110}\frac{d}{dx}a^x=\displaystyle&space;\lim_{h&space;\to&space;0}\frac{a^{x&plus;h}-a^x}{h}=\displaystyle&space;\lim_{h&space;\to&space;0}\frac{a^x(a^h-1)}{h}=a^x*\displaystyle&space;\lim_{h&space;\to&space;0}\frac{(a^h-1)}{h}&space;=&space;a^x*lna"  />  

<img src="https://latex.codecogs.com/png.image?\dpi{110}\displaystyle&space;\lim_{h&space;\to&space;0}a^h-1=\displaystyle&space;\lim_{h&space;\to&space;0}hlna&space;\\\Rightarrow&space;&space;\displaystyle&space;\lim_{h&space;\to&space;0}a^h=\displaystyle&space;\lim_{h&space;\to&space;0}1&plus;hlna&space;\\\Rightarrow&space;&space;\displaystyle&space;\lim_{h&space;\to&space;0}a=\displaystyle&space;\lim_{h&space;\to&space;0}(1&plus;hlna)^{\frac{1}{h}}&space;\\\because&space;a=e^{lna}&space;\&space;\therefore&space;e^{lna}=\lim_{h&space;\to&space;\infty&space;}(1&plus;\frac{lna}{h})^h=[\lim_{h&space;\to&space;\infty&space;}(1&plus;\frac{1}{h})^h]^{lna}&space;=&space;\lim_{h&space;\to&space;\infty&space;}(1&plus;\frac{1}{h})^{hlna}&space;\\i.e.&space;\&space;e^x&space;=&space;\lim_{h&space;\to&space;\infty&space;}&space;(1&plus;\frac{x}{h})^h&space;=&space;\sum_{n=0}^{\infty&space;}\frac{x^n}{n!}"/>  
接著再用二項式展開，就能推出結果!  

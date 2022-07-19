# What is BackPropagation ?
所有深度學習網絡的權重更新都基於反向傳播法，而說穿了就是微積分的連鎖率(Chain Rule)!  
推導過程如下:

定義符號:
1. Input Layer : x_1 , x_2 , ... , x_n  
2. Hidden Layer l : n_11 , n_12 , ... , n_lN(l)  
3. Output Layer O : O_1 , O_2 , ... O_N(m)  
4. Z_l = 第l層隱藏層的input  
5. a_l = 第l層隱藏層的output  



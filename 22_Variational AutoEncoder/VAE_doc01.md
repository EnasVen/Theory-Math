# 模型精神
傳統的AutoEncoder會將input資料壓縮成embedding vector後再利用上採樣(Up-Sampling)還原。  
但是這樣一來一往的過程由於經過非線性的運算，decode出來的圖像未必能完整呈現原始資訊。  
於是VAE透過加入noise來讓decoder在noise附近也能很好地還原最初的圖像。  

和傳統AE不同的是，VAE在Encoder階段會產出高斯分布所需要的mean和variance。  
接著利用GMM的手法從不同權重的高斯分布產出像素點(資料生成)，最後給Decoder生成圖像並與原圖比較(算loss)。  

# 架構


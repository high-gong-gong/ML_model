# ML_model整理

## 監督式學習(#001) #
# 非監督式學習(#002) #
# 集成學習(#003) #



<h2 id="001">監督式學習<h2>
  
  
  * 多元迴歸分析（線性）
  ```js

  一．常見的迴歸係數估計方法：

    1.普通最小平方法（OLS）：未知殘差的分配，使所有觀察值與估計值的殘差平方和最小。
    2.最大概似法（MLE）：已知殘差的分配，使觀察樣本出現的機率最大（意即找出一組與觀察值最接近的參考值）。

    ＃最常見的是普通最小平方法（Ordinary Least Squares, OLS）＃

  二．當為多元迴歸分析時（X1,X2,.....,Xn），需挑選適合的自變數X，分為三種方法：

    1.前向式（foreward）：將X自變數一一加入模型，從最顯著的開始加（只加顯著的X）。
    2.後向式（backward）：將自變數全部丟入模型，從最不顯著的自變數開始剔除（只踢不顯著的X）。
    3.逐步挑選（stepwise）：綜合前向及後向，直至模型顯著後不剔除。（A變數顯著，加入B變數後，A變成不顯著而B顯著，則剔除A變數，後加入C變數，以此類推）。

    ＃較常使用-逐步挑選（stepwise）＃

  三．四大假設：

    1.線性（Linearity）：x與y是線性關係。
    2.常態性（Normality）：若母體為常態分佈，則殘差項也要符合常態分佈。
    3.同質性（Heteroscedasticity）：殘差項之間有相同的變異。
    4.獨立性（Independency）：殘差項之間相互獨立。

  ＊優點：
      1.直觀，線性容易理解。
      2.限制多，樣本需求較少。
  ＊缺點：
      1.無法處理非線性問題。
      2.會有共線性問題，但無法解決線性組合高度相關的問題。
  ```

  * 正規化回歸（Regularized Regression）
  ＃確認線性迴歸有over-fitting問題，再試試看＂正規化迴歸＂＃
  
  ```js

  一．LASSO Regression：

     1.迴歸+L1 penalty（一階懲罰項,絕對值）。
     2.LASSO不僅能正規化優化模型，還能自動執行變數篩選（Feature selection）。
     3.LASSO幫你識別並挑選出有最強訊號的一個變數。

  二．嶺迴歸（Ridge Regression）：

     1.迴歸誤差平方和+L2 penalty（二階懲罰項,平方項）。
     2.將迴歸係數值平均地分散在各個變數之間。

  三．彈性網罩模型（elastic nets）：

     1.迴歸模型中，讓L1懲罰項與L2懲罰項都加入模型（權重相加=1）。
     2.LASSO為L2權重=0的型態，Ridge為L1權重=0的型態。

    ＊參考資料：
      https://ithelp.ithome.com.tw/articles/10227654
      https://www.zhihu.com/question/38121173
      https://www.itread01.com/content/1542591853.html
    
    ＊L1、L2教學影片：https://www.youtube.com/watch?v=TmzzQoO8mr4

   ```
  
  
  * 羅吉斯迴歸(logistic regression)

  ```js

    ’’’
    建立二元類別機率值之勝率比，後對數值的線性分類模型，
    羅吉斯迴歸的依變項（Y）主要為二元的類別變項（亦即是或否，0或1），
    羅吉斯迴歸的自變項（X），可以是離散變數，也可以是連續變數。
    ’’’

    1.為線性分類模型。
    2.不需要常態分配的假設。
    3.使用的估計方法為最大概似估計法。
    4.羅吉斯迴歸使用的是sigmoid激活函數。



    ＊參考資料:
    https://medium.com/%E5%B1%95%E9%96%8B%E6%95%B8%E6%93%9A%E4%BA%BA%E7%94%9F/python%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92-111-%E7%BE%85%E5%90%89%E6%96%AF%E5%9B%9E%E6%AD%B8%E5%88%86%E9%A1%9E%E5%99%A8%E4%BB%8B%E7%B4%B9%E5%8F%8A%E6%87%89%E7%94%A8-caa1cebcf831

   ```
  
  
  * 樸素貝葉斯模型（Naïve Bayesian classifier）

  ```js
  
  ～為非線性分類模型
  
  ＊基本假設為：
    1.每個變數之間相互獨立關係。
    2.每個變數同等重要（權重相等）。
    
  ＊優點：
    1.速度快，簡單，有效。
    2.可用於多類別預測，並可獲得Y的各類別機率。
    3.只需少量樣本進行訓練。
    4.可以處理帶雜訊或遺缺值的資料（相對的，遺缺值會造成'零頻率'，導致某些特徵無法一起運算，須以平滑技術處理）。
  
  ＊缺點：
    1.特徵同等重要且互相獨立的假設通常不符合現實狀況。
    2.不適合有大量數值屬性的資料集。
    3.刪除重複出現的高度相關的特徵，可能會丟失頻率信息，影響效果。

  ＊參考網址：https://kknews.cc/code/ax2xkox.html
  
  ```

  
  * KNN（K nearest neighborhood）
  
  ```js
  
  －KNN為監督式學習，假設欲預測點是i，找出離i最近的k筆資料多數是哪一類，預測i的類型。
  －K為奇數較好，為偶數可能碰上無法分類的情況。
  
  －當K=1的時候容易Over-fitting，而K很大的時候容易Under-fitting。
  
  ＊優點：
    1.對異常值不敏感。
    2.資料輸入無特別的限制。
    3.精度高。
    
  ＊缺點：
    1.訓練模型依賴訓練集資料且不可丟棄。
    2.時間複雜度（計算經過幾道程序）及空間複雜度（耗費的記憶體成本）較高。
    3.無法處理遺缺值。
    
    ＊參考資料：https://medium.com/@NorthBei/machine-learning-knn%E5%88%86%E9%A1%9E%E6%BC%94%E7%AE%97%E6%B3%95-b3e9b5aea8df
   ```
   
  * 支援向量機 SVM （Support Vector Machines）
   
   ```js
   
     ’’’
     為一種監督式學習，利用統計風險最小化的原則來估計一個分類的超平面（hyperplane），找到決策邊界，
     使到兩分類的邊界最大化（落在邊界上或邊界內的點稱為支援向量support vector），以完美區隔兩類別。
     但真實資料不可能完美分類，故SVM藉由誤差限度不敏感損失函數（ε-insensitive loss）能容忍部分誤差（即少許樣本落在邊界內）。
     運用到核函數，用意在於低維空間無法取得超平面的解，將維度轉換到更高維空間，使其找到解。
     ’’’

     ＊優點：
      1.解決高維特徵分類問題很有效。
      2.儘管特徵維度大於樣本數依然可使用。
      3.核函數可將低維轉換高維，可靈活解決各種非線性各種非線性分類迴歸問題。

     ＊缺點：
      1.若特徵維度遠高於樣本數，效果則普通。
      2.對缺失值敏感。
      3.樣本量過大時，映射到高維度，運算量會過高。
      4.核函數選擇無適合的標準，較難選擇。

     ＊參考資料：https://shaohua-mi.gitbooks.io/myself/content/svm/svmde-you-dian-que-dian.html

   ```
   
  * 分類與迴歸樹 （CART樹）
 
   ```js
   
    1.可用於分類及迴歸，根據是否滿足條件進行不斷的二分。
    2.屬於無母數分析方法，不需假設資料的線性關係或者常態分配。
    3.為隨機森林演算法的基礎。
    4.以某個目標函數，將樣本遞迴分割（recursive partition）成許多同質群組，達到群組內異質度最小
      ，分類就用組內多數決（基尼指數最小），迴歸就用均方誤差（MSE）最小。
   
   ＊優點：
    1.無須對母體進行預先假設。
    2.容易解釋，視覺化。
    3.離散或連續皆可建模，且無需處理缺失值。
    4.可以透過交叉驗證的剪枝來選擇模型。
    
   ＊缺點：
    1.容易overfitting或undrfitting。
    2.模型較不穩定，樣本小變動，模型可能劇烈變動。
    3.準確度只侷限於局部。
    
  　＊參考資料：https://juejin.cn/post/6844903513500172295
          https://www.jamleecute.com/decision-tree-cart-%E6%B1%BA%E7%AD%96%E6%A8%B9/

   ```
   
  * 類神經網路ANN （Artificial Neural Networks）
   
   ```js
   
　一．專有名詞：
    
      ＊輸入層（Input Layer）：
        －輸入資料X的地方，視為第0層節點。
        
      ＊輸出層（Output Layer）：
        －輸出預測，也是最後一層。
        
      ＊隱藏層（hidden Layer）：
        －位於輸出層及輸入層之間，都稱為隱藏層。
        
      ＊神經元（或稱感知器，Neuron）：
        －為ANN的最基本的單元，每個神經元內都包含權重係數、線性函數、激活函數（activation function）。
        　權重與線性函數接收輸入層的數據後，做線性加權，利用激活函數轉為非線性函數，後輸入給下一層神經元做迭代。
     　
      ＊激活函數（activation function）：
        －將線性函數轉換成非線性函數。
        －激活函數參考：https://zh.wikipedia.org/wiki/%E6%BF%80%E6%B4%BB%E5%87%BD%E6%95%B0
        
      ＊正向傳播（forward propagation）：
      　－由輸入層輸入資料至隱藏層再到輸出層，為正向傳播。
       
      ＊損失函數（loss function）：
        －損失函數會根據預測的目標有不同的公式，目的都是為了合理的評估正向傳播的輸出ŷ與實際值y之間的差距，最小化損失函數。
        
      ＊反向傳播（back propagation）：
        －將正向傳播計算出的輸出當成輸入，利用梯度下降（gradient descent）來更新權重，最小化損失函數，回傳至隱藏層，再做正向傳播，反覆迭代直到終止條件為止。
        
   二．架構及運行方式：
   
      1.設定ANN的架構與初始參數:隱藏層數、各層神經元數、激活函數、初始化各層神經元的權重與偏差係數。
      2.從輸入層輸入樣本，進行正向傳播，至隱藏層轉換為非線性函數後輸出給下一層節點。
      3.預測的ŷ與實際值y做比較，計算出損失函數、權重及學習率等等，再進行反向傳播。
      4.反覆進行迭代，直到達到終止條件為止。
      
      ＊終止條件：
        －迭代次數上限
        －兩次解的差異太小
        
   ＊優點：
      1.模型穩定度佳。
      2.準確度高。
      3.有記憶功能。
      4.學習能力強。
      5.平行化處理能力強。
      
   ＊缺點：
   　 1.引數多，調參數難。
      2.學習過程難以觀察，模型較難解釋。
      3.需要大量樣本訓練，且學習時間較長，甚至有可能達不到目的。
      
   ＊參考資料：https://www.itread01.com/content/1546620500.html
              https://www.itread01.com/content/1545271264.html
              https://medium.com/@evan_hsiao/%E5%BE%9Ecoursera%E5%AD%B8%E7%BF%92%E6%B7%B1%E5%BA%A6%E5%AD%B8%E7%BF%92-bd6bad6f5e14
              
   ```
   
   
<h2 id = 002 >非監督式學習<h2>   
  
  * 主成分分析PCA（Principal components analysis,PCA）：
  
  ```js
  　－為一種統計分析、簡化數據集的方法，利用正交變換來對一系列可能相關的變數的觀測值進行線性變換
    　，從而投影為一系列線性不相關變數的值，這些不相關變數稱為主成分（Principal Components）。
     
    －將座標軸中心移至數據集的中心，利用旋轉座標軸，使數據在C1軸的變異數最大，以保留更多信息，C1即為第一主成分。
    
    －找一個與C1主成分的共變異數為0的C2主成分，以避免信息重疊。
    
    －主成分分析經常用於減少數據集的維數，同時保留數據集當中對變異數貢獻最大的特徵。
    
    ＊優點：
      1.以變異數為衡量信息量的指標，不受數據集以外的因素影響。
      2.用正交轉換方式，可消除數據成分間相互影響的因素。
      
    ＊缺點：
      1.主成分間的特徵維度較難解釋。
      2.容易捨棄一些也帶有信息量的特徵，分析結果可能會受影響。
      
    ＊參考資料：https://zhuanlan.zhihu.com/p/32412043
               https://zh.wikipedia.org/wiki/%E4%B8%BB%E6%88%90%E5%88%86%E5%88%86%E6%9E%90
               https://leemeng.tw/essence-of-principal-component-analysis.html
               
  ```
   
  * 關聯分析
  
  ```js
  
    －為一種簡單、實用的分析技術，尋找數據之間的關聯性或相關性，以預測某屬性數據出現的規律。
    －最常見的為購物籃分析，當A商品被購買時，可能會一同購買哪些商品，以尋找商品之間的關聯性。
    
    ＊衡量準則：
    
      1.支持度（support）：計算品項集合在整個交易資料庫出現的次數比，介於[0, 1]，說明規則的統計顯著性。
      
      2.信心度（confidence）：利用支持度取出集合後，排列所有可能後挑出高信心度即為關聯規則。比如支持度挑出{A, B}兩品項
        ，其可能規則包含{A} ⇒ {B}或{B} ⇒ {A}。{A}⇒{B}的信心度=P(B|A)=買A的人有多少個AB都買，說明規則的強度。
        
      3.增益率：說明項集{A}和項集{B}之間的獨立性，公式為＂AB共同出現次數／A和B單獨出現次數＂，若Lift＝1說明{A}和{B}相互獨立
      　　　　　，說明兩個條件沒有任何關聯。如果Lift＜1,說明兩個事件是互斥的。一般認為Lift＞3才是有價值的規則。
           
    ＊參考資料：https://www.itread01.com/content/1546135586.html
    
  ```
  
  * 集群分析(K-means)
  
  ```js

    －K-means為非監督學習，先給定K個群心（分K群），利用各個樣本到每個群心，取最短歐式距離（直線距離），判給歐式距離最短的群心
    　，群心再依照分類後的樣本，再更新一次群心，直到所有群心的變動收斂為止。也被稱為懶惰學習。

    ＊優點：
    
      1.原理簡單且訓練速度快。
      2.算法可解釋度高。
      3.主要僅需調整參數K。

    ＊缺點：
    
      1.對於噪音及異常樣本較敏感。
      2.成效很依賴輸入的數據集，有些型態數據集很難收斂；或者某類別樣本較少，聚類效果較差。
      3.效果較局部，並非全部類別準確。

    ＊參考資料:https://blog.csdn.net/u014465639/article/details/71342072

   ```



<h2 id = 003 >集成學習（ensemble learning）<h2>
  
  ```js
  －通過建立幾個模型組合來解決單一預測問題。
  －原理是在數據集上構建多個分類器/模型，各自獨立學習和做出預測
  　，這些預測最後結合成單預測，因此優於任何一個單分類器做出的預測。
  ```
  
  * 引導聚集算法（Boostrap AGGregatING, BAGGING）：
  
  ```js

     ＊概念：
     
      －強模型的Error小但Var大。
      －使用多個強模型結合，使Var縮小，並Error也不會有太大變化。
      －各個模型無關聯性。
      －每個模型權重一致。
    
    ＊方法：
    
       1.從訓練樣本中抽出（取後放回）多個同大小的data set，每個data set分別建立不同的模型。
       2.每個模型為保持多樣性，不做任何改善（如決策樹不做剪枝的動作），並且權重一致。
       3.結合每個模型後，若為類別就用多數決方式來決定結果，若為迴歸則用計算平均數來決定結果。
       
    ＊隨機森林（Random Forest）：
      －為Bagging的方法。
      －可平行運算。
      －對離群值較不敏感。
      
    ＊優點：原始資料具有許多噪音及雜訊，可以透過抽樣方式避免噪音一同訓練，進而改善模型的不穩定性。
    
    ＊參考資料：Hung-yi Lee的youtube頻道 https://www.youtube.com/watch?v=tH9FH1DH5n0
  ```
   
   * Boosting
   
   ```js
     ＊概念：
     
       －弱模型的Error大但Var小。
       －使用多個強模型結合，使Var縮小，並Error也不會有太大變化。
       －每個模型有關聯性。
       －透過第一個模型對各個data set做分類／預測，用得來的錯誤來加強權重做學習
       　，產第二個模型，新模型會學習到之前錯誤，以此類推，進而改善結果。
       －與Bagging方法類似。
       －不同之處在於需先進行一個模型才能找尋另一個模型
       　，會對結果錯誤的模型加重權重，加以學習。
        
        
      一．AdaBoost：
        －是一種Boosting分類算法。
        －一般用於類別二分。
        
        ＊方法：
          1.透過一組data set訓練出一個模型，data初始權重都為1。
          2.對於分類／預測對的data減少權重，錯誤的data則加強權重，創造新的data set。
          3.進行Ｎ次後，將Ｎ個模型結合（準確度高的模型權重較大，反之），進行＂加權＂投票決定最後結果。
          
      二．GDBT（Gradient descent + Boosting）：
      
        －核心是CART迴歸樹。
        －引進殘差的概念。
        
        ＊與隨機森林差異在於：
           1.不可平行運算。
           2.對於離群值較敏感。
           3.只能用CART迴歸樹。
           4.具有殘差的概念。
        
        ＊與Adaboost不同在於：
           1.用梯度下降針對模型做改善取得新的模型。
           2.沒有對訓練集的data做權重的變更。
           3.使變異數和滿足誤差要求，則求得最佳模型。
           
        ＊參考資料:Hung-yi Lee的youtube頻道 https://www.youtube.com/watch?v=tH9FH1DH5n0
                  GDBT  https://zhuanlan.zhihu.com/p/120361768
                  
   ```
   
   * 堆疊法（stacking）：
   
   ```js
     ＊概念：
        －將不同的學習模型結合，給予每個模型權重，創造新的模型。
        －與bagging和boosting不同在於，可以做模型的異質整合。
      
     ＊參考資料：https://www.itread01.com/content/1547223330.html
   ```
    

# Apriori Algorithm
網路上有許多講解的網站，我就不再這邊重複贅述，但我覺得有一個非常有趣的例子就是，美國有間超市在尿布的旁邊放置了啤酒，看似完全沒關西的兩樣東西，經過 Apriori Algorithm 計算之後發現其實兩個的關聯性是非常高的，其原因為爸爸來幫孩子買尿布，一想到家中的壓力，不免想來一手啤酒，Apriori algorithm可以用在許多商品上的統計。

## :heart_eyes: Introduction my self
大家好，我是吳定軒，目前就讀於國立台北科技大學電機工程系碩士班，我將在我的github上分享我所實作的Project，內容也有許多需要改進的地方，如果你有甚麼建議歡迎寫信到我的信箱t109318095@ntut.org.tw。   

Hello everyone, I am TINGHSUAN-WU. I am currently studying in the Master's Program of the Department of Electrical Engineering, National Taipei University of Technology. I will share the projects I have done on my Github. There are many areas for improvement in the content. If you have any suggestions, welcome Write to my mailbox.

## :book: Method
我先將輸入進行 one-hot 的編碼(True 為 1，False 為 0)，如圖所示。

![image](https://user-images.githubusercontent.com/45062401/150716635-dc9d9b5e-07c8-4101-aa59-dc2c3c2d72f7.png)

我先設定我們的 min support count(教授給的是 min support0.03，我這裡設定 count 為 30，因為總量是 1000)，然後設定confidence 為 0.7，就可以開始我們的程式了。

第一步我會先統計各類的總數，只要這裡的總數低於我們所設定的 count，就會被列入刪除的子集。

![image](https://user-images.githubusercontent.com/45062401/150716694-0808e04f-e3a3-4aab-b211-275642a90561.png)

接下來我會把沒有被刪除的類別進行排列組合，從兩個一組到十五個一組的排列組合，我們就可得到一個各種排列組合的陣列

![image](https://user-images.githubusercontent.com/45062401/150716727-b2df093e-8eea-45b8-bf7d-1e4e4f186e22.png)

這個陣列我先將他們都轉成 one-hot 的形式，比如說 apple,bread就會編碼成[1,1,0,0……,0]，然後再藉由這個 one-hot 編碼的形式到輸入的 one-hot 去進行 count 的計算，如果兩個相等的話，那個
類別的排列組合 count 會加一，之後就可以找到這些排列組合類別的 count，如圖十一所示，而這些排列組合我會把它放進一個字典裡面，方便我後面進行 confidence 的計算。

![image](https://user-images.githubusercontent.com/45062401/150716756-5567531c-6644-44da-89db-02b72265c41a.png)

接下來就是將這些排列組合計算 confidence，在這邊比較困難的點是，一個集合有數個不同的子集合，用圖十一的最後一列來舉例，Ice cream, Milk, Onion, Unicorn, chocolate 的子集合就有 Ice cream, Milk、Ice cream, Onion、Ice cream ,Unicorn…，等於是你集合裡有六個項目，它們裡面又可以在排列組合一次，然後來算對不同的子集合的 confidence，而在這裡我結合字典的方法，在跑每一項集合時，再跑裡面子集合的排列組合，此時我會記錄這個集合的 count，並且在排列組合子集合時，進去剛剛我所存的字典找這個子集合的 count，再把兩個 count 相除，這樣就有辦法算出每個子集合對集合的 confidence，並且當這個子集合對集合的confidence 小於 min confidence 時，我就不去紀錄，當confidence 大於 min confidence 時，我才去紀錄，而這些結果就是強關聯性的 confidence。

![image](https://user-images.githubusercontent.com/45062401/150716808-8e408472-30df-4281-ac2b-4cd4b55b7566.png)

最後輸出 apriori_result.csv

![image](https://user-images.githubusercontent.com/45062401/150716839-63905fb9-0909-4087-b6fa-b027131441b3.png)


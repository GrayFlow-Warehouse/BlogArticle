1. 假設你先在使用者電腦localstorage 存著 localstorage.Auth = ‘ABC’  (這個ABC裡面可以加一些expired_time，or 你想要的uniq值)

2. 那他登入前會帶著 Auth，不管裡面是什麼值，只要Rails認得 ABC 他就覺得這是我認識的人，我要給他許可權限。

3. 那RAILS 就會用，IP、瀏覽器資訊、時間、Rails的sercret key，做加密變成一個「好像是憑證的東西」，再把這個字串丟回給頁面用JS 用locastroage存起來。

4. 然後以後每次有帶這個「好像是憑證的東西」，Rails就會先用 IP、瀏覽器資訊、時間、Rails的sercret key再加密，看這個結果會不會跟「好像是憑證的東西」一樣，一樣就通過。

5. 這樣加密邏輯是做在後端，前端也只知道你會丟Auth，不會知道你是用IP和瀏覽器資訊做加密的。
換去別的電腦也會因為瀏覽器資訊、IP不一樣所以在步驟4 RailS再驗證的時候就不合格

6. 假設你要讓所有「好像是憑證的東西」失效，把Rails的sercret key改掉就可以了

最一開始要發可以「有權限拿「好像是憑證的東西」」的那個字串
覺得可以做成Emails的方式寄給那個人開，那是這個字串裡面要有expried_time，不然會換別人拿去開。
打開會跳掉那個網站裡面，然後最開始作剛剛上面那些事。
這樣的重點是 Locastroage，規定只會拿到「網域」底下的資料喔。
Locastroage不是共通的
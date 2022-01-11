## 概念
   ### 緣起
   - 家中有個櫃子常備有乾糧，家人酷愛半夜吃零嘴解饞，最近引發胃食道逆流。
     為減緩他胃食道逆流問題、其他人又不用一起戒零食的前提下，
     為了不影響其他人的生活作息、並讓他養成好習慣，有跟家人約好：深夜不可吃零食，抓到要貢獻罰款給其他人，拍到一次罰一次。
   ### 構想
   - 一個好習慣的養成至少需要21天，為了在習慣養成期間嚴格執行，設計構想是：若在深夜時段打開零食櫃，被拍到照片並傳送到Line群組，馬上就可以跟半夜
  

## 材料
   |NO|項目|數量|
   |:---:|:---:|:---:|
   |1|Rasberry Pi 4|1|
   |2|ＳＤ card 32G|1|
   |2|行動電源|1|
   |3|紅外線運動感測器|１
   |4|鏡頭|1|
   |５|杜邦線（母對母)|３|
   |6|餅乾盒、紙盒｜n|
   
   P.Ｓ..餅乾盒可以任選，只要裝得下工具都可以！我只是趁機想吃義美泡芙≖‿≖   
   
## 實驗步驟
   ### Step1. download Raspberry Pi Imager & 格式化SD card （若已完成本步驟可略）
- Raspberry Pi Imager下載網址請見官網：https://www.raspberrypi.com/software/
![image](https://user-images.githubusercontent.com/96639949/148876834-23a6f604-3e93-4421-9e6c-3f706f9ee3cc.png)
- Raspberry Pi Imager下載完成之後，格式化SD card。並將格式化後的SD card安置到樹莓派背面插槽（如下圖藍框位置）
![image](https://user-images.githubusercontent.com/96639949/148879201-f365c318-05ed-494a-9ad2-93ae063a9c25.png)
   
   ### Step2. 筆電安裝VNC viewer (＊若不需要遠端操作，本步驟可略)
 -可使用Real VNC，若無帳號可一併註冊。下載官網：https://www.realvnc.com/en/connect/download/viewer/
 -安裝好後，會有登入介面可登入（（缺一張圖） 帳號預設是pi
 
   ### Step3. 在Raspberry Pi 開啟Camera、VNC & VNC設定 & wifi測定
   ＊若Raspberry Pi 想直接接鍵盤或螢幕，可不開啟VNC
   ![image](https://user-images.githubusercontent.com/96639949/148880692-ca61181e-d828-468f-a8f1-784f0814c9aa.png)
 -VNC設定
 
   
- ### Step4. 電路圖(Circuit Diagram)
   藍色接線與字代表所需接至Raspberry pi上GPIO對應腳位(例如下圖，N1接至GPIO 16) /<br>
   
- 程式1: 先判斷時間，若深夜時段感測零食櫃被打開，就用相機鏡頭拍下照片
- ### Step5. 程式1:part 2: 將照片透過line notify傳送到群組
   
- ### Step５. 餅乾盒安裝
   可參考：



## 。可以改進或其他發想
-電源：目前是採用以行動電源取代，可以改為鋰電池和充電板
-偵測比對：目前是無差別可以偵測比對到特定人士，在傳送line
-鏡頭高度可以改善

車子位於地板上導致鏡頭過低,可以用支架提高它的拍攝角度
電池為並聯因此區達馬達的電壓較低,會使車子跑不快,若乘載更多重物,會跑更慢甚至跑不動
Raspberry Pi 樹莓派UPS 鋰電池擴充板USB 電源供應模組行動電源耗電量快
可以加上避障模組,使之快碰壁時可以轉向之類
可以從拍照偵測目標物轉變為錄影方式直接偵測
可以若是非本人接近,使用蜂鳴器發出聲音

## 。參考資料
1.https://www.youtube.com/watch?v=Tw0mG4YtsZk
2.https://www.youtube.com/watch?v=VzYGDq0D1mw
3.https://eason851021.medium.com/line-notify-%E5%88%A9%E7%94%A8python%E5%82%B3%E9%80%81%E5%AE%A2%E8%A3%BD%E5%8C%96%E8%A8%8A%E6%81%AF-%E4%BB%A5%E5%90%89%E5%A8%83%E5%A8%83%E9%95%B7%E8%BC%A9%E5%9C%96%E7%82%BA%E4%BE%8B-2a50c6a5197b
4.https://www.youtube.com/watch?v=RPZZZ6FSZuk
5.http://hophd.com/raspberry-pi-sensor-infrared/
6.https://ithelp.ithome.com.tw/articles/10250334
7.https://eason851021.medium.com/line-notify-%E5%88%A9%E7%94%A8python%E5%82%B3%E9%80%81%E5%AE%A2%E8%A3%BD%E5%8C%96%E8%A8%8A%E6%81%AF-%E4%BB%A5%E5%90%89%E5%A8%83%E5%A8%83%E9%95%B7%E8%BC%A9%E5%9C%96%E7%82%BA%E4%BE%8B-2a50c6a5197b

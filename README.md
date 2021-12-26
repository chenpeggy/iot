### draft
## 概念
   ### 。緣起
   - 解決半夜偷吃零食，胃食道逆流問題
   - 解決肥胖問題

   ### 。構想
   四駒車上的鏡頭會間隔幾秒照相，並且回傳照片給Rasberry Pi 3，透過影像辨識，查看相片是否為本人，若照片並非本人，四駒車會逃跑離開。

## 前置作業
- ### 材料
   |NO|項目|數量|購買地址|
   |:---:|:---:|:---:|:---|
   |1|Rasberry Pi 4|1|tbd|
   |2|四顆並聯電池盒(包含正負極單芯線)|1|tbd|
   |3|1.5v電池|4|tbd|
   |4|鏡頭|1|tbd|


-  ### 電路圖(Circuit Diagram)
   藍色接線與字代表所需接至Raspberry pi上GPIO對應腳位(例如下圖，N1接至GPIO 16) /<br>
## 。實驗步驟
- ### Step1. raspberry pi sd卡重置 （若已完成本步驟可省略）
   可參考：
   
- ### Step2. raspberry pi 安裝python（若已完成本步驟可省略）
   可參考：
   
-### Step3. raspberry pi 安裝python（若已完成本步驟可省略）
   可參考：
   
- ### Step1. raspberry pi sd卡重置 （若已完成本步驟可省略）
   可參考：
   
- ### Step2. raspberry pi 安裝python（若已完成本步驟可省略）
   可參考：
   
-### Step3. raspberry pi 安裝python（若已完成本步驟可省略）
   可參考：








7. 程式設計
Requirements.txt # modules versions

00.PerOperation

data___________________# DataGenerator檔生出來的照片
class0 (一堆皮丘照片,但只有正面照)
class1 (一堆小熊跟維尼照片,但只有正面照)
00.DataGenerator.py_____# ImageDataGenerator生成照片
01.GetData.py___________# cv2將照片轉numpy array,以及resize ,再吐出data與label的pickle檔(X.pickle/y.pickle)
02.CNN_model.py___________# 用X.pickle/y.pickle train CNN model ,再吐出json以及h5檔
03.ReadModel_predict.py_____# load model以及test predict
01.FourWheelCar_ImageRecognize

CarClass.py_______# 執行車子指令(B,BR,R,F,BL,L,F,S)
ImagePredict.py_____# load model&predict the image
main.py_____# import CarClass和ImagePredict ,如果ImagePredict回傳class1, CarClass對車子進行指令
model.h5
model.json


## 。可以改進或其他發想
dataset可以使用各種不同角度的物體照片,這樣predict才能更精確
車子位於地板上導致鏡頭過低,可以用支架提高它的拍攝角度
電池為並聯因此區達馬達的電壓較低,會使車子跑不快,若乘載更多重物,會跑更慢甚至跑不動
Raspberry Pi 樹莓派UPS 鋰電池擴充板USB 電源供應模組行動電源耗電量快
可以加上避障模組,使之快碰壁時可以轉向之類
可以從拍照偵測目標物轉變為錄影方式直接偵測
可以若是非本人接近,使用蜂鳴器發出聲音

## 。參考資料

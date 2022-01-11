## 概念
   ### 。緣起
   - 家中有個櫃子常備有乾糧，家人酷愛半夜吃零嘴解饞，最近引發胃食道逆流。
     為減緩胃食道逆流問題、並養成好習慣，有跟家人約好：深夜不可吃零食，抓到要貢獻罰款給其他人。~(～￣▽￣)～     
   ### 。構想
   - 一個好習慣的養成至少需要21天，為了在習慣養成期間嚴格執行，設計構想是：若在深夜時段打開零食櫃，被拍到照片並傳送到Line群組，馬上就可以被大家知道。
  

## 材料
   |NO|項目|數量|
   |:---:|:---:|:---:|
   |1|Rasberry Pi 4|1|
   |2|ＳＤ card 32G|1|
   |2|行動電源|1|
   |3|紅外線運動感測器|１
   |4|鏡頭|1|
   |５|杜邦線（母對母)|３|
   |6|紙盒|視需求自行調整|
   
## 實驗
   ### Step1. download Raspberry Pi Imager & 格式化SD card （若已完成本步驟可略）
   - Raspberry Pi Imager下載網址請見官網：https://www.raspberrypi.com/software/
    <br><img src="https://user-images.githubusercontent.com/96639949/148876834-23a6f604-3e93-4421-9e6c-3f706f9ee3cc.png" width="600" height="500">
   - Raspberry Pi Imager下載完成之後，格式化SD card。並將格式化後的SD card安置到樹莓派背面插槽（如下圖藍框位置）
    <br><img src="https://user-images.githubusercontent.com/96639949/148916569-e3ba030d-0682-4674-9554-de5372c856af.png" width="600" height="400">

   ### Step2.筆電安裝VNC viewer (＊若不需要遠端操作、或已完成，本步驟可略)
   - 可使用Real VNC，若無帳號可一併註冊。下載官網：https://www.realvnc.com/en/connect/download/viewer/
   - 安裝好後，會有登入介面可登入。帳號預設是pi
 
   ### Step3.在Raspberry Pi 中開啟Camera、VNC & VNC登入
   - 開啟Camera、VNC
   <br>*若Raspberry Pi 想直接接鍵盤或螢幕，可不開啟VNC
   <br><img src="https://user-images.githubusercontent.com/96639949/148916678-73c23929-7b9d-481e-b908-e93a5701525b.png" width="600" height="400">
   - 登入VNC
  <br><img src="https://user-images.githubusercontent.com/96639949/148922956-6090460d-5160-43c5-acce-cd47f53491ae.png" width="600" height="400">

   ### Step4.電路圖 ＆接線
   - *接線接時要注意訊VCC、GND和OUT的位置，OUT接在board 7的位置
   <br> *圖片來源：https://projects.raspberrypi.org/en/projects/physical-computing/11
   <br><img src="https://user-images.githubusercontent.com/96639949/148918788-8eac875e-48ad-4f0e-a2c4-b6f6e30354aa.png" width="600" height="300">
   - 鏡頭安裝可參考：https://www.youtube.com/watch?v=VzYGDq0D1mw

   ### Step5.Line Ｎotify 權杖申請
   - 登入Line Ｎotify：https://notify-bot.line.me/zh_TW
    <br><img src="https://user-images.githubusercontent.com/96639949/148904897-2d60d245-7959-4275-82b6-e56a750bc5a1.png" width="600" height="500">
   - 登入後點選個人頁面
    <br><img src="https://user-images.githubusercontent.com/96639949/148916889-0b6a8c51-ec5a-48f9-8a77-60e2cdb2151e.png" width="600" height="400">
   - 點選發權杖
    <br><img src="https://user-images.githubusercontent.com/96639949/148907303-e7d67da3-0585-4f0e-976f-8f81ddbfd116.png" width="600" height="500">
   - 選擇接收通知的聊天室，並輸入會在傳送訊息時顯示的權杖名稱。＊＊請記得將Line Ｎotify邀入對話群組中
    <br><img src="https://user-images.githubusercontent.com/96639949/148908004-89e309ec-2f19-4f2d-9bbc-c7a837acd22d.png" width="600" height="350">
   - 複製Line發行的權杖，呼叫Line API時會需要用到
    <br><img src="https://user-images.githubusercontent.com/96639949/148909138-10cd3bf6-cc57-453d-bacf-53bdb1ca5a7e.png" width="600" height="400">
   
   ### Step6.程式
```python=
import os, sys ,requests, datetime
from picamera import PiCamera
import RPi.GPIO as GPIO
import time
from pathlib import Path 
 
pir =7   ＃紅外線運動感測器pin out位置
camera = PiCamera() 
camera.resolution =(512,512) ＃照片的大小
camera.rotation =270  ＃相機的角度，可以根據自己擺飯位置調整
token ='＊＊＊＊＊＊＊＊＊＊＊＊＊'  ＃line發放的權杖
message ='謝謝現行犯金主 ！｡:.ﾟヽ(*′∀`)ﾉﾟ.:｡' ＃line傳送的訊息
img = Path('/home/pi/Desktop/image/image.jpg') ＃因為會將照片傳送到line，不需要額外留下每次拍下的照片，所以固定照片檔名和位置
GPIO.setmode(GPIO.BOARD) 
GPIO.setup(pir,GPIO.IN)
 
 
def line_notify(token, message, img): ＃請見主要來源：2
    headers = {"Authorization": "Bearer " + token}
    param = {'message': message}
    image = {'imageFile' : open(str(img), 'rb')}
    r = requests.post("https://notify-api.line.me/api/notify", headers = headers, params = param, files = image )
    return r.status_code
 
try:
    while True :
        input_state = GPIO.input(pir)
        datetime_now = datetime.datetime.time(datetime.datetime.now())
        evening = datetime_now.replace(hour=21,minute=0, second=0, microsecond=0)
        morning = datetime_now.replace(hour=5,minute=0, second=0, microsecond=0)
        if input_state == True and (datetime_now > evening or datetime_now < morning): ＃時間內有偵測到，就用拍下照片
            camera.capture('/home/pi/Desktop/image/image.jpg')
            linereturn  = line_notify(token, message, img)＃使用將拍下的照片透過line notify傳送到群組
            print('line return message:',linereturn)
            time.sleep(5)
        else:
            time.sleep(2)
            
except keyboardInterrupt: #press control c to interrup
    print("stop")
    
finally:
    GPIO.cleanup()
 ```
  
   ### Step7.擺放放置鏡頭和位置
   - 紙盒外挖兩個洞，紙盒內用其他廢棄紙盒和餅乾架著感測器和鏡頭外挖兩個洞
    <br>P.Ｓ.餅乾盒可以任選，只要裝得下工具都可以！≖‿≖   
    <br><img src="https://user-images.githubusercontent.com/96639949/148915202-51289b80-2afa-4fb9-b0ab-cb18412ea3b3.png" width="20%" height="20%"><img src="https://user-images.githubusercontent.com/96639949/148917323-5cfff7a9-c34c-4490-861c-7ed6b7ba0e7e.png" width="20%" height="20%">

   ### Step8.實驗結果



## 可以改進地方：
- 改以鋰電池和充電板取代：因為櫃子中沒有插座，目前是以行動電源代替。因耗電量問題，可以改為鋰電池和充電板取代。
- 增加比對功能：目前是無差別，只要感應到人就拍照、傳送訊息。可以增加偵測比對到特定人士，再傳送
- camera:人移動速度過快，會造成照片會模糊
- 人的動作跟照片擷取的速度不好調整，很容易拍太多，或很容易拍太少

## 參考資料
   ### 主要來源：
   - https://atceiling.blogspot.com/2014/02/raspberry-pi-pir-passive-infrared.html
   - https://eason851021.medium.com/line-notify-%E5%88%A9%E7%94%A8python%E5%82%B3%E9%80%81%E5%AE%A2%E8%A3%BD%E5%8C%96%E8%A8%8A%E6%81%AF-%E4%BB%A5%E5%90%89%E5%A8%83%E5%A8%83%E9%95%B7%E8%BC%A9%E5%9C%96%E7%82%BA%E4%BE%8B-2a50c6a5197b
   ### 其他參考：
   - https://www.youtube.com/watch?v=Tw0mG4YtsZk
   - https://www.youtube.com/watch?v=RPZZZ6FSZuk
   - http://hophd.com/raspberry-pi-sensor-infrared/
   - https://ithelp.ithome.com.tw/articles/10250334

` `1. 系統簡介

1\.1規格目的

如今的自駕技術已經可以透過輔具來協助行動不方便的人，加上AR的興起讓人類在獲取資訊上能更加快速，但在輔具上沒有相關的應用，若能將輔具系統加上AI(Artificial Intelligence)及AR(Augmented Reality) 的運用，使得我們可以快速取得資訊或是在人機介面上有更大的突破。本文件針對應用AI及AR技術於行動輔具之操作系統的功能需求，提供相關人員做為系統細部設計階段的重要參考。

1\.2 規格範圍

本文件描述了本系統所需之功能，透過建立軟體架構圖及流程圖的方式，讓團隊成員對系統全貌有一致性的認知，但不會涉及到系統內部技術層面，僅以此進行雙方的溝通。本文件預期讀者有：系統設計人員、專案管理人員、系統測試人員、未來系統使用者。 

`         `1.3 參考文件

`	   `<https://github.com/NVIDIA-AI-IOT/jetbot>

<https://blog.cavedu.com/tag/jetbot/>

<https://developer.nvidia.com/embedded/community/jetson-projects#jetbot>

<https://www.waveshare.net/wiki/JetBot_AI_Kit>

<https://www.youtube.com/watch?v=8Hz2G2SK3KI>

<https://github.com/abuelgasimsaadeldin/Jetbot-Road-Following-and-Collision-Avoidance>

2\. 系統概述

2\.1 系統目標

我們的系統設計一個結合AR與引導的系統，舉例在以下三種可能的使用情形:

在醫院時，如果有年長者或行動不方便的人來看診，時常需要在不只一個科別間移動，醫院的路線複雜，如果沒有志工或是家屬幫忙推輪椅的話，對他們非常的不便，若能有這樣的系統，有自動導航及AR的功能，除了能減少醫院志工所需要的人力，若有吃飯等需求，還可以透過AR導覽，快速取得資訊，將餐廳、甚至是優惠資訊展示在使用者眼前。


或是在機場時，由於過多的航班資訊很混亂和登機口的路線複雜，很常在找登機口時，花過多的時間，如果有個系統能顯示航班資訊，甚至是把免稅商品資訊顯示給使用者，讓旅客除了能準時抵達登機口外，還能好好的逛機場的免稅用品。

博物館顯示展覽資訊，如果對特定某個展品有興趣，透過引導遊客到該展場外，還能使用AR將展品資訊傳遞給使用者。

2\.2 系統範圍

在本節中將分別說明應用AI及AR技術於行動輔具之操作系統的相關功能與定義。

（一）系統名稱： 

應用AI及AR技術於行動輔具之操作系統

（二）系統功能說明：

一般使用者：透過本系統的使用，使用者可以在公共場所利用穩定循跡的功能到達想抵達的目的地，也可以透過手動模式，直接操作車子抵達目的地。在車子行走時也會透過AR讓使用者知道周圍的店家資訊、廣告投放等。

2\.3 系統架構

![https://lh4.googleusercontent.com/2slObrnu9Z0nm_3HDn7iDRaZBMMRnO-b0Atm0PC7uIKE80fYzhpHNRgRtQ7FbSnUVmc4Nfczg0VN5ZmDLXxWqkK8uvWmQHrqzgtn_ETSUmIXs5aNBqy4P1vNXcaE_ZgORhUb8xUP93XRGp-XIi1zdG-Cij3jvdJ2wAPhsyh19NGoxBXsvKa-kdjNcFZzf4MxOpFuXA](Aspose.Words.47e94274-4414-4dcb-afe0-2bd4c90be825.001.png)

硬體: 

(1)車輛控制系統:以Jetson Nano(4GB,Nvidia,USA)來模擬行動輔具，包含電池供應系統、無線網卡、手部輔助控制器、馬達，如圖一。

軟體:

(2)即時路況資訊顯示系統:使用Unity Vuforia (Ver.10.8.4, Qualcomm, USA)套件來實作AR的功能。使用Jupyter Notebook編譯程式，  並應用PyTorch(Ver.1.11.0, Facebook AI研究室, USA)來訓練模型。

技術:

(3)以PyTorch的深度學習方法，計算適當過彎弧度及速度，使得輪椅過彎更加順暢安全；使用TCP(Transmission Control Protocol)連線讓AR及Jetbot進行溝通，例如:路上的狀況在車子接收後，可以傳送到AR端，將警示訊息傳達給使用者。

2\.4 軟/硬體建構項目需求概述

本章節主要在說明本系統各軟體建構項目之間的功能需求、介面需求、品質需求、及安全需求，綜合上述的考量，為使用者訂作最為人性化使用的系統。

（一）功能需求 ：

本系統有(1)穩定循跡 (2)即時避障 (3)手動模式 (4)廣告投放 (5)店家資訊 (6)方向顯示六種功能可讓使用者去做使用。

(1)穩定循跡：本功能可以讓車子跟隨著路地上的路線行走，並幫助使用者可以快速到達目的地。

(2)即時避障：本功能可以讓車子的鏡頭在行走若判斷到前方有障礙物時可以立刻停下車子以免發生危險。

(3)手動模式：本功能可以讓使用者如果在發生突發狀況時使使用者可以接管車子的控制權以免發生危險。

(4)廣告投放：本功能可以讓贊助商放置廣告，若使用者的車子經過其店家ＡR會投放出其店家的廣告。

(5)店家資訊：本功能可以讓使用者在經過路旁店家時，若對該店家感興趣則可以點擊螢幕上的店家，即可獲的該店資訊。

(6)方向顯示：本功能可以讓使用者知道車子接下來的行走方向。

（二）介面需求：

本系統會提供一個簡潔的畫面方便使用者可以直接控制，也會提供簡單的標示系統讓使用者可以一目瞭然當前車子的狀況，讓使用者隨時可以處在一個安心的情狀下使用本系統。

（三） 品質需求：

本系統具備即時性及穩定性，讓使用者在使用上可以感受到較人性化的使用效果。針對使用者，給予相對的權限，改變車子的行走模式，讓使用者有更加的行車體驗。

（四） 安全需求：

`	`本系統提供即時避障及手動模式以便在發生危急情況時可以停下車子或讓使用者即時控制來化解危機的狀況以免發生危險。

2\.5 軟/硬體環境 

`	`（一）軟體環境：

本系統是使用Ubuntu(Ver.20.04, Canonical, UK)作業系統，將AR軟體運行在Android(Ver.11, Open Handset Alliance, USA)系統的裝置上。	

（二）硬體還境：

`		`Jetson nano ：

- GPU：基於 128 核心的 NVIDIA Maxwell™ 架構 GPU
- CPU：四核 ARM® A57

`		`Jetbot：

- 散熱風扇組  X1
- PQI Power 12000PD 行動電源
- IMX219 MIPI 高品質視覺攝像模組(77度視角) X1。
- Micro SD 快閃記憶卡128GB  (含作業系統與範例) X1

控制搖桿

2\.6 一般限制

本系統因為要讓移動式行動輔具可以明確地知道要前往哪一個方向，故只能讓它在有線的地面上移動，例如醫院的地面。由於使用AR的關係，所以要先對餐廳、購物、景點等地方標上tag，所以本系統只能限制在已經訓練好的地方，不能帶使用者到未知的場景。

3\.設計內容

3\.1 軟/硬體建構項目架構

硬體架構:

![https://lh3.googleusercontent.com/qtYiW2PPba177lJf0fnNrlkPDKf7qqmHC3LV4aRoefFWxf1ygPxWfi-dRujtKCzwZnWWftAIhK95GgFq6L8RLdIEgNeiyROdkilMFMXd61UEXiQk4VcFUye5g1KhfNfbRc5F2kvNOOIXyMqwvlkq510is_6eslY0WoLYO-7qarS95o67XJCzz-8tr6wk](Aspose.Words.47e94274-4414-4dcb-afe0-2bd4c90be825.002.png)




軟體架構:

![https://lh4.googleusercontent.com/CwLes5mafRCGdpRuXWkO_3LxgVxwCTh8--gMlbTuacf2SqBrUghQ1EPHQeFT2A0pVCzm3U0vfHxZaYSmqn6yPt9gN8CDH2kRt-b1_5pSMHXOCz45abokHJUP0zvHkDN8M33swheBB5yxlmkMrDTdQWxVItZoICCzMPeIBEMM_-pzvNarbRcpCn4C09g-](Aspose.Words.47e94274-4414-4dcb-afe0-2bd4c90be825.003.png)

![](Aspose.Words.47e94274-4414-4dcb-afe0-2bd4c90be825.004.png)

3\.2 軟硬體組件設計說明

硬體 ：

NVIDIA Jetson Nano Developer Kit B01

5V 4A變壓器 

Micro SD 快閃記憶卡64GB 

IMX219 MIPI 高品質攝像模組

EPIMAX AC1200 雙頻長距離USB3.0無線網卡

散熱風扇組

PQI Power 12000PD 行動電源

直流馬達驅動模組 

壓克力車體 

操作搖桿

軟體： 

即時避障： 

在行動輔具的自動模式時，攝像頭如果判斷到前方有障礙物之後會停下來，避免使用者在不注意的時候撞到障礙物，並且會傳送警示訊息在顯示面板上，直到障礙物離開攝像頭的視線範圍為止。

穩定循跡： 

開啟自動模式後 ，行動輔具將沿著原本的路線行走，同時間也會對周遭環境進行偵測，除了可以降低使用者在操作上的負擔之外，也可以協助偵測周遭的危險狀況，並且在第一時間通知使用者，讓使用者有更多的反應時間，減少受傷的風險 。

手動模式： 

手動模式的設計是要讓行動輔具的使用者有更多自由選擇的空間，在路口會先停下來等待使用者的指示再前進，或者是遇到緊急狀況時，使用者切換到手動模式來任意移動行動輔具，進而提早避開危險。

AR資訊顯示： 

透過對場景的判斷，在相對位置上用不同的方式顯示相對應的AR，有圖示、文字、上下浮動、影片形式呈現的AR物件，目的就是為了要讓行動不便的使用者在獲取資訊上簡單又快速，在短時間內取得周遭環境的資訊，不會因為輪椅高度的限制造成獲取資訊上的不易。

訊息傳輸： 

透過程式，在行動輔具運作的過程中，將其路況的參數利用TCP/IP(Transmission Control Protocol/Internet Protocol)傳輸的方式傳送給AR端，AR端用其接收行動輔具傳送過來的參數值將結果顯示在面板上。不同的值將會有對應的顯示，像是行進的方向、路況等。

路況判斷：

行動輔具運作的過程中，其行進的道路上將會有不同的路口，像是 T字路口以及十字路口等，在進入彎道前會先停下來等使用者給予指令，再來做相對應的操控，降低使用者在轉彎時的風險。

`	`3.3 介面設計說明

本介面主要是為行動不便的人在使用軟體時，不需要花費過多的心思在獲取資訊上，利用簡單又清楚的方式的將車況訊息顯示在面板上，因此本介面主要是以圖形的方式來代替文字描述提高使用者在瀏覽的可讀性，另外圖形之間的間距、顏色明暗、尺寸大小等都是有經過特別的配置使畫面更加俐落簡潔。本介面也有將顯示面板上的車況訊息進行分類，將相似的訊息顯示在面板上的同一側符合邏輯認知，減少行動不便的使用者在獲取資訊上出錯的可能性。由於介面會搭配本專題的行動輔具配合使用，所以顯示面板中大多的空間將會留給行車的路況顯示其餘的訊息將會安排在畫面的上側及下側以免遮擋到行車路線，同時又能讓使用者清楚的看到車況訊息。

3\.4 作業程序設計說明

一開始程式開始執行的時候相機會自動拍攝相片，接下來由AI判斷目前的狀況，第一種是等待障礙物移動，表示目前正前方有障礙物，需要等待障礙物移開之後才能跳出迴圈，否則在回圈內持續等待。第二種狀況是前方道路淨空，需要沿著固定路線行走，程式會根據圖片跟目前位置計算偏移量，計算完畢之後將數值賦予給馬達，如果馬達差值大於20%會輸出左右轉訊號。第三種情況是遇到路口，需要使用者給予指示告知如何移動，當使用者給予指示後才跳出迴圈，否則一直在迴圈等待，最後檢查是否收到終止訊號，否則輸入相片持續執行迴圈。

![https://lh3.googleusercontent.com/9Jcq8hzdA4jox5VfxQcSB47z-TjFB3yxVKZn2L-Dqj-cgk_k2zBLwpDstZuRJsCxuDG_Sj4_wJ29fJrouDKPJRJoOwLxLeJSTQKFMiWUeM9cQOpIoGU7xa_AIS4k7kfsmsc1UO7sMd4tMB3ENWoi53tevNdRrx6D0j8wfWPZT0gj2QZo0oKeLxlMvfzx](Aspose.Words.47e94274-4414-4dcb-afe0-2bd4c90be825.005.png)



3\.5 輸入/輸出設計說明

輸入：圖片一開始經由PIL ( Python Imaging Library,荷蘭)將圖片轉換成Numpy(Numerical Python,USA) Array，再將Numpy Array轉換成Tensor，讓AI模型看懂的一種格式。

`	`輸出：圖片轉換成Tensor後丟入AI模型進行運算，運算結果為自己設定節點數的比率。

`	`4. 需求制設計之追溯與版本管理

|NO.|修改日期|修改後版號|修改位置|修改內容概述|
| :-: | :-: | :-: | :-: | :-: |
|1|2022\.01.04|1\.1|全部|初版新訂|
|2|2022\.06.25|2\.1|實作方式|進度更新|
|3|2022\.9.27|3\.1|全部|新增內容|

`	`附錄 訊息清單

` 		 `檔案與程式對照表


|網址|功能|
| :-: | :-: |
|<https://github.com/CHEN-HSING-CHIEH/B08project/blob/main/PROJECT/final.ipynb>|<p>行動輔具的控制程式</p><p></p>|
|<https://github.com/CHEN-HSING-CHIEH/B08project/blob/main/PROJECT/TcpClient.cs>|行動輔具與AR端的網路訊息傳輸程式|
|<https://github.com/CHEN-HSING-CHIEH/B08project/blob/main/PROJECT/PlayPause.cs>|<p>AR廣告影片顯示程式</p><p></p>|
|<https://github.com/CHEN-HSING-CHIEH/B08project/blob/main/PROJECT/showdetail.cs>|AR商家資訊顯示程式|



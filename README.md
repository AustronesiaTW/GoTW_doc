Guide of Taiwan
===================


來自東南亞的外籍勞工亦稱移工（移住勞工 migrant worker），一直是台灣、香港、新加坡、日本、韓國甚至是阿拉伯世界重要的勞動力來源。根據國際勞工協會統計<sup>[1](#footnote1)</sup>，2013年亞太地區就有2千5百萬的移民工，移民工通常會在工作國待上3年或是更多，也因為語言及文化的差異而產生許多問題。
我們希望首先針對於台灣的移工推出在地的網路服務，以交通運輸為出發點，提供他們在台生活所需之資訊，來降低因語言或文化所產生的差異。

Requirement analysis
-----

根據勞基法，移工每週會有一天休假日，大多數的人都會聚集到各縣市的車站，直到傍晚才回到公司的宿舍。這一天的休假產生了相當多的消費行為，而根據我們的問卷調查，有6成的外勞表示他們對於語言的問題感到困擾，尤其搭乘大眾運輸時這個問題更加棘手。

Solution
-----

針對上述的問題，我們選擇從交通運輸出發，透過交通部提供的  API<sup>[2](#footnote2)</sup>，利用手機 App 作為媒介，將火車時刻及公車動態展示給移工們。

### Features

- 提供多國語言介面（英、越、印、泰）

- 台鐵時刻表查詢

- 公車動態查詢（台北市、新北市）

- 查詢之歷史紀錄

- 同時提供中英文站名

- 問路（Helper）系統
 
#### **User scenario**

#### **Flow chart**

### API 

#### **TRA**

取得指定日期、起迄站間之 JSON 格式站間時刻表資料並加入時間篩選
```
/v2/Rail/TRA/DailyTimetable/OD/{OriginStationID}/to/{DestinationStationID}/{TrainDate}?$filter=OriginStopTime/ArrivalTime gt '{DepartureTime}'&$format=JSON
```

取得當天指定車次的 JSON 格式時刻表資料並取出停靠時間資料
```
/v2/Rail/TRA/DailyTimetable/{TrainNo}?$select=StopTimes&$format=JSON
```

取得指定起訖站間之 JSON 格式票價資料
```
/v2/Rail/TRA/ODFare/{OriginStationID}/to/{DestinationStationID}?$format=JSON
```
#### **City Bus**
取得指定縣市的 JSON 格式市區公車路線與站牌資料並篩選與查詢條件相同之路線
```
/v2/Bus/StopOfRoute/City/{City}/{RouteName}?$filter=RouteName/Zh_tw eq '{RouteName}'&$format=JSON
```
取得指定縣市、路線名稱的 JSON 格式公車預估到站資料並篩選與查詢條件相同之路線
```
/v2/Bus/EstimatedTimeOfArrival/City/{City}/{RouteName}?$filter=RouteName/Zh_tw eq '{RouteName}'&$format=JSON
```


### User Interface

![test](http://imgur.com/50tBqsG.jpg)


Future
-----
當台灣獲得一定的用戶後，我們也可以將業務拓展至香港、新加坡等國家，此外，鑑於市場的空白，功能面的部分還可以多作嘗試。
功能|現有公司
---|----
計程車|Uber, 55688, findTaxi, Lyft, Go-Jek
團購|GOMAJI, Groupon, 美團
折價券|
線上匯款|TranserWise
拍賣|Facebook, Carousell, PiPiMy, 蝦皮

Reference
-----

<a name="footnote1">1</a>: http://ilo.org/asia/areas/labour-migration/lang--en/index.htm

<a name="footnote2">2</a>: http://ptx.transportdata.tw/MOTC
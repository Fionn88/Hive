# hive

# 20445 -- 替代役役男訓練人數統計表

- HDFS 完整路徑 `/dataset/20445/20445.csv`

```
欄位名稱
年度   year:int
梯次   phase:chararray
替代役役男訓練人數   trainees:int

原始資料集內容
year phase trainees
100,91,1079
100,92,969
100,92_2,122
```
- 建立 HIVE TABLE 

> CREATE EXTERNAL TABLE a_20445 
(
year int, 
phase string, 
trainees int
)
ROW FORMAT 
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/20445';


- 題目 1-1. 哪一年的總替代役人數最多？

    - 輸出格式:  年分, 人數

        - 答案範例:  107, 87

> SELECT year, SUM(trainees) AS trainees_sum
FROM a_20445
GROUP BY year
ORDER BY trainees_sum DESC LIMIT 1;

```
(103,37210)
```

- 題目 1-2. 哪一年的梯次最多？

    - 輸出格式:  年分, 數量

        - 答案範例:  107, 87

> SELECT COUNT(phase) AS phase_count,year
FROM a20445
GROUP BY year
ORDER BY phase_count DESC LIMIT 1;

```
(104,23)
```

---

# 5958 -- 各縣(市)警察(分)局暨所屬分駐(派出)所地址資料

- HDFS 完整路徑 `/dataset/5958/5958.csv`

```
欄位名稱
名稱       name:chararray
郵遞區號   zip_code:chararray
地址       address:chararray

原始資料集內容
       name     zip_code    address
臺北市政府警察局,100,臺北市中正區延平南路96號
中山分局,104,臺北市中山區中山北路2段1號
中山一派出所,104,臺北市中山區中山北路1段110號
```
- 建立 HIVE TABLE 

> CREATE EXTERNAL TABLE a5958
(
name string,
zip_code string,
address string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/5958/';

- 題目 2-1. 最多派出所的郵遞區號是幾號？

   - 輸出格式:  郵遞區號, 數量

        - 答案範例:  100, 87

> SELECT zip_code,COUNT(zip_code) AS zip_code_count
FROM a5958
WHERE name LIKE "%派出所%"
GROUP BY zip_code
ORDER BY zip_code_count DESC LIMIT 1;

```
(546,21)
```

- 題目 2-2. 哪個縣市有最多派出所？

> SELECT COUNT(address) AS address_count
FROM a5958
WHERE address LIKE "新北市%" AND name LIKE "%派出所%";

```
(新北市,145)
```

---

# 6086 -- 107 年幼兒園名錄

- HDFS 完整路徑 `/dataset/6086/6086.csv`

```
欄位名稱
代碼 code:chararray
學校名稱 school:chararray
縣市名稱 city:chararray
地址 address:chararray
電話 phone:chararray

原始資料集內容
 code             school             city                  address                                     phone
011K02,新北市私立溫特爾幼兒園,新北市,新北市三峽區龍埔里5鄰三樹路336號1、2、3樓,(02)26718181
011K03,新北市私立新榮富新莊幼兒園,新北市,新北市新莊區中信里13鄰中和街204巷1、3號，218巷2、6號，中信里12鄰中和街1、3、5、7、11號,(02)29922174
011K04,新北市私立崇儒幼兒園,新北市,新北市中和區安樂里16鄰宜安路56之1號1樓,(02)29435789
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a6086
(
code string,
school string,
city string,
address string,
phone string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/6086/';

- 題目 3-1. 幼兒園數量最少的是哪個縣市?

    - 輸出格式:  縣市, 數量

        - 答案範例:  臺北市, 87

> SELECT city,COUNT(city) AS city_count
FROM a6086
WHERE school LIKE "%幼兒園%"
GROUP BY city
ORDER BY city_count LIMIT 1;

```
(連江縣,5)
```

- 題目 3-2. 臺北市與新北市的幼兒園各有多少間? 由數量多到少排序。

    - 輸出格式:  縣市, 數量

        - 答案範例:  臺北市, 87

> SELECT city,COUNT(city) AS city_count
FROM a6086
WHERE school LIKE "%幼兒園%"
GROUP BY city
ORDER BY city_count;

```
(新北市,1134)
(臺北市,689)
```

---

# 6087 -- 107年國民小學名錄

-  HDFS 完整路徑 `/dataset/6087/6087.csv`

```
欄位名稱
代碼 code:chararray
學校名稱 school:chararray
縣市名稱 city:chararray
地址 address:chararray
電話 phone:chararray
網址 url:chararray

原始資料集內容
   code       school           city                  address                                  phone                       url
011601,私立育才國小,新北市,新北市永和區福和路125巷20號,(02)29214630,http://www.ytes.ntpc.edu.tw
011602,私立聖心國小,新北市,新北市八里區龍米路一段261號,(02)26182330,http://lshes.com/school/
011603,私立及人國小,新北市,新北市永和區文化路172號,(02)29212145,http://www.cjps.ntpc.edu.tw
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE aa6087
(
code string,
school string,
city string,
address string,
phone string,
url string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/6087/';

- 題目 4-1. 新北市有多少間私立國小？

    - 輸出格式:  數量

        - 答案範例:  87

> SELECT city,COUNT(school) AS school_count
FROM aa6087
WHERE school LIKE "%私立%"
GROUP BY city;

```
(新北市,5)
```

---

# 999003 -- 107年6月行政區分齡兒童及少年性別人口統計_縣市

- HDFS 完整路徑 `/dataset/999003/999003.csv`

```
欄位名稱
縣市代碼  country_id:int
縣市名稱  country:chararray
0-5歲兒童人口數  a0a5_cnt:int
6-11歲兒童人口數  a6a11_cnt:int
12-17歲少年人口數  a12a17_cnt:int

原始資料集內容
country_id country a0a5_cnt a6a11_cnt a12a17_cnt
10002,宜蘭縣,20907,21718,27474
10015,花蓮縣,        `    15380,15338,19695
09020,金門縣,6373,4437,5451
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a999003
(
country_id int,
country string,
a0a5 int,
a6a11 int,
a12a17 int
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/999003/';

- 題目 5-1. 新北市的 0~17 歲兒童總數有多少個?

    - 輸出格式:  數量

        - 答案範例:  87

> SELECT country,SUM(a0a5) AS a0a5_sum,SUM(a6a11) AS a6a11_sum,SUM(a12a17) AS a12a17_sum
FROM a999003
GROUP BY country;

```
(新北市,620357)
```

---

# 12197_A1 -- A1 類交通事故資料

- HDFS 完整路徑 `/dataset/12197_A1/12197_A1.csv`

```
欄位名稱
發生時間 time:chararray
死亡人數 dead:chararray
受傷人數 injured:chararray
車種 vehicle:chararray

原始資料集內容
                        ctime                     dead  injured    vehicle
106年01月01日 02時35分00秒,死亡1,受傷0,普通重型-機車
106年01月01日 02時43分00秒,死亡1,受傷0,普通重型-機車
106年01月01日 03時35分00秒,死亡2,受傷0,普通重型-機車
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a12197_A1
(
time string,
dead string,
injured string,
vehicle string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/12197_A1/';

- 題目 6-1. 造成事故最多的車種是哪種車? (造成死亡或受傷皆算事故)

    - 輸出格式:  車種, 次數

        - 答案範例:  普通重型-機車, 87

> SELECT vehicle,COUNT(vehicle) AS vehicle_sum
FROM a12197_A1
GROUP BY vehicle
ORDER BY vehicle_sum DESC LIMIT 1;

```
(普通重型-機車,513)
```

- 題目 6-2. 發生事故最多的是哪年哪月哪日? (造成死亡或受傷皆算事故)

    - 輸出格式:  日期, 次數

        - 答案範例:  106年01月01日, 87

> SELECT COUNT(SUBSTR(time,1,10)) AS time_sub_count,SUBSTR(time,1,10) AS time_sub
FROM a12197_A1
GROUP BY SUBSTR(time,1,10)
ORDER BY time_sub_count DESC;
```
(106年08月13日,10)
```

- 題目 6-3. 造成死亡總數最高的是哪個車種?

    - 輸出格式:  車種, 次數

        - 答案範例:  普通重型-機車, 87

> SELECT vehicle,SUM(SUBSTR(dead,3,1)) AS dead_sub_sum
FROM a12197_A1
GROUP BY vehicle
ORDER BY dead_sub_sum DESC;

```
(普通重型-機車,517)
```

==延伸題==  發生事故`人數`最多的是哪年哪月哪日? (造成死亡或受傷皆算事故)

> SELECT (SUM(SUBSTR(injured,3,1))+SUM(SUBSTR(dead,3,1))) AS all_sub_sum,SUBSTR(time,1,10) AS time_sub
FROM a12197_A1
GROUP BY SUBSTR(time,1,10)
ORDER BY all_sub_sum DESC;

---

# 12197_A2 – A2 類交通事故資料

- HDFS 完整路徑 `/dataset/12197_A2/12197_A2.csv`

```
欄位名稱
發生時間 time:chararray
死亡人數 dead:chararray
受傷人數 injured:chararray
車種 vehicle:chararray

原始資料集內容
                        ctime                     dead  injured    vehicle
106年01月01日 00時00分00秒,死亡0,受傷1,自用-小客車
106年01月01日 00時00分00秒,死亡0,受傷2,自用-小客車
106年01月01日 00時03分00秒,死亡0,受傷1,自用-小客車
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a12197_A2
(
time string,
dead string,
injured string,
vehicle string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/12197_A2/';

- 題目 7-1. 平均造成受傷數最高的是哪個車種? (造成受傷人數總數/事故總數) 平均一樣時依車種字母大到小排序。

    - 輸出格式:  車種, 次數

        - 答案範例:  普通重型-機車, 87

> SELECT (SUM(SUBSTR(injured,3,1))/COUNT(vehicle)) AS all_all,vehicle
FROM a12197_A2
GROUP BY vehicle
ORDER BY vehicle DESC;

```
(普通重型-特種車,2.0)
(大客車-軍車,2.0)
```

---

# 24333 -- 「ATM位置」查詢一覽表

- HDFS 完整路徑 ``/dataset/24333/24333.csv`

```
欄位名稱
裝設金融機構代號  code:chararray
裝設金融機構名稱  name:chararray
裝設地點  location:chararray
裝設縣市  city:chararray
裝設地址  address:chararray

原始資料集內容
code name  location city               address
004,臺灣銀行,士林分行,台北市,台北市士林區中山北路六段197號
004,臺灣銀行,大同公司,台北市,台北市中山區中山北路三段22號
004,臺灣銀行,大安分行,台北市,台北市大安區敦化南路二段69號1樓
```

- 建立 HIVE TABLE

CREATE EXTERNAL TABLE a24333
(
code string,
name string,
location string,
city string,
address string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/24333/';


- 題目 8-1. 哪間銀行的ATM在台中市有最多台?

    - 輸出格式:  銀行名稱, 數量

        - 答案範例:  元大商業銀行, 87

> SELECT COUNT(name) AS name_count,name
FROM a24333
WHERE city LIKE "%台中市%"
GROUP BY name
ORDER BY name_count DESC;

```
A: (中國信託商業銀行,642)
```


- 題目 8-2. 哪個縣市擁有最多"臺灣銀行"的ATM?  [注] "台"跟"臺"

    - 輸出格式:  縣市, 數量

        - 答案範例:  台北市, 87

> SELECT city,COUNT(code) AS code_count
FROM a24333
WHERE code LIKE "%004%"
GROUP BY city
ORDER BY code_count DESC;


```
A: (台北市,95)
```

---

# 8066 -- 農產品交易行情

- HDFS 完整路徑 ``/dataset/8066/8066.csv`


```
欄位名稱
交易日期  date:chararray
作物代號  crop_code:chararray
作物名稱  crop_name:chararray
市場代號  market_code:chararray
市場名稱  market_name:chararray
上價  upper_price:float
中價  middle_price:float
下價  lower_price:float
平均價  average_price:float
交易量  trading_volume:int

原始資料集內容
cdata crop_code crop_name market_code market_name upper_price middle_price lower_price average_price trading_volume
107.09.11,11,椰子,104,台北二,31,20,15.7,21.3,849
107.09.11,129,椰子-進口剝殼,104,台北二,88.3,72.8,60,73.3,60
107.09.11,31,釋迦,104,台北二,114,73.5,46.8,76.3,3581
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a8066
(
data string,
crop_code string,
crop_name string,
market_code string,
market_name string,
upper_price float,
middle_price float,
lower_price float,
average float,
trading_volume int
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/8066/';

- 題目 9-1. 全台農產品交易量最高的是哪個市場?

    - 輸出格式:  市場名稱, 交易量

        - 答案範例:  台北二, 87

> SELECT market_name,SUM(trading_volume) AS trading_volume_sum
FROM a8066
GROUP BY market_name
ORDER BY trading_volume_sum;

```
A: (台北一,1676906)
```


- 題目 9-2. 全台交易總量最高的是哪種農產品? </br> ("百香果-其他"與"百香果-改良種"皆算是"百香果"，以此類推其他農產品名稱)

    - 輸出格式:  農產品名, 交易量

        - 答案範例:  椰子, 87

>　SELECT split(crop_name,'-')[0] AS crop_name_split,SUM(trading_volume) AS trading_volume_sum
FROM a8066
GROUP BY split(crop_name,'-')[0]
ORDER BY trading_volume_sum DESC;

```
A: (文旦柚,589354)
```


- 題目 9-3. 平均上價與平均下價平均價差最高的是哪項農產品? </br> ("百香果-其他"與"百香果-改良種"算兩項不同的農產品，以此類推其他農產品名稱)

    - 輸出格式:  農產品名, 交易量

        - 答案範例:  椰子, 87

> SELECT crop_name,(AVG(upper_price)-AVG(lower_price)) AS all_sum
FROM a8066
GROUP BY crop_name
ORDER BY all_sum;

```
A: (葡萄-進口,334.6)
```

---

# 63029 -- 十六縣持卡人前十大國外消費金額及筆數(依簽帳筆數排名)

- HDFS 完整路徑 ``/dataset/63029/63029.csv`

```
欄位名稱
年月  year_month:chararray
國別  country:chararray
城市  tw_city:chararray
金額  amt:int
筆數  count:int

原始資料集內容
year_month country tw_city amt count
2014-01,英國,基隆市,20933333,30063
2014-01,盧森堡,基隆市,2575891,5276
2014-01,日本,基隆市,20238233,3895
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a63029
(
year_month string,
country string,
tw_city string,
amt int,
count int
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/63029/';



- 題目 10-1. 2016到2018年國外消費總金額最高的是哪個縣市?

    - 輸出格式:  縣市, 金額
    
        - 答案範例:  基隆市, 87

> SELECT tw_city,SUM(amt) AS amt_sum
FROM a63029
WHERE year_month LIKE "%2016%" OR year_month LIKE "%2017%" OR year_month LIKE "%2018%"
GROUP BY tw_city
ORDER BY amt_sum DESC;


```
A: (新竹市,10005781918)
```


- 題目 10-2. 哪一個月的國外消費平均金額最高?

    - 輸出格式:  月份, 金額

        - 答案範例:  一月, 87

> SELECT split(year_month,"-")[1],CAST(SUM(amt)/COUNT(count) AS INT) AS all_sum
FROM a63029
GROUP BY split(year_month,"-")[1]
ORDER BY all_sum;

```
A: (六月,11158768)
```
[注] 結果為06，我自己將答案改成'六月'


- 題目 10-3. 新竹市2018年在哪個國家的總消費金額最高?

    - 輸出格式:  國家, 金額
    
        - 答案範例:  英國, 87

> SELECT country,SUM(amt) AS amt_sum
FROM a63029
WHERE tw_city LIKE "%新竹市%" AND year_month LIKE "%2018%"
GROUP BY country
ORDER BY amt_sum;

```
A: (日本,548333518)
```

---

# 38315 -- 十六縣居民跨縣市消費樣態

- HDFS 完整路徑 ``/dataset/38315/38315.csv`

```
欄位名稱
年月 year:chararray
地區 area:chararray
類別 type:chararray
卡數 cards:int
總交易筆數 total_trans:int
總交易金額[新台幣] total_amt:biginteger
跨縣市交易筆數 inter_city_trans:int
跨縣市交易金額[新台幣] inter_city_amt:biginteger

原始資料集內容
 year      area  type  cards total_trans total_amt inter_city_trans inter_city_amt
2014-01,基隆市,ALL,241213,942118,2265105458,714100,1803194168
2014-02,基隆市,ALL,229540,813048,1842401862,641756,1533509566
2014-03,基隆市,ALL,239793,918036,1992896656,722421,1658553554
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a38315
(
year string,
area string,
type string,
cards int,
total_trans int,
total_amt bigint,
inter_city_trans int,
inter_city_amt bigint
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/dataset/38315/';

- 題目 11-1. 2018年哪一個縣市的跨縣市交易金額平均最高?

    - 輸出格式:  縣市, 金額

        - 答案範例:  基隆市, 87

> SELECT area,(SUM(inter_city_amt)/SUM(inter_city_trans)) AS amt_trans_avg
FROM a38315
WHERE year LIKE "%2018%"
GROUP BY area
ORDER BY amt_trans_avg DESC;

```
A: (新竹市,4164)
```

- 題目 11-2. 總交易筆數中平均單筆消費金額最高的是哪個縣市?

    - 輸出格式:  縣市, 金額

        - 答案範例:  基隆市, 87

> SELECT area,(SUM(total_amt)/SUM(total_trans)) AS amt_trans_avg
FROM a38315
GROUP BY area
ORDER BY amt_trans_avg DESC;

```
A: (新竹市,2651)
```

---

# 999001 -- 連線紀錄

- HDFS完整路徑 ``/dataset/999001/999001.tsv`


```
欄位名稱
連線編號  connection:int
連線形式  type:chararray
通訊協定  protocol:chararray
服務程式  service:chararray
時間戳記  timestamp:int
本機位址  local_host:chararray
本機通訊埠  local_port:int
遠端位址  remote_host:chararray
遠端通訊埠  remote_port:int

原始資料集內容
connection  type  protocol  service  ctimestamp  local _host  local _port  remote_ host  remote_ port
3       accept  tcp     mssqld  1502196257      192.168.131.6   1433    222.174.114.42  56803
4       accept  tcp     mssqld  1502196259      192.168.131.6   1433    222.174.114.42  56889
5       accept  tcp     smbd    1502196284      192.168.131.4   445     218.81.136.101  2671
```

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a999001
(
connection int,
type string,
protocol string,
service string,
times_tamp int,
local_host string,
local_port int,
remote_host string,
remote_port int
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE
LOCATION '/dataset/999001/';



- 題目 12-1. 哪一個本機位址提供的服務程式種類最多？

    - 輸出格式:  IP, 種類數

        - 答案範例:  192.168.131.6, 87

> SELECT local_host,COUNT(DISTINCT service) AS service_dis_count
FROM a999001
GROUP BY local_host
ORDER BY service_dis_count DESC;

```
A: (192.168.130.1,19)
```

- 題目 12-2. 哪一個服務程式的IP數最多？

    - 輸出格式:  服務程式, IP數

        - 答案範例:  mssqld, 87


> SELECT service,COUNT(DISTINCT local_host) AS local_host_count
FROM a999001
GROUP BY service
ORDER BY local_host_count DESC;

```
A:
(mysqld,10)
(mssqld,10)
(RtpUdpStream,10)
(SipSession,10)
(Blackhole,10)
(smbd,10)
(Memcache,10)
(httpd,10)
(upnpd,10)
(SipCall,10) 
```

- 題目 12-3. 哪一個遠端位址連線次數最多？

    - 輸出格式:  IP, 次數

        - 答案範例:  222.174.114.42, 87

> SELECT remote_host,COUNT(remote_host) AS remote_host_count
FROM a999001
GROUP BY remote_host
ORDER BY remote_host_count DESC LIMIT 5;


```
A: (35.185.109.141,31564)
```

---

# 999001 -- 連線紀錄

- 建立 HIVE TABLE

> CREATE EXTERNAL TABLE a999002
(
download int,
connection int,
download_url string,
download_md5_hash string
)
ROW FORMAT
DELIMITED FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE
LOCATION '/dataset/999002/';



- 題目 13-1. 哪一個網址的 IP:port 被下載檔案最多次？

    - 輸出格式:  IP:port, 次數

        - 答案範例:  118.89.159.61:12347, 87


> SELECT split(download_url,"/")[2],COUNT(split(download_url,"/")[2]) AS dow_spl_count
FROM a999002
GROUP BY split(download_url,"/")[2]
ORDER BY dow_spl_count;


```
A: (203.189.234.149:8080,282)
```

---

# JOIN 以下題目資料集 999001 跟 999002 均會使用到

- 題目 14-1. 哪一個遠端位址下載檔案次數最多？ </br> (資料集:  999001 & 999002)

    - 輸出格式:  IP, 次數

        - 答案範例:  222.174.114.42, 87


> SELECT a1.remote_host,COUNT(a1.remote_host) AS remote_host_count
FROM 
(
a999001 a1 JOIN a999002 a2 ON (a1.connection = a2.connection)
)
GROUP BY a1.remote_host
ORDER BY remote_host_count;

```
A: (222.186.21.168,50)
```

- 題目 14-2. 哪一個本機位置被下載檔案次數第三多？ </br> (資料集:  999001、 999002)

    - 輸出格式:  IP, 次數
        
        - 答案範例:  222.174.114.42, 87

> SELECT a1.local_host,COUNT(a1.local_host) AS local_host_count
FROM 
(
a999001 a1 JOIN a999002 a2 ON (a1.connection = a2.connection)
)
GROUP BY a1.local_host
ORDER BY local_host_count;

```
A: (192.168.130.3, 87)
```

---

# JOIN 以下題目資料集 5989 跟 24333 均會使用到

- 題目15-1. 哪個縣市的警察局與ATM數量差距最大？ </br> [注] "台"跟"臺" </br> (資料集: 5958 & 24333)

    - 輸出格式:  縣市, 數量

        - 答案範例:  台北市, 87

> SELECT atm_count.city,CAST(atm_count.location_count / police_count.location_count AS INT) AS aaa
FROM
(
(SELECT TRANSLATE(city,"台","臺") AS city,COUNT(location) AS location_count FROM a24333 GROUP BY city ) AS atm_count
JOIN 
(SELECT SUBSTR(address,0,3) AS city,COUNT(*) AS location_count FROM a5958 GROUP BY SUBSTR(address,0,3)) AS police_count
ON (atm_count.city = police_count.city)
);

```
A: (台北市,37)
```


- 題目 15-2.依內政部行事曆，2018年有最多節日的月份，其節日有哪些? (節日以名稱大到小排序) </br> 十六縣居民該月總消費金額平均是12個月中最高的嗎? (平均為每月平均) </br> 資料集:  26557 & 38315
    
    - 輸出格式:  月份, 節日(不一定一個), 是/否, 金額

        - 答案範例:  一月, 是, 87

>

```
A: (02,3,和平紀念日,農曆除夕,春節,02,1932543150.25)
```

- [注] </br> 原始答案為 (02,3,{(02,和平紀念日),(02,農曆除夕),(02,春節)},02,1932543150.25) 手動刪除不必要的符號與內容














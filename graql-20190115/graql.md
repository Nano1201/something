

```Graql
define

animal sub entity isabstract,
	has ___,
	plays ___;

person sub animal,
  has full-name,
  has nickname,
  has gender,
  key email,
  plays employee,
  relates employer;
  plays marrigeship-requester,
  plays marrigeship-respondent;
  
wonmen sub person,
  has ___,
  plays wife;

men sub person,
  has __,
  plays husband;
	
marriageship sub relationsip,
  relates husband,
  relate wife,
  play request-marriageship;
  
marrige-request sub relationsip,
   has request-date,
   relates request-marriageship,
   relates marrigeship-requester,
   relates marrigeship-respondent;
  
employment sub relationship,
  key reference-id,    ##unique attribute 'key'
  relates employer,
  relates employee;
```

```
define

reaction sub relationship,
  relates reacted-emotion,
  relates reacted-to,
  relates reacted-by;

emotion sub attribute datatype string,
  plays reacted-emotion;

post sub entity,
  plays reacted-to;

person sub entity,
  plays reacted-by;
```

```
define

location-of-everything sub relationship is-abstract,
  relates located-subject,
  relates subject-location;

location-of-birth sub location-of-everything,
  relates located-birth as located-subject,
  relates birth-location as subject-location;

location-of-residence sub location-of-everything,
  relates located-residence as located-subject,
  relates residence as subject-location;
```



define attribute:

```
define

start-date sub attribute datatype data;

residency sub relationship,
  ## roles and other attributes
  has start-date;

travel sub relationship,
  ## roles and other attributes
  has start-date;
```



Regex : 

```
emotion sub attribute datatype string regex /[like, love, funny, shocking, sad, angry]/;
```



attribute has attribute:

```
define

content sub attribute datatype string,
  has language;

language sub attribute datatype string;
```



attribute play a role

```
define

language sub attribute datatype string,
  plays spoken;

person sub entity,
  plays speaker;

speaking-of-language sub relationship,
  relates speaker,
  relates spoken;
```



subtype attribute:

```
define

event-date sub attribute is-abstract datatype date;
birth-date sub event-date;
start-date sub event-date;
end-date sub event-date;

```



role:

```
define

people-with-same-parents-are-siblings sub rule,
  when {
    (mother: $m, $x) isa parentship;
    (mother: $m, $y) isa parentship;
    (father: $f, $x) isa parentship;
    (father: $f, $y) isa parentship;
    $x != $y;
  } then {
    ($x, $y) isa siblings;
  };
```



教授的研究領域和合作關係的資料庫，包含一個教授本身有它的所屬的單位，他是哪個學校哪個系所屬單位，他有他的研究領域，他是專長在電腦視覺 可能是自然語言處理，可能是語音辨認，這幾個都可以當attri，他目前是負責那一個專案，我現在轄下的21個專案，還有他餐與那些專案，他可能是A專案的負責人，但是他也可可能被邀請參加B專案，他目前跟國外的哪一個組織的哪一位教授也有合作關係(researc可能是local 也可能是國外的)，所以我們建立這個資料庫之後，之後我們可以QUERY說，有哪些老師在這個計畫裡，哪一個學校裡面，我們可以query這個學校有哪些教授，參與了那些計畫，像這類的，或是在哪一個領與裡面有哪些老師(attri裡面有哪些領域)，我們希望能夠定義好SCHEMA，我們會把轄下的計畫都input 整理好進去，然後透過query的方法可以做到啥，重點是一個老師他的專長，同樣的專案的角度來看，他也有採用的技術也會成為attri，當然我們部不放所有的detail，但是這個案子有他的TITLE 還有PI是誰(計畫主持人)，他還有共同主持人(COPI??)，還有involve的研究員(老師)，這是從人的角度來看，還有這個計畫所採用的技術，比如說這個專案可能會用到CV，他就會有CV的技術，他的主要的核心所使用的技術也會成為attri，所以我們也可以說，這個專案所使用的核心技術，有哪些老師也擅長這個領域，有可能找到這個PI還有他參與的人，也有可能會找到別的計畫，別的老師找出來(因為也擁有這些技術)，所以我們剛剛講說，我們可以想一下SCHEMA要怎麼訂，地好之後把資料放進去，然後可以用query作排列組合，下午想一下，目前attri並不多，包含 老師(researcher)，organization，project，還因為我們還有可能講說，因為project可能跟這個老師有關，這幾層關係都存在，那我們query的角度還說，可以做到啥



下午寫出一個建議的schema，不用真正打字畫一張圖，然後去隔壁的白板畫畫看，這個地方增加那些attr，增加甚麼link、relationship，做成第一個版本，然後我們之後put in writing，然後建立schema，然後建我們的keyspace出來，然後我們看看有這些之後，我們再把現有的資訊倒進去看看，因為我們可能會建立先從PI阿 幾個計畫丟進去，先丟比如說我們會先把機器人計畫丟進去看看效果怎麼樣，四個計畫丟進去大概有三四十個仁的資料進去，然後來看看



那原則上我希望今天結束之前 我們可以把schema建出來，交教授怎麼把資料放進去R，原則上希望今天結束之前schema放進去，這個禮拜之前，星期四可以verify 可以用! 剩下的時候趕快把資料道進去，因為schema建立好之後 就可以把之前的資料convert成schema inport 的 statement GOGOGOGGOGOGO
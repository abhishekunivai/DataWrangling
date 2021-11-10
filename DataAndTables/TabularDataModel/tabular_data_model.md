The Tabular Data Model
======================

```python--0d2591f5-99f1-4b47-addc-ded93ef4cf4d
import pandas as pd
```

```python--49c4a1f0-4471-4414-829e-78b80aa998d4
from collections import OrderedDict
def make_frame(list_of_tuples, legend):
    framelist=[]
    for i, cname in enumerate(legend):
        framelist.append((cname,[e[i] for e in list_of_tuples]))
    return pd.DataFrame.from_dict(OrderedDict(framelist)) 
```

Pandas
------

Here is what the data looks like from the file `data/candidates.txt`

```
id|first_name|last_name|middle_name|party
33|Joseph|Biden||D
36|Samuel|Brownback||R
34|Hillary|Clinton|R.|D
39|Christopher|Dodd|J.|D
26|John|Edwards||D
22|Rudolph|Giuliani||R
24|Mike|Gravel||D
16|Mike|Huckabee||R
30|Duncan|Hunter||R
31|Dennis|Kucinich||D
37|John|McCain||R
20|Barack|Obama||D
32|Ron|Paul||R
29|Bill|Richardson||D
35|Mitt|Romney||R
38|Tom|Tancredo||R
41|Fred|Thompson|D.|R
```

Use Pandas to read in the data

```python--44191eae-2feb-4428-8456-776b81311064
dfcand=pd.read_csv("data/candidates.txt", sep='|')
dfcand
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

first\_name

last\_name

middle\_name

party

0

33

Joseph

Biden

NaN

D

1

36

Samuel

Brownback

NaN

R

2

34

Hillary

Clinton

R.

D

3

39

Christopher

Dodd

J.

D

4

26

John

Edwards

NaN

D

5

22

Rudolph

Giuliani

NaN

R

6

24

Mike

Gravel

NaN

D

7

16

Mike

Huckabee

NaN

R

8

30

Duncan

Hunter

NaN

R

9

31

Dennis

Kucinich

NaN

D

10

37

John

McCain

NaN

R

11

20

Barack

Obama

NaN

D

12

32

Ron

Paul

NaN

R

13

29

Bill

Richardson

NaN

D

14

35

Mitt

Romney

NaN

R

15

38

Tom

Tancredo

NaN

R

16

41

Fred

Thompson

D.

R

Here is the other file, of contributions to candidates:

```
id|last_name|first_name|middle_name|street_1|street_2|city|state|zip|amount|date|candidate_id
|Agee|Steven||549 Laurel Branch Road||Floyd|VA|24091|500.00|2007-06-30|16
|Ahrens|Don||4034 Rennellwood Way||Pleasanton|CA|94566|250.00|2007-05-16|16
|Ahrens|Don||4034 Rennellwood Way||Pleasanton|CA|94566|50.00|2007-06-18|16
|Ahrens|Don||4034 Rennellwood Way||Pleasanton|CA|94566|100.00|2007-06-21|16
|Akin|Charles||10187 Sugar Creek Road||Bentonville|AR|72712|100.00|2007-06-16|16
|Akin|Mike||181 Baywood Lane||Monticello|AR|71655|1500.00|2007-05-18|16
|Akin|Rebecca||181 Baywood Lane||Monticello|AR|71655|500.00|2007-05-18|16
|Aldridge|Brittni||808 Capitol Square Place, SW||Washington|DC|20024|250.00|2007-06-06|16
|Allen|John D.||1052 Cannon Mill Drive||North Augusta|SC|29860|1000.00|2007-06-11|16
|Allen|John D.||1052 Cannon Mill Drive||North Augusta|SC|29860|1300.00|2007-06-29|16
|Allison|John W.||P.O. Box 1089||Conway|AR|72033|1000.00|2007-05-18|16
|Allison|Rebecca||3206 Summit Court||Little Rock|AR|72227|1000.00|2007-04-25|16
|Allison|Rebecca||3206 Summit Court||Little Rock|AR|72227|200.00|2007-06-12|16
|Altes|R.D.||8600 Moody Road||Fort Smith|AR|72903|2300.00|2007-06-21|16
|Andres|Dale||1160 Glen Oaks Drive||West Des Moines|IA|50266|250.00|2007-06-06|16
|Anthony|John||211 Long Island Drive||Hot Springs|AR|71913|2300.00|2007-06-12|16
|Arbogast|Robert||12900 State Route 56 SE||Mount Sterling|OH|43143|500.00|2007-04-08|16
|Arbogast|Robert||12900 State Route 56 SE||Mount Sterling|OH|43143|100.00|2007-06-22|16
|Ardle|William||412 Dakota Avenue||Springfield|OH|45504|50.00|2007-06-28|16
|Atiq|Omar||7200 S Hazel Street||Pine Bluff|AR|71603|1000.00|2007-05-18|16
|Atiq|Omar||7200 S Hazel Street||Pine Bluff|AR|71603|1000.00|2007-06-27|16
|Baker|David||2550 Adamsbrooke Drive||Conway|AR|72034|2300.00|2007-04-11|16
|Bancroft|David||2934 Broderick Street||San Francisco|CA|94123|250.00|2007-04-24|16
|Banks|Charles||P.O. Box 251310||Little Rock|AR|72225|1000.00|2007-05-14|16
|Barbee|John||516 Kellyridge Drive||Apex|NC|27502|500.00|2007-05-23|16
|Buckler|Steve||24351 Armada Dr||Dana Point|CA|926291306|50.00|2007-07-30|20
|Buckler|Steve||24351 Armada Dr||Dana Point|CA|926291306|25.00|2007-08-16|20
|Buckheit|Bruce||8904 KAREN DR||FAIRFAX|VA|220312731|100.00|2007-09-19|20
|Buckel|Linda||PO Box 683130||Park City|UT|840683130|2300.00|2007-08-14|20
|Buckel|Linda||PO Box 683130||Park City|UT|840683130|-2300.00|2007-08-14|20
|Buckel|Linda||PO Box 683130||Park City|UT|840683130|4600.00|2007-08-14|20
|Buck|Thomas||4206 Terrace Street||Kansas City|MO|64111|100.00|2007-09-25|20
|Buck|Jay|K.|1855 Old Willow Rd Unit 322||Northfield|IL|600932918|200.00|2007-09-12|20
|Buck|Blaine|M|45 Eaton Ave||Camden|ME|048431752|2300.00|2007-09-30|20
|Buck|Barbara||1780 NE 138th St||North Miami|FL|331811316|50.00|2007-09-13|20
|Buck|Barbara||1780 NE 138th St||North Miami|FL|331811316|50.00|2007-07-19|20
|Buchman|Mark M||2530 Lawton Ave||San Luis Obispo|CA|934015622|460.80|2007-07-18|20
|Bucher|Ida|M|1400 Warnall Ave||Los Angeles|CA|900245333|100.00|2007-07-10|20
|Buchanek|Elizabeth||7917 Kentbury Dr||Bethesda|MD|208144615|50.00|2007-09-30|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|500.00|2007-09-24|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|-500.00|2007-09-24|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|500.00|2007-09-24|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|700.00|2007-08-28|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|-700.00|2007-08-28|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|1000.00|2007-08-28|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|1300.00|2007-08-09|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|200.00|2007-08-14|20
|Buchanan|John||2025 NW 29th Rd||Boca Raton|FL|334316303|500.00|2007-07-25|20
|Buchanan|John||4635 49th St NW||Washington|DC|200164320|200.09|2007-09-23|20
|Harrison|Ryan||2247 3rd St||La Verne|CA|917504918|25.00|2007-07-26|20
|BYNUM|HERBERT||332 SUNNYSIDE ROAD||TAMPA|FL|336177249|-500.00|2008-03-10|22
|BYINGTON|MARGARET|E.|2633 MIDDLEBORO LANE N.E.||GRAND RAPIDS|MI|495061254|-2300.00|2008-03-03|22
|BYERS|BOB|A.|13170 TELFAIR AVENUE||SYLMAR|CA|913423573|-2300.00|2008-03-07|22
|BYERS|AUDREY||2658 LADBROOK WAY||THOUSAND OAKS|CA|913615073|-200.00|2008-03-07|22
|BUSH|KRYSTIE||P.O. BOX 61046||DENVER|CO|802061046|-2300.00|2008-03-06|22
|BUSH|ERIC||P.O. BOX 61046||DENVER|CO|802061046|-2300.00|2008-03-06|22
|BURTON|SUSAN||9338 DEER CREEK DRIVE||TAMPA|FL|336472286|-2300.00|2008-03-05|22
|BURTON|STEVEN|G.|9938 DEER CREEK DRIVE||TAMPA|FL|33647|-2300.00|2008-03-05|22
|BURTON|GLENN|M.|4404 CHARLESTON COURT||TAMPA|FL|336092620|-2300.00|2008-03-05|22
|BURKHARDT|CRAIG|S.|910 15TH STREET N.W.||WASHINGTON|DC|200052503|-500.00|2008-03-07|22
|BURKHARDT|CRAIG|S.|910 15TH STREET N.W.||WASHINGTON|DC|200052503|-1000.00|2008-03-07|22
|BURKHARDT|BARBARA||910 15TH STREET N.W.||WASHINGTON|DC|200052503|-500.00|2008-03-07|22
|BURKE|SUZANNE|M.|3401 EVANSTON||SEATTLE|WA|981038677|-700.00|2008-03-05|22
|BURKE|GAIL||165 E. 32ND STREET|APARTMENT 9E|NEW YORK|NY|100166014|-2000.00|2008-03-05|22
|BURKE|DONALD|J.|12 LOMPOC||RANCHO SANTA MARGA|CA|926881817|-2300.00|2008-03-11|22
|BURGERT|RONALD|L.|5723 PLUMTREE DRIVE||DALLAS|TX|752524926|-1000.00|2008-03-05|22
|BULL|BARTLE|B.|439 E. 51ST STREET||NEW YORK|NY|100226473|-800.00|2008-03-10|22
|BULL|BARTLE|B.|439 E. 51ST STREET||NEW YORK|NY|100226473|-1000.00|2008-03-10|22
|BUKOWSKI|DANIEL|J.|702 S. WRIGHT STREET||NAPERVILLE|IL|605406736|-100.00|2008-03-10|22
|BUISSON|MARGARET|A.|P.O. BOX 197029||LOUISVILLE|KY|402597029|-200.00|2008-03-11|22
|BUCKLEY|WALTER|W.|1635 COUNTRY ROAD||BETHLEHEM|PA|180155718|-100.00|2008-03-05|22
|BUCKLEY|MARJORIE|B.|1635 COUNTRY ROAD||BETHLEHEM|PA|180155718|-100.00|2008-03-05|22
|BRUNO|JOHN||10136 WINDERMERE CHASE BLVD.||GOTHA|FL|347344707|-2300.00|2008-03-06|22
|BRUNO|IRENE||10136 WINDERMERE CHASE BLVD.||GOTHA|FL|347344707|-2300.00|2008-03-06|22
|BROWN|TIMOTHY|J.|26826 MARLOWE COURT||STEVENSON RANCH|CA|913811020|-2300.00|2008-03-06|22
|Schuff|Bryan||1700 W Sweden Rd||Brockport|NY|14420|-25.00|2008-08-22|32
|Hobbs|James||229 Cherry Lane||White House|TN|37188|-25.00|2008-08-19|32
|Ranganath|Anoop||2507 Willard Drive||Charlottesville|VA|22903|-100.00|2008-04-21|32
|Nystrom|Michael|A|93A Fairmont Street||Arlington|MA|02474|-503.00|2008-04-21|32
|Muse|Nina|Jo|2915 Toro Canyon Rd||Austin|TX|78746|-50.00|2008-04-21|32
|Waddell|James|L.|1823 Spel Lane SW||Rochester|MN|55902|-28.00|2008-04-21|32
|Brucks|William|C.|PO Box 391||Corona del Mar|CA|92625|-150.00|2008-04-21|32
|Kuehn|David||14502 West 93rd Street||Lenexa|KS|66215|-330.00|2008-04-21|32
|Verster|Jeanette|M.|7220 SW 61st St||Miami|FL|331431807|-1000.00|2008-04-21|32
|Uihlein|Richard||1396 N Waukegan Rd||Lake Forest|IL|600451147|-2300.00|2008-04-21|32
|Eskenberry|Robert|P|10960 Gray Cir||Westminster|CO|80020|-223.00|2008-04-21|32
|Froehling|Alan|L.|302 Broadway St||Mount Vernon|IL|628645116|-844.80|2008-04-21|32
|Duryea|Marcia|A.|123 Bayview Ave||Amityville|NY|11701|-299.50|2008-04-21|32
|Perreault|Louise||503 Brockridge Hunt Drive||Hampton|VA|23666|-34.08|2008-04-21|32
|Rozenfeld|Timur||57 Herbert Road||Robbinsville|NJ|08691|-777.95|2008-04-21|32
|Kazor|Christopher|M|707 Spindletree ave||Naperville|IL|60565|-2592.00|2008-04-21|32
|Lehner|Thomas|S.|2701 Star Lane||Wadsworth|OH|44281|-200.00|2008-04-21|32
|Plummer|Joseph||587 Blake Hill Rd||New Hampton|NH|032564424|-24.60|2008-04-21|32
|Raught|Philip|M|4714 Plum Way||Pittsburgh|PA|15201|-1046.00|2008-04-21|32
|Ferrara|Judith|D|1508 Waterford Road||Yardley|PA|19067|-1100.00|2008-04-21|32
|Johnson|Cathleen|E.|1003 Justin Ln Apt 2016||Austin|TX|787572648|-14.76|2008-04-21|32
|Sanford|Bradley||940 Post St #43||San Francisco|CA|94109|-24.53|2008-04-21|32
|Gaarder|Bruce||PO Box 4085||Mountain Home AFB|ID|83648|-261.00|2008-04-21|32
|Choe|Hyeokchan||207 Bridle Way||Fort Lee|NJ|070246302|-39.50|2008-04-21|32
|Jacobs|Richard|G.|14337 Tawya Rd||Apple Valley|CA|923075545|-1000.00|2008-04-21|32
|Aaronson|Rebecca||2000 Village Green Dr Apt 12||Mill Creek|WA|980125787|100.00|2008-02-08|34
|Aarons|Elaine||481 Buck Island Rd Apt 17A|APT 17A|West Yarmouth|MA|026733300|25.00|2008-02-26|34
|Aarons|Elaine||481 Buck Island Rd Apt 17A|APT 17A|West Yarmouth|MA|026733300|70.00|2008-02-25|34
|Aarons|Elaine||481 Buck Island Rd Apt 17A|APT 17A|West Yarmouth|MA|026733300|100.00|2008-02-08|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|50.00|2008-02-29|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|100.00|2008-02-29|34
|Aaronson|Rebecca||2000 Village Green Dr Apt 12||Mill Creek|WA|980125787|100.00|2008-02-14|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|100.00|2008-02-24|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|100.00|2008-02-22|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|100.00|2008-02-17|34
|Reid|Elizabeth||73 W Patent Rd|OPHIR FARM NORTH|Bedford Hills|NY|105072222|-350.00|2008-08-28|34
|Reich|Thomas||499 Park Ave||New York|NY|100221240|-2300.00|2008-08-28|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|100.00|2008-02-08|34
|Aaron|Shirley||101 Cherry Ave||Havana|FL|323331311|100.00|2008-02-03|34
|Aaron|Sharron||1804 E Montgomery St||Broken Arrow|OK|740121840|500.00|2008-02-09|34
|Aaron|Patricia||418 NW 35th St||Oklahoma City|OK|731188602|200.00|2008-02-26|34
|Aaron|Patricia||418 NW 35th St||Oklahoma City|OK|731188602|100.00|2008-02-12|34
|Aaron|Jim||2178 Fairway Cir||Canton|MI|481885097|300.00|2008-02-07|34
|Aaron|Jim||2178 Fairway Cir||Canton|MI|481885097|200.00|2008-02-29|34
|Aaron|Carole||PO Box 1806||Ogunquit|ME|039071806|70.00|2008-02-29|34
|Aaron|Carole||PO Box 1806||Ogunquit|ME|039071806|50.00|2008-02-07|34
|Aaron|Carole||PO Box 1806||Ogunquit|ME|039071806|100.00|2008-02-03|34
|Aaron|Barbara||2298 Pacific Ave # 6||San Francisco|CA|941151435|1000.00|2008-02-11|34
|Aanonsen|Lin||897 Raymond Ave||Saint Paul|MN|551141508|250.00|2008-02-21|34
|Aanonsen|Lin||897 Raymond Ave||Saint Paul|MN|551141508|100.00|2008-02-08|34
|BOURNE|TRAVIS||LAGE KAART 77||BRASSCHATT||02930|-500.00|2008-11-20|35
|SECRIST|BRIAN|L.|3 MULE DEER TRAIL||LITTLETON|CO|801275722|-1000.00|2008-04-07|35
|TOLLESTRUP|TRAVIS|W.|16331 WINECREEK RD.||SAN DIEGO|CA|92127|-1000.00|2008-05-15|35
|ACCORD|DEAN|C.|8813 ROBINSON RIDGE ROAD||LAS VEGAS|NV|891175812|500.00|2007-07-13|35
|ABTS|HENRY||P. O. BOX 7299||INCLINE VILLAGE|NV|894527299|100.00|2007-07-13|35
|ABSHIER|LANNY||14191 S.E. HIGHWAY 301||SUMMERFIELD|FL|34491|500.00|2007-09-25|35
|ABSHIER|DIANA||14191 S.E. HIGHWAY 301||SUMMERFIELD|FL|34491|500.00|2007-09-25|35
|ABREU|KEVIN|M.|1305 GARDEN GLEN LANE||PEARLAND|TX|775816547|50.00|2007-09-30|35
|ABREU|KEVIN|M.|1305 GARDEN GLEN LANE||PEARLAND|TX|775816547|150.00|2007-08-09|35
|ABREU|KEVIN|M.|1305 GARDEN GLEN LANE||PEARLAND|TX|775816547|50.00|2007-07-19|35
|ABRAMOWITZ|NIRA||411 HARBOR ROAD||SOUTHPORT|CT|068901376|2300.00|2007-09-14|35
|ABRAMS|MICHAEL||7910 WOODMONT AVENUE||BETHESDA|MD|208143002|250.00|2007-09-29|35
|ABRAMOWITZ|KEN||200 CENTRAL PARK S.|APARTMENT 31A|NEW YORK|NY|100191448|300.00|2007-09-11|35
|ABOUBAKARE|NASAR||1400 SAN MIGUEL DRIVE||CORONA DEL MAR|CA|926251300|1000.00|2007-07-09|35
|ABEGG|PATRICIA|T.|1862 E. 5150 S.||SALT LAKE CITY|UT|841176911|75.00|2007-09-25|35
|ABEGG|PATRICIA|T.|1862 E. 5150 S.||SALT LAKE CITY|UT|841176911|25.00|2007-09-17|35
|ABEGG|PATRICIA|T.|1862 E. 5150 S.||SALT LAKE CITY|UT|841176911|75.00|2007-08-31|35
|ABEGG|PATRICIA|T.|1862 E. 5150 S.||SALT LAKE CITY|UT|841176911|75.00|2007-08-14|35
|ABEGG|PATRICIA|T.|1862 E. 5150 S.||SALT LAKE CITY|UT|841176911|25.00|2007-08-06|35
|ABEGG|PATRICIA|T.|1862 E. 5150 S.||SALT LAKE CITY|UT|841176911|25.00|2007-07-10|35
|ABDELLA|THOMAS|M.|4231 MONUMENT WALL WAY #340||FAIRFAX|VA|220308440|50.00|2007-09-30|35
|ABBOTT|WELDON|S.|777 EAST SOUTH TEMPLE  4E||SALT LAKE CITY|UT|841021269|100.00|2007-09-29|35
|ABBOTT|WELDON|S.|777 EAST SOUTH TEMPLE  4E||SALT LAKE CITY|UT|841021269|50.00|2007-08-09|35
|ABBOTT|GERALD|F.|389 BENEFIT STREET||PROVIDENCE|RI|029032946|100.00|2007-09-15|35
|ABBOTT|GERALD|F.|389 BENEFIT STREET||PROVIDENCE|RI|029032946|100.00|2007-08-15|35
|ABEDIN|ZAINUL||715 N. CENTRAL AVENUE|SUITE 212|GLENDALE|CA|912031164|500.00|2008-01-21|37
|ABBOTT|SYBIL|F.|446 GAMES DRIVE||RENO|NV|895093326|75.00|2008-01-08|37
|ABBOTT|SYBIL|F.|446 GAMES DRIVE||RENO|NV|895093326|50.00|2008-01-08|37
|ABBOTT|RONALD|LEANDER|5453 HAWTHORNE STREET||MONTCLAIR|CA|917632551|200.00|2008-01-31|37
|ABBOTT|RONALD|LEANDER|5453 HAWTHORNE STREET||MONTCLAIR|CA|917632551|100.00|2008-01-08|37
|ABBOTT|ROBERT|A.|3061 LOREE ROAD||DECKERVILLE|MI|484279763|500.00|2008-01-21|37
|ABBOTT|MIKE|E.|4516 OSPREY LNDG||NICEVILLE|FL|325786810|1000.00|2008-01-15|37
|ABBOT|DAVID|M.|56 SALEM STREET||ANDOVER|MA|018102114|200.00|2008-01-21|37
|ABBO|PAULINE|MORENCY|10720 JACOB LANE||WHITE LAKE|MI|483862274|35.00|2008-01-07|37
|ABATE|MARIA|ELENA|1291 NIGHTINGALE AVENUE||MIAMI SPRINGS|FL|331663832|2600.00|2008-01-25|37
|ABAIR|PETER||40 EVANS STREET||WATERTOWN|MA|024722150|25.00|2008-01-09|37
|ABACHERLI|SHIRLEY|M.|29875 NEWPORT ROAD||MENIFEE|CA|925849524|150.00|2008-01-28|37
|AARONS|CHARLES||1730 SHORE DRIVE||ANCHORAGE|AK|995153207|300.00|2008-01-30|37
|AARONS|CHARLES||1730 SHORE DRIVE||ANCHORAGE|AK|995153207|410.00|2008-01-15|37
|AARONS|CHARLES||1730 SHORE DRIVE||ANCHORAGE|AK|995153207|500.00|2008-01-09|37
|ABEL|JOHN|H.|422 THOMAS STREET||BETHLEHEM|PA|180153316|200.00|2008-01-22|37
|ABEL|MARLING|L.|14 HANGING MOSS LANE||GREENVILLE|SC|296155069|100.00|2008-01-22|37
|ABEL|RUDOLPH||4532 OCEAN BLVD.|# 108|SARASOTA|FL|342421337|100.00|2008-01-08|37
|ABELE|RODNEY||3620 METAIRIE HEIGHTS AVENUE||METAIRIE|LA|700021823|500.00|2008-01-15|37
|ABERCROMBIE|DENIS||11811 WATER OAK CT||MAGNOLIA|TX|773546270|500.00|2008-01-30|37
|ABESHAUS|MERRILL|M.|1801 N. HEREFORD DRIVE||FLAGSTAFF|AZ|860011121|120.00|2008-01-16|37
|ABRAHAM|GEORGE||P.O. BOX 1504||LAKE CHARLES|LA|706021504|800.00|2008-01-17|37
|ABRAHAMSON|PETER|J.|1030 W. ROSCOE STREET||CHICAGO|IL|606572207|50.00|2008-01-25|37
|ABRAHAM|SALEM|A.|P.O. BOX 7||CANADIAN|TX|790140007|1000.00|2008-01-17|37
|ABRAHAM|SALEM|A.|P.O. BOX 7||CANADIAN|TX|790140007|1300.00|2008-01-30|37
```

```python--1286f0a9-362e-402c-b6d6-32ce68249746
dfcwci=pd.read_csv("data/contributors_with_candidate_id.txt", sep="|")
dfcwci.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

NaN

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.0

2007-06-30

16

1

NaN

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

250.0

2007-05-16

16

2

NaN

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

50.0

2007-06-18

16

3

NaN

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

100.0

2007-06-21

16

4

NaN

Akin

Charles

NaN

10187 Sugar Creek Road

NaN

Bentonville

AR

72712

100.0

2007-06-16

16

You'll notice that the contributions dont have the first column, so we will need to be cleaning things up a bit...

```python--c58d6945-cf55-4273-963f-414558b5cd01
del dfcwci['id']
dfcwci.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.0

2007-06-30

16

1

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

250.0

2007-05-16

16

2

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

50.0

2007-06-18

16

3

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

100.0

2007-06-21

16

4

Akin

Charles

NaN

10187 Sugar Creek Road

NaN

Bentonville

AR

72712

100.0

2007-06-16

16

SQL and Relational Databases
----------------------------

Lets start with Relational Databases, so called because they contain "relations" (tables), which are SETS of "tuples" (rows) which map "attributes" (columns) to atomic values.

The available attributes are constrained by a "header" tuple of attributes which set the type. We do this below here, using the SQL language to set things up.

```sql
DROP TABLE IF EXISTS "candidates";
DROP TABLE IF EXISTS "contributors";
CREATE TABLE "candidates" (
    "id" INTEGER PRIMARY KEY  NOT NULL ,
    "first_name" VARCHAR,
    "last_name" VARCHAR,
    "middle_name" VARCHAR,
    "party" VARCHAR NOT NULL
);
CREATE TABLE "contributors" (
    "id" INTEGER PRIMARY KEY  AUTOINCREMENT  NOT NULL,
    "last_name" VARCHAR,
    "first_name" VARCHAR,
    "middle_name" VARCHAR,
    "street_1" VARCHAR,
    "street_2" VARCHAR,
    "city" VARCHAR,
    "state" VARCHAR,
    "zip" VARCHAR, -- Notice that we are converting the zip from integer to string
    "amount" INTEGER,
    "date" DATETIME,
    "candidate_id" INTEGER NOT NULL,
    FOREIGN KEY(candidate_id) REFERENCES candidates(id)
);
```

```python--883e616a-14ae-4443-b5d5-b5fdf5ba62b6
ourschema="""
DROP TABLE IF EXISTS "candidates";
DROP TABLE IF EXISTS "contributors";
CREATE TABLE "candidates" (
    "id" INTEGER PRIMARY KEY  NOT NULL ,
    "first_name" VARCHAR,
    "last_name" VARCHAR,
    "middle_name" VARCHAR,
    "party" VARCHAR NOT NULL
);
CREATE TABLE "contributors" (
    "id" INTEGER PRIMARY KEY  AUTOINCREMENT  NOT NULL,
    "last_name" VARCHAR,
    "first_name" VARCHAR,
    "middle_name" VARCHAR,
    "street_1" VARCHAR,
    "street_2" VARCHAR,
    "city" VARCHAR,
    "state" VARCHAR,
    "zip" VARCHAR, -- Notice that we are converting the zip from integer to string
    "amount" INTEGER,
    "date" DATETIME,
    "candidate_id" INTEGER NOT NULL,
    FOREIGN KEY(candidate_id) REFERENCES candidates(id)
);
"""
```

### SQLITE

We use sqlite here (and recommend Postgres for production purposes). Sqlite is a on-file database, as opposed to other common databases such as Oracle and Postgres, which run as different processes on your system. Sqlite is great for on-disk large databases which wont fit into memory.

Its also built into Python, but to use the [command line tool](https://www.sqlite.org/cli.html), I recommend you install it: https://www.sqlite.org/download.html. I also recommend you download and install the sqlite browser: http://sqlitebrowser.org .

Python implements a standard database API over all databases. Its called [DBAPI2](http://cewing.github.io/training.codefellows/lectures/day21/intro_to_dbapi2.html). It works across many SQL databases.

There is an even higher level API available, called [SQLAlchemy](http://www.sqlalchemy.org). While we wont use it here, I thoroughly recommend it. Many things in Pandas use it to interface with databases. Here we'll get away with things by using SQLITE.

We'll write some functions to connect to Sqlite.

(1) Connect and get a DBAPI2 connection.

```python--cb4a21ce-6c42-45b1-963c-7b8f8499807a
from sqlite3 import dbapi2 as sq3
from pathlib import Path
PATHSTART="."
def get_db(dbfile):
    sqlite_db = sq3.connect(Path(PATHSTART) / dbfile)
    return sqlite_db
```

(2) Set up the database with tables. Drop tables if they exist and create them.

```python--5dee599b-05a7-4956-9b9c-6acbbac5d38d
def init_db(dbfile, schema):
    """Creates the database tables."""
    db = get_db(dbfile) 
    db.cursor().executescript(schema)
    db.commit()
    return db
```

Initializing the database:

```python--a1c34c0c-f985-4c18-96f9-2a63cc793d34
db=init_db("/tmp/cancont.db", ourschema)
```

### Populating with Pandas!!

```python--a2c8fbe8-f621-496a-afa7-db7eaa036a83
dfcand.to_sql("candidates", db, if_exists="append", index=False)
```

```python--06651f7d-eae5-4b38-936d-cc96ffc9d706
dfcwci.to_sql("contributors", db, if_exists="append", index=False)
```

Now we can do queries in the lingua franca of databases: SQL

```python--00dcb810-9ed7-4eba-af29-f53e07ddc596
sel="""
SELECT * FROM candidates;
"""
c=db.cursor().execute(sel)
```

```python--cba599aa-9f08-4647-b362-b94ef2b7fe53
c.fetchall()
```

```output--cba599aa-9f08-4647-b362-b94ef2b7fe53
[(16, 'Mike', 'Huckabee', None, 'R'),
 (20, 'Barack', 'Obama', None, 'D'),
 (22, 'Rudolph', 'Giuliani', None, 'R'),
 (24, 'Mike', 'Gravel', None, 'D'),
 (26, 'John', 'Edwards', None, 'D'),
 (29, 'Bill', 'Richardson', None, 'D'),
 (30, 'Duncan', 'Hunter', None, 'R'),
 (31, 'Dennis', 'Kucinich', None, 'D'),
 (32, 'Ron', 'Paul', None, 'R'),
 (33, 'Joseph', 'Biden', None, 'D'),
 (34, 'Hillary', 'Clinton', 'R.', 'D'),
 (35, 'Mitt', 'Romney', None, 'R'),
 (36, 'Samuel', 'Brownback', None, 'R'),
 (37, 'John', 'McCain', None, 'R'),
 (38, 'Tom', 'Tancredo', None, 'R'),
 (39, 'Christopher', 'Dodd', 'J.', 'D'),
 (41, 'Fred', 'Thompson', 'D.', 'R')]
```

```python--b3b6e767-835e-43bd-8392-2e9ee2824270
def make_query(sel):
    c=db.cursor().execute(sel)
    return c.fetchall()
```

```python--ca0e0eee-a102-41c1-8589-6996287842da
make_query("SELECT * FROM candidates;")
```

```output--ca0e0eee-a102-41c1-8589-6996287842da
[(16, 'Mike', 'Huckabee', None, 'R'),
 (20, 'Barack', 'Obama', None, 'D'),
 (22, 'Rudolph', 'Giuliani', None, 'R'),
 (24, 'Mike', 'Gravel', None, 'D'),
 (26, 'John', 'Edwards', None, 'D'),
 (29, 'Bill', 'Richardson', None, 'D'),
 (30, 'Duncan', 'Hunter', None, 'R'),
 (31, 'Dennis', 'Kucinich', None, 'D'),
 (32, 'Ron', 'Paul', None, 'R'),
 (33, 'Joseph', 'Biden', None, 'D'),
 (34, 'Hillary', 'Clinton', 'R.', 'D'),
 (35, 'Mitt', 'Romney', None, 'R'),
 (36, 'Samuel', 'Brownback', None, 'R'),
 (37, 'John', 'McCain', None, 'R'),
 (38, 'Tom', 'Tancredo', None, 'R'),
 (39, 'Christopher', 'Dodd', 'J.', 'D'),
 (41, 'Fred', 'Thompson', 'D.', 'R')]
```

```python--b1949a8a-0347-47aa-a89c-5d6c739f142e
make_query("PRAGMA table_info(candidates);")
```

```output--b1949a8a-0347-47aa-a89c-5d6c739f142e
[(0, 'id', 'INTEGER', 1, None, 1),
 (1, 'first_name', 'VARCHAR', 0, None, 0),
 (2, 'last_name', 'VARCHAR', 0, None, 0),
 (3, 'middle_name', 'VARCHAR', 0, None, 0),
 (4, 'party', 'VARCHAR', 1, None, 0)]
```

```python--61d4e1d3-8b82-4eaf-a2d1-fbd8b8de650b
make_query("PRAGMA table_info(contributors);")
```

```output--61d4e1d3-8b82-4eaf-a2d1-fbd8b8de650b
[(0, 'id', 'INTEGER', 1, None, 1),
 (1, 'last_name', 'VARCHAR', 0, None, 0),
 (2, 'first_name', 'VARCHAR', 0, None, 0),
 (3, 'middle_name', 'VARCHAR', 0, None, 0),
 (4, 'street_1', 'VARCHAR', 0, None, 0),
 (5, 'street_2', 'VARCHAR', 0, None, 0),
 (6, 'city', 'VARCHAR', 0, None, 0),
 (7, 'state', 'VARCHAR', 0, None, 0),
 (8, 'zip', 'VARCHAR', 0, None, 0),
 (9, 'amount', 'INTEGER', 0, None, 0),
 (10, 'date', 'DATETIME', 0, None, 0),
 (11, 'candidate_id', 'INTEGER', 1, None, 0)]
```

```python--86b87f8b-0542-42d6-a38b-71454f5e8f6a
candidate_cols = [e[1] for e in make_query("PRAGMA table_info(candidates);")]
candidate_cols
```

```output--86b87f8b-0542-42d6-a38b-71454f5e8f6a
['id', 'first_name', 'last_name', 'middle_name', 'party']
```

```python--5f74639d-2a8d-42ff-ae11-0211053fe2e9
contributor_cols = [e[1] for e in make_query("PRAGMA table_info(contributors);")]
contributor_cols
```

```output--5f74639d-2a8d-42ff-ae11-0211053fe2e9
['id',
 'last_name',
 'first_name',
 'middle_name',
 'street_1',
 'street_2',
 'city',
 'state',
 'zip',
 'amount',
 'date',
 'candidate_id']
```

```python--17bdcacb-bae5-44f1-b5c9-907479218f40
out=make_query("SELECT * FROM candidates;")
make_frame(out, legend=candidate_cols)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

first\_name

last\_name

middle\_name

party

0

16

Mike

Huckabee

None

R

1

20

Barack

Obama

None

D

2

22

Rudolph

Giuliani

None

R

3

24

Mike

Gravel

None

D

4

26

John

Edwards

None

D

5

29

Bill

Richardson

None

D

6

30

Duncan

Hunter

None

R

7

31

Dennis

Kucinich

None

D

8

32

Ron

Paul

None

R

9

33

Joseph

Biden

None

D

10

34

Hillary

Clinton

R.

D

11

35

Mitt

Romney

None

R

12

36

Samuel

Brownback

None

R

13

37

John

McCain

None

R

14

38

Tom

Tancredo

None

R

15

39

Christopher

Dodd

J.

D

16

41

Fred

Thompson

D.

R

THE GRAMMAR OF DATA
-------------------

Let us now focus on core data manipulation commands. The reason to do this is that they are _universal across systems, and by identifying them, we can quickly ask how to do these_ when we encounter a new system.

See https://gist.github.com/TomAugspurger/6e052140eaa5fdb6e8c0/ which has a comparison of r/dplyr and pandas. I stole and modified this table from there:

`dplyr` has a small set of nicely defined verbs, which Hadley Wickham has used to identify core data manipulation commands. Here are listed the closest SQL and Pandas verbs, so we can see the universality of these manipulations.

**VERB**

**dplyr**

**pandas**

**SQL**

QUERY/SELECTION

filter() (and slice())

query() (and loc\[\], iloc\[\])

SELECT WHERE

SORT

arrange()

sort\_values()

ORDER BY

SELECT-COLUMNS/PROJECTION

select() (and rename())

\[\](\_\_getitem\_\_) (and rename())

SELECT COLUMN

SELECT-DISTINCT

distinct()

unique(),drop\_duplicates()

SELECT DISTINCT COLUMN

ASSIGN

mutate() (and transmute())

assign

ALTER/UPDATE

AGGREGATE

summarise()

describe(), mean(), max()

None, AVG(),MAX()

SAMPLE

sample\_n() and sample\_frac()

sample()

implementation dep, use RAND()

GROUP-AGG

group\_by/summarize

groupby/agg, count, mean

GROUP BY

DELETE

?

drop/masking

DELETE/WHERE

### QUERY

We'll want to make queries on columns that are both numerical and categorical, combining these queries when appropriate...

```python--b67edc34-fa16-4059-b89b-8f1e0c0040ab
dfcwci.query("20 <= amount <= 40")
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

26

Buckler

Steve

NaN

24351 Armada Dr

NaN

Dana Point

CA

926291306

25.0

2007-08-16

20

49

Harrison

Ryan

NaN

2247 3rd St

NaN

La Verne

CA

917504918

25.0

2007-07-26

20

101

Aarons

Elaine

NaN

481 Buck Island Rd Apt 17A

APT 17A

West Yarmouth

MA

26733300

25.0

2008-02-26

34

140

ABEGG

PATRICIA

T.

1862 E. 5150 S.

NaN

SALT LAKE CITY

UT

841176911

25.0

2007-09-17

35

143

ABEGG

PATRICIA

T.

1862 E. 5150 S.

NaN

SALT LAKE CITY

UT

841176911

25.0

2007-08-06

35

144

ABEGG

PATRICIA

T.

1862 E. 5150 S.

NaN

SALT LAKE CITY

UT

841176911

25.0

2007-07-10

35

158

ABBO

PAULINE

MORENCY

10720 JACOB LANE

NaN

WHITE LAKE

MI

483862274

35.0

2008-01-07

37

160

ABAIR

PETER

NaN

40 EVANS STREET

NaN

WATERTOWN

MA

24722150

25.0

2008-01-09

37

```python--f8014812-cdc6-45bc-9e68-8d41a0dde236
out=make_query("SELECT * FROM contributors WHERE amount BETWEEN 20 AND 40;")
make_frame(out, legend=contributor_cols)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

27

Buckler

Steve

None

24351 Armada Dr

None

Dana Point

CA

926291306

25

2007-08-16

20

1

50

Harrison

Ryan

None

2247 3rd St

None

La Verne

CA

917504918

25

2007-07-26

20

2

102

Aarons

Elaine

None

481 Buck Island Rd Apt 17A

APT 17A

West Yarmouth

MA

26733300

25

2008-02-26

34

3

141

ABEGG

PATRICIA

T.

1862 E. 5150 S.

None

SALT LAKE CITY

UT

841176911

25

2007-09-17

35

4

144

ABEGG

PATRICIA

T.

1862 E. 5150 S.

None

SALT LAKE CITY

UT

841176911

25

2007-08-06

35

5

145

ABEGG

PATRICIA

T.

1862 E. 5150 S.

None

SALT LAKE CITY

UT

841176911

25

2007-07-10

35

6

159

ABBO

PAULINE

MORENCY

10720 JACOB LANE

None

WHITE LAKE

MI

483862274

35

2008-01-07

37

7

161

ABAIR

PETER

None

40 EVANS STREET

None

WATERTOWN

MA

24722150

25

2008-01-09

37

You can combine queries on different columns (here a numerical and a categorical):

```python--b5314f0f-9675-41be-aaba-b54ff252da6d
dfcwci.query("state=='VA' & amount < 400")
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

27

Buckheit

Bruce

NaN

8904 KAREN DR

NaN

FAIRFAX

VA

220312731

100.00

2007-09-19

20

77

Ranganath

Anoop

NaN

2507 Willard Drive

NaN

Charlottesville

VA

22903

\-100.00

2008-04-21

32

88

Perreault

Louise

NaN

503 Brockridge Hunt Drive

NaN

Hampton

VA

23666

\-34.08

2008-04-21

32

145

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

NaN

FAIRFAX

VA

220308440

50.00

2007-09-30

35

```python--640e6acb-1214-4bc2-aa81-ec58e8040b72
dfcwci[(dfcwci.state=='VA') & (dfcwci.amount < 400)]
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

27

Buckheit

Bruce

NaN

8904 KAREN DR

NaN

FAIRFAX

VA

220312731

100.00

2007-09-19

20

77

Ranganath

Anoop

NaN

2507 Willard Drive

NaN

Charlottesville

VA

22903

\-100.00

2008-04-21

32

88

Perreault

Louise

NaN

503 Brockridge Hunt Drive

NaN

Hampton

VA

23666

\-34.08

2008-04-21

32

145

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

NaN

FAIRFAX

VA

220308440

50.00

2007-09-30

35

```python--c50656a2-1541-46ba-bae7-aaf7d3dc0b33
out=make_query("SELECT * FROM contributors WHERE state='VA' AND amount < 400;")
make_frame(out, legend=contributor_cols)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

28

Buckheit

Bruce

None

8904 KAREN DR

None

FAIRFAX

VA

220312731

100.00

2007-09-19

20

1

78

Ranganath

Anoop

None

2507 Willard Drive

None

Charlottesville

VA

22903

\-100.00

2008-04-21

32

2

89

Perreault

Louise

None

503 Brockridge Hunt Drive

None

Hampton

VA

23666

\-34.08

2008-04-21

32

3

146

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

None

FAIRFAX

VA

220308440

50.00

2007-09-30

35

Queries that look if things are in a list...useful for categorical variables or discrete valued numerical variables...

```python--2899aabd-4b72-431d-8c55-42acdc368017
dfcwci[dfcwci.state.isin(['VA','WA'])].head(10)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.00

2007-06-30

16

27

Buckheit

Bruce

NaN

8904 KAREN DR

NaN

FAIRFAX

VA

220312731

100.00

2007-09-19

20

62

BURKE

SUZANNE

M.

3401 EVANSTON

NaN

SEATTLE

WA

981038677

\-700.00

2008-03-05

22

77

Ranganath

Anoop

NaN

2507 Willard Drive

NaN

Charlottesville

VA

22903

\-100.00

2008-04-21

32

88

Perreault

Louise

NaN

503 Brockridge Hunt Drive

NaN

Hampton

VA

23666

\-34.08

2008-04-21

32

100

Aaronson

Rebecca

NaN

2000 Village Green Dr Apt 12

NaN

Mill Creek

WA

980125787

100.00

2008-02-08

34

106

Aaronson

Rebecca

NaN

2000 Village Green Dr Apt 12

NaN

Mill Creek

WA

980125787

100.00

2008-02-14

34

145

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

NaN

FAIRFAX

VA

220308440

50.00

2007-09-30

35

```python--a191f2b6-2dbc-4a37-af25-cde9898d54f1
out=make_query("SELECT * FROM contributors WHERE state IN ('VA','WA');")
make_frame(out, legend=contributor_cols).head(10)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

1

Agee

Steven

None

549 Laurel Branch Road

None

Floyd

VA

24091

500.00

2007-06-30

16

1

28

Buckheit

Bruce

None

8904 KAREN DR

None

FAIRFAX

VA

220312731

100.00

2007-09-19

20

2

63

BURKE

SUZANNE

M.

3401 EVANSTON

None

SEATTLE

WA

981038677

\-700.00

2008-03-05

22

3

78

Ranganath

Anoop

None

2507 Willard Drive

None

Charlottesville

VA

22903

\-100.00

2008-04-21

32

4

89

Perreault

Louise

None

503 Brockridge Hunt Drive

None

Hampton

VA

23666

\-34.08

2008-04-21

32

5

101

Aaronson

Rebecca

None

2000 Village Green Dr Apt 12

None

Mill Creek

WA

980125787

100.00

2008-02-08

34

6

107

Aaronson

Rebecca

None

2000 Village Green Dr Apt 12

None

Mill Creek

WA

980125787

100.00

2008-02-14

34

7

146

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

None

FAIRFAX

VA

220308440

50.00

2007-09-30

35

### SELECT-COLUMNS

Sometimes we only want to get a few columns, not the entire table

```python--bfc5f073-bd88-4fcd-a264-1111babbd76c
dfcwci[['first_name', 'amount']].head(10)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

first\_name

amount

0

Steven

500.0

1

Don

250.0

2

Don

50.0

3

Don

100.0

4

Charles

100.0

5

Mike

1500.0

6

Rebecca

500.0

7

Brittni

250.0

8

John D.

1000.0

9

John D.

1300.0

```python--d000d795-cb56-40a4-acde-2e391e74ae16
out=make_query("SELECT first_name, amount FROM contributors;")
make_frame(out,['first_name', 'amount']).head(10)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

first\_name

amount

0

Steven

500.0

1

Don

250.0

2

Don

50.0

3

Don

100.0

4

Charles

100.0

5

Mike

1500.0

6

Rebecca

500.0

7

Brittni

250.0

8

John D.

1000.0

9

John D.

1300.0

### AGGREGATE

```python--baab69c7-b8c1-490f-a82c-8de3a647a531
dfcwci.describe()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

zip

amount

candidate\_id

count

1.750000e+02

175.000000

175.000000

mean

3.780014e+08

3.418114

28.000000

std

3.628278e+08

1028.418999

7.823484

min

2.474000e+03

\-2592.000000

16.000000

25%

9.336700e+04

\-175.000000

20.000000

50%

3.233313e+08

100.000000

32.000000

75%

7.816946e+08

300.000000

35.000000

max

9.951532e+08

4600.000000

37.000000

```python--4d3358b2-ae39-4414-bf63-acd59bf5e9c5
dfcwci.amount.max()
```

```output--4d3358b2-ae39-4414-bf63-acd59bf5e9c5
4600.0
```

SQL is actually simpler

```python--aeae81bb-715f-424e-ac95-ef75f3d45284
out=make_query("SELECT MAX(amount) FROM contributors;")
out
```

```output--aeae81bb-715f-424e-ac95-ef75f3d45284
[(4600,)]
```

Aso `MIN`, `SUM`, `AVG`.

### GROUP-AGG

Being able to group data by the value of any column is critical functionality. This is how you understand your sampling, and the distributions of various quantities in your data.

```python--d838eb9e-d8c6-4dec-a314-9ebea7642764
dfcwci.groupby("state").sum()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

zip

amount

candidate\_id

state

AK

2985459621

1210.00

111

AR

864790

14200.00

192

AZ

860011121

120.00

37

CA

14736360720

\-5013.73

600

CO

2405477834

\-5823.00

111

CT

68901376

2300.00

35

DC

800341853

\-1549.91

102

FL

8970626520

\-4050.00

803

IA

50266

250.00

16

ID

83648

\-261.00

32

IL

3042068689

\-5586.80

175

KS

66215

\-330.00

32

KY

402597029

\-200.00

22

LA

1406043327

1300.00

74

MA

123026638

\-83.00

208

MD

416287617

300.00

55

ME

165647170

2520.00

122

MI

2426973485

\-1265.00

164

MN

1102338918

322.00

100

MO

64111

100.00

20

NC

27502

500.00

16

NH

32564424

\-24.60

32

NJ

70254993

\-817.45

64

NV

3575889763

725.00

144

NY

606129991

\-6474.50

233

OH

176071

450.00

80

OK

2202499044

800.00

102

PA

540499020

\-2146.00

145

RI

58065892

200.00

70

SC

296214789

2400.00

69

TN

37188

\-25.00

32

TX

6221452245

1985.24

302

UT

9251153394

5050.00

340

VA

440691831

515.92

135

WA

2941290251

\-500.00

90

```python--c2c7c1e0-08c2-49c1-9c0c-b35d90b80c5c
dfcwci.groupby("state")['amount'].mean()
```

```output--c2c7c1e0-08c2-49c1-9c0c-b35d90b80c5c
state
AK     403.333333
AR    1183.333333
AZ     120.000000
CA    -217.988261
CO   -1455.750000
CT    2300.000000
DC    -309.982000
FL    -135.000000
IA     250.000000
ID    -261.000000
IL    -931.133333
KS    -330.000000
KY    -200.000000
LA     650.000000
MA     -13.833333
MD     150.000000
ME     630.000000
MI    -253.000000
MN     107.333333
MO     100.000000
NC     500.000000
NH     -24.600000
NJ    -408.725000
NV     181.250000
NY    -809.312500
OH     112.500000
OK     266.666667
PA    -429.200000
RI     100.000000
SC     800.000000
TN     -25.000000
TX     220.582222
UT     459.090909
VA     103.184000
WA    -166.666667
Name: amount, dtype: float64
```

```python--12b377ea-d775-4986-9fed-b33341eddb13
out=make_query("SELECT state,SUM(amount) FROM contributors GROUP BY state;")
make_frame(out, legend=['state','sum'])
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

state

sum

0

None

\-500.00

1

AK

1210.00

2

AR

14200.00

3

AZ

120.00

4

CA

\-5013.73

5

CO

\-5823.00

6

CT

2300.00

7

DC

\-1549.91

8

FL

\-4050.00

9

IA

250.00

10

ID

\-261.00

11

IL

\-5586.80

12

KS

\-330.00

13

KY

\-200.00

14

LA

1300.00

15

MA

\-83.00

16

MD

300.00

17

ME

2520.00

18

MI

\-1265.00

19

MN

322.00

20

MO

100.00

21

NC

500.00

22

NH

\-24.60

23

NJ

\-817.45

24

NV

725.00

25

NY

\-6474.50

26

OH

450.00

27

OK

800.00

28

PA

\-2146.00

29

RI

200.00

30

SC

2400.00

31

TN

\-25.00

32

TX

1985.24

33

UT

5050.00

34

VA

515.92

35

WA

\-500.00

Creation and Alteration
-----------------------

So far, when we created the database, we did it using Pandas. Clearly, one ought to be able to populate a SQL database using SQL. We now turn to this use case, as well as the alteration of databases.

### Populate with SQL INSERT

Before we populate a the `candidates` table, lets delete all data from it...

```python--f30a5a59-2013-4dbb-acb8-572d8a4583e3
rem="""
DELETE FROM candidates;
"""
c=db.cursor().execute(rem)
db.commit()
```

Once again, lets look at the structure of the candidates file.

Here is what the data looks like from the file `data/candidates.txt`

```
id|first_name|last_name|middle_name|party
33|Joseph|Biden||D
36|Samuel|Brownback||R
34|Hillary|Clinton|R.|D
39|Christopher|Dodd|J.|D
26|John|Edwards||D
22|Rudolph|Giuliani||R
24|Mike|Gravel||D
16|Mike|Huckabee||R
30|Duncan|Hunter||R
31|Dennis|Kucinich||D
37|John|McCain||R
20|Barack|Obama||D
32|Ron|Paul||R
29|Bill|Richardson||D
35|Mitt|Romney||R
38|Tom|Tancredo||R
41|Fred|Thompson|D.|R
```

We compose an insertion template using the SQL insertion command...

```python--dedae323-8677-4606-8753-9445464e3d75
ins="""
INSERT INTO candidates (id, first_name, last_name, middle_name, party) \
    VALUES (?,?,?,?,?);
"""
```

Now we read the file line by line, not including the header line and slurp in the data. Notice that we only finish the transaction after we have slurped in all the lines. So its all lines or none. When we execute the cursor, the question marks are used a templates with a tuple provided in..

```python--b5d8cc03-3e56-4a92-b466-108031c4ed41
with open("data/candidates.txt") as fd:
    slines =[l.strip().split('|') for l in fd.readlines()]
    for line in slines[1:]:
        theid, first_name, last_name, middle_name, party = line
        print(theid, first_name, last_name, middle_name, party)
        valstoinsert = (int(theid), first_name, last_name, middle_name, party)
        print(ins, valstoinsert)
        db.cursor().execute(ins, valstoinsert)
        
db.commit()    
```

```output--b5d8cc03-3e56-4a92-b466-108031c4ed41
33 Joseph Biden  D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (33, 'Joseph', 'Biden', '', 'D')
36 Samuel Brownback  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (36, 'Samuel', 'Brownback', '', 'R')
34 Hillary Clinton R. D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (34, 'Hillary', 'Clinton', 'R.', 'D')
39 Christopher Dodd J. D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (39, 'Christopher', 'Dodd', 'J.', 'D')
26 John Edwards  D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (26, 'John', 'Edwards', '', 'D')
22 Rudolph Giuliani  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (22, 'Rudolph', 'Giuliani', '', 'R')
24 Mike Gravel  D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (24, 'Mike', 'Gravel', '', 'D')
16 Mike Huckabee  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (16, 'Mike', 'Huckabee', '', 'R')
30 Duncan Hunter  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (30, 'Duncan', 'Hunter', '', 'R')
31 Dennis Kucinich  D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (31, 'Dennis', 'Kucinich', '', 'D')
37 John McCain  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (37, 'John', 'McCain', '', 'R')
20 Barack Obama  D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (20, 'Barack', 'Obama', '', 'D')
32 Ron Paul  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (32, 'Ron', 'Paul', '', 'R')
29 Bill Richardson  D

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (29, 'Bill', 'Richardson', '', 'D')
35 Mitt Romney  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (35, 'Mitt', 'Romney', '', 'R')
38 Tom Tancredo  R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (38, 'Tom', 'Tancredo', '', 'R')
41 Fred Thompson D. R

INSERT INTO candidates (id, first_name, last_name, middle_name, party)     VALUES (?,?,?,?,?);
 (41, 'Fred', 'Thompson', 'D.', 'R')

```

```python--b90a5d96-5fa2-437d-b44e-85055234eb88
make_query("SELECT * FROM candidates;")
```

```output--b90a5d96-5fa2-437d-b44e-85055234eb88
[(16, 'Mike', 'Huckabee', '', 'R'),
 (20, 'Barack', 'Obama', '', 'D'),
 (22, 'Rudolph', 'Giuliani', '', 'R'),
 (24, 'Mike', 'Gravel', '', 'D'),
 (26, 'John', 'Edwards', '', 'D'),
 (29, 'Bill', 'Richardson', '', 'D'),
 (30, 'Duncan', 'Hunter', '', 'R'),
 (31, 'Dennis', 'Kucinich', '', 'D'),
 (32, 'Ron', 'Paul', '', 'R'),
 (33, 'Joseph', 'Biden', '', 'D'),
 (34, 'Hillary', 'Clinton', 'R.', 'D'),
 (35, 'Mitt', 'Romney', '', 'R'),
 (36, 'Samuel', 'Brownback', '', 'R'),
 (37, 'John', 'McCain', '', 'R'),
 (38, 'Tom', 'Tancredo', '', 'R'),
 (39, 'Christopher', 'Dodd', 'J.', 'D'),
 (41, 'Fred', 'Thompson', 'D.', 'R')]
```

### Create new columns with ASSIGN

In Pandas it is simple to create a new column (`pd.Series`) in the dataframe:

```python--05743f9d-a3f3-40dd-b9c5-25f67f90adfe
dfcwci['name']=dfcwci['last_name']+", "+dfcwci['first_name']
dfcwci.head(10)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

name

0

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.0

2007-06-30

16

Agee, Steven

1

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

250.0

2007-05-16

16

Ahrens, Don

2

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

50.0

2007-06-18

16

Ahrens, Don

3

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

100.0

2007-06-21

16

Ahrens, Don

4

Akin

Charles

NaN

10187 Sugar Creek Road

NaN

Bentonville

AR

72712

100.0

2007-06-16

16

Akin, Charles

5

Akin

Mike

NaN

181 Baywood Lane

NaN

Monticello

AR

71655

1500.0

2007-05-18

16

Akin, Mike

6

Akin

Rebecca

NaN

181 Baywood Lane

NaN

Monticello

AR

71655

500.0

2007-05-18

16

Akin, Rebecca

7

Aldridge

Brittni

NaN

808 Capitol Square Place, SW

NaN

Washington

DC

20024

250.0

2007-06-06

16

Aldridge, Brittni

8

Allen

John D.

NaN

1052 Cannon Mill Drive

NaN

North Augusta

SC

29860

1000.0

2007-06-11

16

Allen, John D.

9

Allen

John D.

NaN

1052 Cannon Mill Drive

NaN

North Augusta

SC

29860

1300.0

2007-06-29

16

Allen, John D.

One can also use `assign`, which creates a new dataframe...

```python--d7bdf00c-81a9-40cd-866d-d74364fa72fd
newdf = dfcwci.assign(ucname=dfcwci.last_name+":"+dfcwci.first_name).head(10)
newdf.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

name

ucname

0

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.0

2007-06-30

16

Agee, Steven

Agee:Steven

1

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

250.0

2007-05-16

16

Ahrens, Don

Ahrens:Don

2

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

50.0

2007-06-18

16

Ahrens, Don

Ahrens:Don

3

Ahrens

Don

NaN

4034 Rennellwood Way

NaN

Pleasanton

CA

94566

100.0

2007-06-21

16

Ahrens, Don

Ahrens:Don

4

Akin

Charles

NaN

10187 Sugar Creek Road

NaN

Bentonville

AR

72712

100.0

2007-06-16

16

Akin, Charles

Akin:Charles

Will the above command actually change `dfcwci`? `assign` creates a whole new dataframe. The dictionary style assigns in memory.

**What if we wanted to change an existing assignment?**

In other words, we are not creating a new column, but rather changing the values associated with a column, based on some criterion

```python--ec210141-d71b-486d-a0a0-d3ff963ea6c4
dfcwci[dfcwci.state=='VA']
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

name

0

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.00

2007-06-30

16

Agee, Steven

27

Buckheit

Bruce

NaN

8904 KAREN DR

NaN

FAIRFAX

VA

220312731

100.00

2007-09-19

20

Buckheit, Bruce

77

Ranganath

Anoop

NaN

2507 Willard Drive

NaN

Charlottesville

VA

22903

\-100.00

2008-04-21

32

Ranganath, Anoop

88

Perreault

Louise

NaN

503 Brockridge Hunt Drive

NaN

Hampton

VA

23666

\-34.08

2008-04-21

32

Perreault, Louise

145

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

NaN

FAIRFAX

VA

220308440

50.00

2007-09-30

35

ABDELLA, THOMAS

Lets get the `name` column we just created...

```python--c67cb06a-b09a-4308-9ec0-e4da68dba6a1
dfcwci.loc[dfcwci.state=='VA', 'name']
```

```output--c67cb06a-b09a-4308-9ec0-e4da68dba6a1
0           Agee, Steven
27       Buckheit, Bruce
77      Ranganath, Anoop
88     Perreault, Louise
145      ABDELLA, THOMAS
Name: name, dtype: object
```

Now we set the names from Virginia to be "junk":

```python--80a21f82-af8c-410a-a7e2-d1f3d7997bfa
dfcwci.loc[dfcwci.state=='VA', 'name']="junk"
```

```python--487ee419-3fc3-4b8f-a6f8-7f7d01003e0a
dfcwci.query("state=='VA'")['name']
```

```output--487ee419-3fc3-4b8f-a6f8-7f7d01003e0a
0      junk
27     junk
77     junk
88     junk
145    junk
Name: name, dtype: object
```

* * *

Let us see the entire process in SQL

```python--a2007b60-4881-4cbf-a8e1-75c3d3706cba
alt="ALTER TABLE contributors ADD COLUMN name;"
db.cursor().execute(alt)
db.commit()
```

```python--98923934-79f9-41b1-868f-cf46384043a3
make_query("PRAGMA table_info(contributors);")
```

```output--98923934-79f9-41b1-868f-cf46384043a3
[(0, 'id', 'INTEGER', 1, None, 1),
 (1, 'last_name', 'VARCHAR', 0, None, 0),
 (2, 'first_name', 'VARCHAR', 0, None, 0),
 (3, 'middle_name', 'VARCHAR', 0, None, 0),
 (4, 'street_1', 'VARCHAR', 0, None, 0),
 (5, 'street_2', 'VARCHAR', 0, None, 0),
 (6, 'city', 'VARCHAR', 0, None, 0),
 (7, 'state', 'VARCHAR', 0, None, 0),
 (8, 'zip', 'VARCHAR', 0, None, 0),
 (9, 'amount', 'INTEGER', 0, None, 0),
 (10, 'date', 'DATETIME', 0, None, 0),
 (11, 'candidate_id', 'INTEGER', 1, None, 0),
 (12, 'name', '', 0, None, 0)]
```

```python--f38ed5e0-798d-4118-a962-6f9460b8e847
out = make_query("SELECT id, last_name,first_name from contributors;")
out2 = [(e[1]+", "+e[2],e[0]) for e in out]
out2[:5]
```

```output--f38ed5e0-798d-4118-a962-6f9460b8e847
[('Agee, Steven', 1),
 ('Ahrens, Don', 2),
 ('Ahrens, Don', 3),
 ('Ahrens, Don', 4),
 ('Akin, Charles', 5)]
```

```python--66654328-3a74-4500-9362-1fdb43bc3386
alt2="UPDATE contributors SET name = ? WHERE id = ?;"
for ele in out2:
    db.cursor().execute(alt2, ele)
db.commit()
```

```python--775ded5f-8ca4-4f93-8691-e304f468f6d1
out=make_query("SELECT * from contributors;")
print(out[0])
make_frame(out,legend=contributor_cols+["name"]).head(10)
```

```output--775ded5f-8ca4-4f93-8691-e304f468f6d1
(1, 'Agee', 'Steven', None, '549 Laurel Branch Road', None, 'Floyd', 'VA', '24091', 500, '2007-06-30', 16, 'Agee, Steven')

```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

name

0

1

Agee

Steven

None

549 Laurel Branch Road

None

Floyd

VA

24091

500.0

2007-06-30

16

Agee, Steven

1

2

Ahrens

Don

None

4034 Rennellwood Way

None

Pleasanton

CA

94566

250.0

2007-05-16

16

Ahrens, Don

2

3

Ahrens

Don

None

4034 Rennellwood Way

None

Pleasanton

CA

94566

50.0

2007-06-18

16

Ahrens, Don

3

4

Ahrens

Don

None

4034 Rennellwood Way

None

Pleasanton

CA

94566

100.0

2007-06-21

16

Ahrens, Don

4

5

Akin

Charles

None

10187 Sugar Creek Road

None

Bentonville

AR

72712

100.0

2007-06-16

16

Akin, Charles

5

6

Akin

Mike

None

181 Baywood Lane

None

Monticello

AR

71655

1500.0

2007-05-18

16

Akin, Mike

6

7

Akin

Rebecca

None

181 Baywood Lane

None

Monticello

AR

71655

500.0

2007-05-18

16

Akin, Rebecca

7

8

Aldridge

Brittni

None

808 Capitol Square Place, SW

None

Washington

DC

20024

250.0

2007-06-06

16

Aldridge, Brittni

8

9

Allen

John D.

None

1052 Cannon Mill Drive

None

North Augusta

SC

29860

1000.0

2007-06-11

16

Allen, John D.

9

10

Allen

John D.

None

1052 Cannon Mill Drive

None

North Augusta

SC

29860

1300.0

2007-06-29

16

Allen, John D.

And lets now do an assignment to an existing column

```python--f9829c16-8865-4c15-8488-d1a1dbfe6306
upd="UPDATE contributors SET name = 'junk' WHERE state = 'VA';"
db.cursor().execute(upd)
db.commit()
```

```python--94673592-f3b6-4e38-bd58-faf84059e683
out=make_query("SELECT * from contributors where state='VA';")
make_frame(out,contributor_cols+["name"]).head(10)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

name

0

1

Agee

Steven

None

549 Laurel Branch Road

None

Floyd

VA

24091

500.00

2007-06-30

16

junk

1

28

Buckheit

Bruce

None

8904 KAREN DR

None

FAIRFAX

VA

220312731

100.00

2007-09-19

20

junk

2

78

Ranganath

Anoop

None

2507 Willard Drive

None

Charlottesville

VA

22903

\-100.00

2008-04-21

32

junk

3

89

Perreault

Louise

None

503 Brockridge Hunt Drive

None

Hampton

VA

23666

\-34.08

2008-04-21

32

junk

4

146

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

None

FAIRFAX

VA

220308440

50.00

2007-09-30

35

junk

Denormalization of Relationships: Two Table Grammar of Data
-----------------------------------------------------------

We will soon see that to feed data to models, we want to denormalize it. Pointers to other tables make logical sense for storage, but not when we want to feed data, both for performance and array shape reasons. This denormalization is achived by a technique and a verb: JOIN.

JOINs are Cartesian Products followed by filterings. They come in different varieties, and all pay attention to the "left" element in the join. The standard Pandas merge is an inner join, and often you will see it being done with 2 dataframes on a commonly named column.

Here the `candidate_id` column in the contributors table is equivalent to the `id` in the candidate table, so we need to be explicit:

```python--3cfe1ce4-27d9-4c9c-b578-a7f2ac4374ba
dfcwci.shape, dfcand.shape
```

```output--3cfe1ce4-27d9-4c9c-b578-a7f2ac4374ba
((172, 11), (17, 5))
```

```python--9f147c12-b68d-4230-af5f-4bdc627546fd
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id")
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name\_x

first\_name\_x

middle\_name\_x

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

id

first\_name\_y

last\_name\_y

middle\_name\_y

party

0

Agee

Steven

NaN

549 Laurel Branch Road

NaN

Floyd

VA

24091

500.0

2007-06-30

16

16

Mike

Huckabee

NaN

R

1

Akin

Charles

NaN

10187 Sugar Creek Road

NaN

Bentonville

AR

72712

100.0

2007-06-16

16

16

Mike

Huckabee

NaN

R

2

Akin

Mike

NaN

181 Baywood Lane

NaN

Monticello

AR

71655

1500.0

2007-05-18

16

16

Mike

Huckabee

NaN

R

3

Akin

Rebecca

NaN

181 Baywood Lane

NaN

Monticello

AR

71655

500.0

2007-05-18

16

16

Mike

Huckabee

NaN

R

4

Aldridge

Brittni

NaN

808 Capitol Square Place, SW

NaN

Washington

DC

20024

250.0

2007-06-06

16

16

Mike

Huckabee

NaN

R

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

167

ABESHAUS

MERRILL

M.

1801 N. HEREFORD DRIVE

NaN

FLAGSTAFF

AZ

860011121

120.0

2008-01-16

37

37

John

McCain

NaN

R

168

ABRAHAM

GEORGE

NaN

P.O. BOX 1504

NaN

LAKE CHARLES

LA

706021504

800.0

2008-01-17

37

37

John

McCain

NaN

R

169

ABRAHAMSON

PETER

J.

1030 W. ROSCOE STREET

NaN

CHICAGO

IL

606572207

50.0

2008-01-25

37

37

John

McCain

NaN

R

170

ABRAHAM

SALEM

A.

P.O. BOX 7

NaN

CANADIAN

TX

790140007

1000.0

2008-01-17

37

37

John

McCain

NaN

R

171

ABRAHAM

SALEM

A.

P.O. BOX 7

NaN

CANADIAN

TX

790140007

1300.0

2008-01-30

37

37

John

McCain

NaN

R

172 rows × 16 columns

This command repeats information about the candidate on each contributor to that candidate. Now you have a flat table.

If you do it in the opposite direction, the result is symmetric, since the `id` is guaranteed to match the `candidate_id` in out case

```python--846d6b3d-8523-4d12-9084-49978f438d71
dfcand.merge(dfcwci, right_on="candidate_id", left_on="id")
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

first\_name\_x

last\_name\_x

middle\_name\_x

party

last\_name\_y

first\_name\_y

middle\_name\_y

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

34

Hillary

Clinton

R.

D

Aaronson

Rebecca

NaN

2000 Village Green Dr Apt 12

NaN

Mill Creek

WA

980125787

100.0

2008-02-08

34

1

34

Hillary

Clinton

R.

D

Aarons

Elaine

NaN

481 Buck Island Rd Apt 17A

APT 17A

West Yarmouth

MA

26733300

25.0

2008-02-26

34

2

34

Hillary

Clinton

R.

D

Aarons

Elaine

NaN

481 Buck Island Rd Apt 17A

APT 17A

West Yarmouth

MA

26733300

70.0

2008-02-25

34

3

34

Hillary

Clinton

R.

D

Aarons

Elaine

NaN

481 Buck Island Rd Apt 17A

APT 17A

West Yarmouth

MA

26733300

100.0

2008-02-08

34

4

34

Hillary

Clinton

R.

D

Aaron

Shirley

NaN

101 Cherry Ave

NaN

Havana

FL

323331311

50.0

2008-02-29

34

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

167

35

Mitt

Romney

NaN

R

ABDELLA

THOMAS

M.

4231 MONUMENT WALL WAY #340

NaN

FAIRFAX

VA

220308440

50.0

2007-09-30

35

168

35

Mitt

Romney

NaN

R

ABBOTT

WELDON

S.

777 EAST SOUTH TEMPLE 4E

NaN

SALT LAKE CITY

UT

841021269

100.0

2007-09-29

35

169

35

Mitt

Romney

NaN

R

ABBOTT

WELDON

S.

777 EAST SOUTH TEMPLE 4E

NaN

SALT LAKE CITY

UT

841021269

50.0

2007-08-09

35

170

35

Mitt

Romney

NaN

R

ABBOTT

GERALD

F.

389 BENEFIT STREET

NaN

PROVIDENCE

RI

29032946

100.0

2007-09-15

35

171

35

Mitt

Romney

NaN

R

ABBOTT

GERALD

F.

389 BENEFIT STREET

NaN

PROVIDENCE

RI

29032946

100.0

2007-08-15

35

172 rows × 16 columns

### Explicit INNER JOIN

The notion above (and the default) in Pandas is an inner join. Think of a cartesian product of the left table by the right one, 16 choices, followed by a drop of all the unmatched rows. Thus it gives us rows that are in both tables:

![](images/innerjoin.png)

(The set images are from http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/ which also has a very nice description of these joins).

![inner join](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_inner.png)

(from http://pandas.pydata.org/pandas-docs/stable/merging.html)

```python--9e7072fb-4ae7-42fe-bc94-8a3d40fbbc5d
cols_wanted=['last_name_x', 'first_name_x', 'candidate_id', 'id', 'last_name_y']
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id")[cols_wanted]
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name\_x

first\_name\_x

candidate\_id

id

last\_name\_y

0

Agee

Steven

16

16

Huckabee

1

Akin

Charles

16

16

Huckabee

2

Akin

Mike

16

16

Huckabee

3

Akin

Rebecca

16

16

Huckabee

4

Aldridge

Brittni

16

16

Huckabee

...

...

...

...

...

...

167

ABESHAUS

MERRILL

37

37

McCain

168

ABRAHAM

GEORGE

37

37

McCain

169

ABRAHAMSON

PETER

37

37

McCain

170

ABRAHAM

SALEM

37

37

McCain

171

ABRAHAM

SALEM

37

37

McCain

172 rows × 5 columns

```python--337c7317-4895-4a3d-ac5d-caef05aed780
explicitjoinsel="""
SELECT 
    contributors.last_name, contributors.first_name, candidates.last_name 
FROM 
    contributors JOIN candidates 
ON contributors.candidate_id = candidates.id;
"""
out=make_query(explicitjoinsel)
make_frame(out, legend=["contributors.last_name", 
            "contributors.first_name",  "candidates.last_name"]).head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

contributors.last\_name

contributors.first\_name

candidates.last\_name

0

Agee

Steven

Huckabee

1

Akin

Charles

Huckabee

2

Akin

Mike

Huckabee

3

Akin

Rebecca

Huckabee

4

Aldridge

Brittni

Huckabee

Here is an usage example:

```python--3ee7438e-75b8-44aa-8877-d386c26b750a
explicitjoinsel="""
SELECT 
    COUNT(contributors.id), contributors.first_name, candidates.last_name 
FROM 
    contributors JOIN candidates 
ON contributors.candidate_id = candidates.id

GROUP BY candidates.last_name;
"""
out=make_query(explicitjoinsel)
make_frame(out, legend=["count(contributors.id)", 
            "contributors.first_name",  "candidates.last_name"])
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

count(contributors.id)

contributors.first\_name

candidates.last\_name

0

25

Rebecca

Clinton

1

25

HERBERT

Giuliani

2

22

Steven

Huckabee

3

25

ZAINUL

McCain

4

25

Steve

Obama

5

25

Bryan

Paul

6

25

TRAVIS

Romney

Some Other Useful patterns
--------------------------

### Simple subselect

We do one "select" and then use that in another one...

```python--200f6cdc-d0f5-4f65-be97-288205623b48
dfcand.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

first\_name

last\_name

middle\_name

party

0

33

Joseph

Biden

NaN

D

1

36

Samuel

Brownback

NaN

R

2

34

Hillary

Clinton

R.

D

3

39

Christopher

Dodd

J.

D

4

26

John

Edwards

NaN

D

```python--4d784cfb-cc37-4d49-af88-49324b9ce792
obamaid=dfcand.query("last_name=='Obama'")['id'].values[0]
```

```python--16519c3f-87d4-4909-918d-d1af8febe626
obamacontrib=dfcwci.query("candidate_id==%i" % obamaid)
obamacontrib.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

25

Buckler

Steve

NaN

24351 Armada Dr

NaN

Dana Point

CA

926291306

50.0

2007-07-30

20

26

Buckler

Steve

NaN

24351 Armada Dr

NaN

Dana Point

CA

926291306

25.0

2007-08-16

20

27

Buckheit

Bruce

NaN

8904 KAREN DR

NaN

FAIRFAX

VA

220312731

100.0

2007-09-19

20

28

Buckel

Linda

NaN

PO Box 683130

NaN

Park City

UT

840683130

2300.0

2007-08-14

20

29

Buckel

Linda

NaN

PO Box 683130

NaN

Park City

UT

840683130

\-2300.0

2007-08-14

20

The SQL syntax makes this look like a russian doll scenario where there is a select inside a select..

```python--94a4f094-cad1-4b31-ad9f-23ada39e74bd
russiandollsel="""
SELECT * FROM contributors WHERE 
    candidate_id = (SELECT id from candidates WHERE last_name = 'Obama');
"""
out=make_query(russiandollsel)
make_frame(out, legend=contributor_cols)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

last\_name

first\_name

middle\_name

street\_1

street\_2

city

state

zip

amount

date

candidate\_id

0

26

Buckler

Steve

None

24351 Armada Dr

None

Dana Point

CA

926291306

50.00

2007-07-30

20

1

27

Buckler

Steve

None

24351 Armada Dr

None

Dana Point

CA

926291306

25.00

2007-08-16

20

2

28

Buckheit

Bruce

None

8904 KAREN DR

None

FAIRFAX

VA

220312731

100.00

2007-09-19

20

3

29

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

2300.00

2007-08-14

20

4

30

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

\-2300.00

2007-08-14

20

5

31

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

4600.00

2007-08-14

20

6

32

Buck

Thomas

None

4206 Terrace Street

None

Kansas City

MO

64111

100.00

2007-09-25

20

7

33

Buck

Jay

K.

1855 Old Willow Rd Unit 322

None

Northfield

IL

600932918

200.00

2007-09-12

20

8

34

Buck

Blaine

M

45 Eaton Ave

None

Camden

ME

48431752

2300.00

2007-09-30

20

9

35

Buck

Barbara

None

1780 NE 138th St

None

North Miami

FL

331811316

50.00

2007-09-13

20

10

36

Buck

Barbara

None

1780 NE 138th St

None

North Miami

FL

331811316

50.00

2007-07-19

20

11

37

Buchman

Mark M

None

2530 Lawton Ave

None

San Luis Obispo

CA

934015622

460.80

2007-07-18

20

12

38

Bucher

Ida

M

1400 Warnall Ave

None

Los Angeles

CA

900245333

100.00

2007-07-10

20

13

39

Buchanek

Elizabeth

None

7917 Kentbury Dr

None

Bethesda

MD

208144615

50.00

2007-09-30

20

14

40

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

500.00

2007-09-24

20

15

41

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

\-500.00

2007-09-24

20

16

42

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

500.00

2007-09-24

20

17

43

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

700.00

2007-08-28

20

18

44

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

\-700.00

2007-08-28

20

19

45

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

1000.00

2007-08-28

20

20

46

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

1300.00

2007-08-09

20

21

47

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

200.00

2007-08-14

20

22

48

Buchanan

John

None

2025 NW 29th Rd

None

Boca Raton

FL

334316303

500.00

2007-07-25

20

23

49

Buchanan

John

None

4635 49th St NW

None

Washington

DC

200164320

200.09

2007-09-23

20

24

50

Harrison

Ryan

None

2247 3rd St

None

La Verne

CA

917504918

25.00

2007-07-26

20

### Implicit join

This is a SQL only construct which is nevertheless an often seen pattern where we dont do an explicit inner join...

```python--a97029c8-57f6-4ac1-9075-7a05c17f94d8
implicitjoinsel="""
SELECT 
    contributors.last_name, contributors.first_name, contributors.amount, candidates.last_name 
FROM 
    contributors, candidates 
WHERE contributors.candidate_id = candidates.id
AND candidates.last_name = 'Obama';
"""
out=make_query(implicitjoinsel)
make_frame(out, legend=["contributors.last_name", 
            "contributors.first_name", "contributors.amount", "candidates.last_name"]).head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

contributors.last\_name

contributors.first\_name

contributors.amount

candidates.last\_name

0

Buckler

Steve

50.0

Obama

1

Buckler

Steve

25.0

Obama

2

Buckheit

Bruce

100.0

Obama

3

Buckel

Linda

2300.0

Obama

4

Buckel

Linda

\-2300.0

Obama

```python--f1b52176-e51a-4b8d-beb9-b82ded4e1707
db.close()
```
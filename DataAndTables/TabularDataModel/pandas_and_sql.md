Pandas, SQL, and the Grammar of Data
====================================

We'd like a data structure that can represent the columns in the data above by their name. In particular, we want a structure that can easily store variables of different types, that stores column names, and that we can reference by column name as well as by indexed position. And it would be nice this data structure came with built-in functions that we can use to manipulate it.

Pandas is a package/library that does all of this! The library is built on top of numpy. There are two basic pandas objects, _series_ and _dataframes_, which can be thought of as enhanced versions of 1D and 2D numpy arrays, respectively. Indeed Pandas attempts to keep all the efficiencies that `numpy` gives us.

For reference, here is a useful pandas [cheat sheet](https://drive.google.com/folderview?id=0ByIrJAE4KMTtaGhRcXkxNHhmY2M&usp=sharing) and the pandas [documentation](https://pandas.pydata.org/pandas-docs/stable/).

```python--0ac8ebd7-dcc4-4ebf-9d0a-b7d3b7edc731
import pandas as pd
```

```python--0f4328e2-1bfd-4af9-a87d-eef929aca175
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

### Building a dataframe

The easiest way to build a dataframe is simply to read in a CSV file.

This example is adapted from: https://github.com/tthibo/SQL-Tutorial

Use Pandas to read in the data

```python--98d694d3-171f-45bf-a47f-2f6066aa1b46
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

```python--940d1173-6493-4125-892e-289603f035f4
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

```python--f2b5b3b9-d68f-456f-9ce3-6f0d124a2c02
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

```python--43813b90-14f5-46a3-ae47-9db8e48ce7fa
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

We use sqlite here (and recommend Postgres for production purposes). Sqlite is a on-file database, as opposed to other common databases such as Oracle and Psogres, which run as different processes on your system. Sqlite is great for on-disk large databases which wont fit into memory.

Its also built into Python, but to use the [command line tool](https://www.sqlite.org/cli.html), I recommend you install it: https://www.sqlite.org/download.html. I also recommend you download and install the sqlite browser: http://sqlitebrowser.org .

Python implements a standard database API over all databases. Its called [DBAPI2](http://cewing.github.io/training.codefellows/lectures/day21/intro_to_dbapi2.html). It works across many SQL databases.

There is an even higher level API available, called [SQLAlchemy](http://www.sqlalchemy.org). While we wont use it here, I thoroughly recommend it. Many things in Pandas use it to interface with databases. Here we'll get away with things by using SQLITE.

We'll write some functions to connect to Sqlite.

(1) Connect and get a DBAPI2 connection.

```python--3f3e546a-e35e-46da-b7ff-a3910d46e6d8
from sqlite3 import dbapi2 as sq3
from pathlib import Path
PATHSTART="."
def get_db(dbfile):
    sqlite_db = sq3.connect(Path(PATHSTART) / dbfile)
    return sqlite_db
```

(2) Set up the database with tables. Drop tables if they exist and create them.

```python--5b2965d8-97bf-49b1-9169-72898e91de03
def init_db(dbfile, schema):
    """Creates the database tables."""
    db = get_db(dbfile) 
    db.cursor().executescript(schema)
    db.commit()
    return db
```

Initializing the database:

```python--c708920d-fb6a-4350-9556-9e52161382ed
db=init_db("/tmp/cancont.db", ourschema)
```

### Populating with Pandas!!

```python--df07e6c2-b261-4c32-963b-0f7d5c80687b
dfcand.to_sql("candidates", db, if_exists="append", index=False)
```

```python--7621671e-c1de-4ca3-bf0e-8bf1699a397c
dfcwci.to_sql("contributors", db, if_exists="append", index=False)
```

Now we can do queries in the lingua franca of databases: SQL

```python--7ea087d1-b47c-45d5-911c-c7f3e8927a1b
sel="""
SELECT * FROM candidates;
"""
c=db.cursor().execute(sel)
```

```python--30a655f0-eb25-45c6-836e-7823ed1a9662
c.fetchall()
```

```output--30a655f0-eb25-45c6-836e-7823ed1a9662
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

```python--c8a2c058-37cc-4179-84cd-a4d0e5d90404
def make_query(sel):
    c=db.cursor().execute(sel)
    return c.fetchall()
```

```python--1634b170-08bf-4a8c-bc06-0a6acc2c0152
make_query("SELECT * FROM candidates;")
```

```output--1634b170-08bf-4a8c-bc06-0a6acc2c0152
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

```python--0db76293-54f9-48f8-a8da-28c61a0bcad2
make_query("PRAGMA table_info(candidates);")
```

```output--0db76293-54f9-48f8-a8da-28c61a0bcad2
[(0, 'id', 'INTEGER', 1, None, 1),
 (1, 'first_name', 'VARCHAR', 0, None, 0),
 (2, 'last_name', 'VARCHAR', 0, None, 0),
 (3, 'middle_name', 'VARCHAR', 0, None, 0),
 (4, 'party', 'VARCHAR', 1, None, 0)]
```

```python--3f9ed0a1-9e05-4c30-942d-241b81e9ae98
make_query("PRAGMA table_info(contributors);")
```

```output--3f9ed0a1-9e05-4c30-942d-241b81e9ae98
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

```python--37c166e2-e433-4c03-8632-870606568b12
candidate_cols = [e[1] for e in make_query("PRAGMA table_info(candidates);")]
candidate_cols
```

```output--37c166e2-e433-4c03-8632-870606568b12
['id', 'first_name', 'last_name', 'middle_name', 'party']
```

```python--316ba878-1d44-4d00-a53a-3eb1235bc381
contributor_cols = [e[1] for e in make_query("PRAGMA table_info(contributors);")]
contributor_cols
```

```output--316ba878-1d44-4d00-a53a-3eb1235bc381
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

```python--61456fa1-6a5d-4a88-a526-5482750dc4bd
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

```python--b47b84b1-3ca2-445e-9f99-71d48b411695
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

```python--51a96771-ca9d-486b-bb44-a7109b73a1f6
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

```python--c77d5bdf-2490-453a-93a7-bf5a683bff40
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

```python--78c98abe-5f33-4e62-a7a4-f42ce32fc446
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

```python--cdae108b-f7e9-4bc1-bc61-a84f32dcaff3
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

Looking for data problems with nulls:

```python--d7124ecf-6bcc-41b2-bdde-e4b3a8c03d78
dfcwci[dfcwci.state.isnull()]
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

125

BOURNE

TRAVIS

NaN

LAGE KAART 77

NaN

BRASSCHATT

NaN

2930

\-500.0

2008-11-20

35

```python--6fa833bf-71e3-4757-b452-150e369fa74a
out=make_query("SELECT * FROM contributors WHERE state IS NULL;")
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

126

BOURNE

TRAVIS

None

LAGE KAART 77

None

BRASSCHATT

None

2930

\-500

2008-11-20

35

Or the other way....

```python--1e8008c0-fa2f-472e-88af-8e9413ed6f94
dfcwci[dfcwci.state.notnull()] # or dfcwci[~dfcwci.state.isnull()]
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

170

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

171

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

172

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

173

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

174

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

174 rows × 11 columns

```python--ff7c31b2-3cf3-4af6-ba68-fe2ae57f2299
out=make_query("SELECT * FROM contributors WHERE state IS NOT NULL;")
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

169

171

ABESHAUS

MERRILL

M.

1801 N. HEREFORD DRIVE

None

FLAGSTAFF

AZ

860011121

120.0

2008-01-16

37

170

172

ABRAHAM

GEORGE

None

P.O. BOX 1504

None

LAKE CHARLES

LA

706021504

800.0

2008-01-17

37

171

173

ABRAHAMSON

PETER

J.

1030 W. ROSCOE STREET

None

CHICAGO

IL

606572207

50.0

2008-01-25

37

172

174

ABRAHAM

SALEM

A.

P.O. BOX 7

None

CANADIAN

TX

790140007

1000.0

2008-01-17

37

173

175

ABRAHAM

SALEM

A.

P.O. BOX 7

None

CANADIAN

TX

790140007

1300.0

2008-01-30

37

174 rows × 12 columns

Queries that look if things are in a list...useful for categorical variables or discrete valued numerical variables...

```python--75e1d3df-7fdb-456b-9445-b988d83783a5
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

```python--45628d25-1af0-4010-9804-e40fd94befea
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

### SORT

After possibly making a query, we want to sort our results...

```python--1bf85ff4-8288-470d-8a94-cfa642f0f6e6
dfcwci.sort_values("amount").head(10)
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

90

Kazor

Christopher

M

707 Spindletree ave

NaN

Naperville

IL

60565

\-2592.0

2008-04-21

32

72

BRUNO

JOHN

NaN

10136 WINDERMERE CHASE BLVD.

NaN

GOTHA

FL

347344707

\-2300.0

2008-03-06

22

64

BURKE

DONALD

J.

12 LOMPOC

NaN

RANCHO SANTA MARGA

CA

926881817

\-2300.0

2008-03-11

22

73

BRUNO

IRENE

NaN

10136 WINDERMERE CHASE BLVD.

NaN

GOTHA

FL

347344707

\-2300.0

2008-03-06

22

74

BROWN

TIMOTHY

J.

26826 MARLOWE COURT

NaN

STEVENSON RANCH

CA

913811020

\-2300.0

2008-03-06

22

58

BURTON

GLENN

M.

4404 CHARLESTON COURT

NaN

TAMPA

FL

336092620

\-2300.0

2008-03-05

22

57

BURTON

STEVEN

G.

9938 DEER CREEK DRIVE

NaN

TAMPA

FL

33647

\-2300.0

2008-03-05

22

84

Uihlein

Richard

NaN

1396 N Waukegan Rd

NaN

Lake Forest

IL

600451147

\-2300.0

2008-04-21

32

56

BURTON

SUSAN

NaN

9338 DEER CREEK DRIVE

NaN

TAMPA

FL

336472286

\-2300.0

2008-03-05

22

55

BUSH

ERIC

NaN

P.O. BOX 61046

NaN

DENVER

CO

802061046

\-2300.0

2008-03-06

22

```python--bcae5bfb-d7d9-4d02-a35b-0b00efd966af
dfcwci.sort_values("amount", ascending=False).head(10)
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

30

Buckel

Linda

NaN

PO Box 683130

NaN

Park City

UT

840683130

4600.0

2007-08-14

20

159

ABATE

MARIA

ELENA

1291 NIGHTINGALE AVENUE

NaN

MIAMI SPRINGS

FL

331663832

2600.0

2008-01-25

37

15

Anthony

John

NaN

211 Long Island Drive

NaN

Hot Springs

AR

71913

2300.0

2007-06-12

16

33

Buck

Blaine

M

45 Eaton Ave

NaN

Camden

ME

48431752

2300.0

2007-09-30

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

21

Baker

David

NaN

2550 Adamsbrooke Drive

NaN

Conway

AR

72034

2300.0

2007-04-11

16

13

Altes

R.D.

NaN

8600 Moody Road

NaN

Fort Smith

AR

72903

2300.0

2007-06-21

16

135

ABRAMOWITZ

NIRA

NaN

411 HARBOR ROAD

NaN

SOUTHPORT

CT

68901376

2300.0

2007-09-14

35

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

174

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

```python--aa78a78f-fe4c-44dd-a2b5-3a3d5e9430a3
out=make_query("SELECT * FROM contributors ORDER BY amount;")
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

91

Kazor

Christopher

M

707 Spindletree ave

None

Naperville

IL

60565

\-2592.0

2008-04-21

32

1

30

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

\-2300.0

2007-08-14

20

2

52

BYINGTON

MARGARET

E.

2633 MIDDLEBORO LANE N.E.

None

GRAND RAPIDS

MI

495061254

\-2300.0

2008-03-03

22

3

53

BYERS

BOB

A.

13170 TELFAIR AVENUE

None

SYLMAR

CA

913423573

\-2300.0

2008-03-07

22

4

55

BUSH

KRYSTIE

None

P.O. BOX 61046

None

DENVER

CO

802061046

\-2300.0

2008-03-06

22

5

56

BUSH

ERIC

None

P.O. BOX 61046

None

DENVER

CO

802061046

\-2300.0

2008-03-06

22

6

57

BURTON

SUSAN

None

9338 DEER CREEK DRIVE

None

TAMPA

FL

336472286

\-2300.0

2008-03-05

22

7

58

BURTON

STEVEN

G.

9938 DEER CREEK DRIVE

None

TAMPA

FL

33647

\-2300.0

2008-03-05

22

8

59

BURTON

GLENN

M.

4404 CHARLESTON COURT

None

TAMPA

FL

336092620

\-2300.0

2008-03-05

22

9

65

BURKE

DONALD

J.

12 LOMPOC

None

RANCHO SANTA MARGA

CA

926881817

\-2300.0

2008-03-11

22

```python--a29dafa2-6bc8-4395-a3aa-91690d9b10b5
out=make_query("SELECT * FROM contributors ORDER BY amount DESC;")
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

31

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

4600.0

2007-08-14

20

1

160

ABATE

MARIA

ELENA

1291 NIGHTINGALE AVENUE

None

MIAMI SPRINGS

FL

331663832

2600.0

2008-01-25

37

2

14

Altes

R.D.

None

8600 Moody Road

None

Fort Smith

AR

72903

2300.0

2007-06-21

16

3

16

Anthony

John

None

211 Long Island Drive

None

Hot Springs

AR

71913

2300.0

2007-06-12

16

4

22

Baker

David

None

2550 Adamsbrooke Drive

None

Conway

AR

72034

2300.0

2007-04-11

16

5

29

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

2300.0

2007-08-14

20

6

34

Buck

Blaine

M

45 Eaton Ave

None

Camden

ME

48431752

2300.0

2007-09-30

20

7

136

ABRAMOWITZ

NIRA

None

411 HARBOR ROAD

None

SOUTHPORT

CT

68901376

2300.0

2007-09-14

35

8

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

### SELECT-COLUMNS

Sometimes we only want to get a few columns, not the entire table

```python--ddfc2dfd-6306-4d15-9cee-f58ddb5127bd
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

```python--d0d172dd-d39f-437f-be90-b17f91c06678
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

### SELECT-DISTINCT

Once we have chosen certain columns we might want to drop rows which have duplicate values for some of these columns..

Selecting a distinct set is useful for cleaning. Here, we might wish to focus on contributors rather than contributions and see how many distinct contributors we have. Of-course we might be wrong, some people have identical names.

```python--65371285-9ee5-4676-88fc-c448f2737c1a
dfcwci[['last_name','first_name']].count()
```

```output--65371285-9ee5-4676-88fc-c448f2737c1a
last_name     175
first_name    175
dtype: int64
```

```python--d695d82c-1313-4e62-9298-09f8e43cd3e3
dfcwci[['last_name','first_name']].drop_duplicates().count()
```

```output--d695d82c-1313-4e62-9298-09f8e43cd3e3
last_name     126
first_name    126
dtype: int64
```

```python--6a531418-a7c9-40bd-95a8-dac3f6e7f8f3
out=make_query("SELECT DISTINCT last_name, first_name FROM contributors;")
make_frame(out,['last_name', 'first_name'])
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

0

Agee

Steven

1

Ahrens

Don

2

Akin

Charles

3

Akin

Mike

4

Akin

Rebecca

...

...

...

121

ABERCROMBIE

DENIS

122

ABESHAUS

MERRILL

123

ABRAHAM

GEORGE

124

ABRAHAMSON

PETER

125

ABRAHAM

SALEM

126 rows × 2 columns

Creation and Alteration
-----------------------

So far, when we created the database, we did it using Pandas. Clearly, one ought to be able to populate a SQL database using SQL. We now turn to this use case, as well as the alteration of databases.

### Populate with SQL INSERT

Before we populate a the `candidates` table, lets delete all data from it...

```python--154a8c1d-11a7-41e3-9e8a-c28edb8fc0d7
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

```python--0bbdc085-df56-4119-973e-f7bda0b2a34f
ins="""
INSERT INTO candidates (id, first_name, last_name, middle_name, party) \
    VALUES (?,?,?,?,?);
"""
```

Now we read the file line by line, not including the header line and slurp in the data. Notice that we only finish the transaction after we have slurped in all the lines. So its all lines or none. When we execute the cursor, the question marks are used a templates with a tuple provided in..

```python--171971fa-da3e-4d32-bb1d-b5cd8c44eb6f
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

```output--171971fa-da3e-4d32-bb1d-b5cd8c44eb6f
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

```python--10b7bb26-92a7-46d2-87f1-59cb514e3b51
make_query("SELECT * FROM candidates;")
```

```output--10b7bb26-92a7-46d2-87f1-59cb514e3b51
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

```python--60c46d42-665b-4b3e-98a3-b771d8e780b4
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

```python--d312249f-24c0-473b-a1c5-619517f3ac1e
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

```python--d44a223d-92b2-45cf-aad4-cde0c78e506e
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

```python--507dc1b4-e5a8-403c-b802-30074fd244a9
dfcwci.loc[dfcwci.state=='VA', 'name']
```

```output--507dc1b4-e5a8-403c-b802-30074fd244a9
0           Agee, Steven
27       Buckheit, Bruce
77      Ranganath, Anoop
88     Perreault, Louise
145      ABDELLA, THOMAS
Name: name, dtype: object
```

Now we set the names from Virginia to be "junk":

```python--2301e557-d833-41af-b42d-37df8f613400
dfcwci.loc[dfcwci.state=='VA', 'name']="junk"
```

```python--5a894cfa-ef8b-4971-9b8a-99a7f548d373
dfcwci.query("state=='VA'")['name']
```

```output--5a894cfa-ef8b-4971-9b8a-99a7f548d373
0      junk
27     junk
77     junk
88     junk
145    junk
Name: name, dtype: object
```

* * *

Let us see the entire process in SQL

```python--df2f5709-6342-43ea-b441-e55725eee747
alt="ALTER TABLE contributors ADD COLUMN name;"
db.cursor().execute(alt)
db.commit()
```

```python--105d53d1-c867-490e-80d7-a1cb28c913a9
make_query("PRAGMA table_info(contributors);")
```

```output--105d53d1-c867-490e-80d7-a1cb28c913a9
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

```python--3a4550fd-db9a-4ccd-8bcc-5f9a88d21430
out = make_query("SELECT id, last_name,first_name from contributors;")
out2 = [(e[1]+", "+e[2],e[0]) for e in out]
out2[:5]
```

```output--3a4550fd-db9a-4ccd-8bcc-5f9a88d21430
[('Agee, Steven', 1),
 ('Ahrens, Don', 2),
 ('Ahrens, Don', 3),
 ('Ahrens, Don', 4),
 ('Akin, Charles', 5)]
```

```python--76778653-c297-4a15-918b-abd14053c5f8
alt2="UPDATE contributors SET name = ? WHERE id = ?;"
for ele in out2:
    db.cursor().execute(alt2, ele)
db.commit()
```

```python--ccc6b41b-2162-4edb-a97b-d1d4c548f55d
out=make_query("SELECT * from contributors;")
print(out[0])
make_frame(out,legend=contributor_cols+["name"]).head(10)
```

```output--ccc6b41b-2162-4edb-a97b-d1d4c548f55d
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

```python--aefd39d2-e05e-45a1-ac50-a3826f97a577
upd="UPDATE contributors SET name = 'junk' WHERE state = 'VA';"
db.cursor().execute(upd)
db.commit()
```

```python--3892d624-3491-4a95-ba01-ee2cbca805ad
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

### No DROP COLUMN in SQLITE

Its available in other databases. Here you must just re-create your database, or know about this gotcha from the start. (reasons here: https://www.quora.com/Why-cant-SQLite-drop-columns)

```python--2e421836-a5fb-4e7e-a55c-6eac36d775c4
alt="ALTER TABLE contributors DROP COLUMN name;"
db.cursor().execute(alt)
db.commit()
```

```output--2e421836-a5fb-4e7e-a55c-6eac36d775c4
---------------------------------------------------------------------------
```

```output--2e421836-a5fb-4e7e-a55c-6eac36d775c4
OperationalError                          Traceback (most recent call last)
```

```output--2e421836-a5fb-4e7e-a55c-6eac36d775c4
 in 
      1 alt="ALTER TABLE contributors DROP COLUMN name;"
----> 2 db.cursor().execute(alt)
      3 db.commit()

```

```output--2e421836-a5fb-4e7e-a55c-6eac36d775c4
OperationalError: near "DROP": syntax error
```

Its much simpler in Pandas, of-course

```python--0a502981-b540-4c25-b42e-e68349aed787
del dfcwci['name']
```

### AGGREGATE

```python--149109ac-c885-4db5-8ac1-09d6ae2f4db2
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

```python--ddba2bbe-5449-4fa4-811f-ba61e8573ffa
dfcwci.amount.max()
```

```output--ddba2bbe-5449-4fa4-811f-ba61e8573ffa
4600.0
```

```python--34eb4cc8-7c46-4927-a7b3-aa616b5a1ac4
dfcwci[dfcwci.amount==dfcwci.amount.max()]
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

30

Buckel

Linda

NaN

PO Box 683130

NaN

Park City

UT

840683130

4600.0

2007-08-14

20

SQL is actually simpler

```python--745fd1b8-6dc8-44d9-a96f-0ea411c343e0
out=make_query("SELECT MAX(amount) FROM contributors;")
out
```

```output--745fd1b8-6dc8-44d9-a96f-0ea411c343e0
[(4600,)]
```

```python--eaad9536-e094-41bb-a6c0-d5394de74c7b
out=make_query("SELECT *, MAX(amount) AS maxamt FROM contributors;")
print(out)
make_frame(out, legend=contributor_cols+['name','maxamt'])
```

```output--eaad9536-e094-41bb-a6c0-d5394de74c7b
[(31, 'Buckel', 'Linda', None, 'PO Box 683130', None, 'Park City', 'UT', '840683130', 4600, '2007-08-14', 20, 'Buckel, Linda', 4600)]

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

maxamt

0

31

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

4600

2007-08-14

20

Buckel, Linda

4600

```python--c12317fd-41bc-4449-991e-38907eea3a4a
out=make_query("SELECT COUNT(amount) AS AMOUNTCOUNT FROM contributors;")
print(out)
```

```output--c12317fd-41bc-4449-991e-38907eea3a4a
[(175,)]

```

```python--f8814d97-05b2-49cd-8213-0478e9d7fa55
dfcwci[dfcwci.amount > dfcwci.amount.max() - 2300]
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

30

Buckel

Linda

NaN

PO Box 683130

NaN

Park City

UT

840683130

4600.0

2007-08-14

20

159

ABATE

MARIA

ELENA

1291 NIGHTINGALE AVENUE

NaN

MIAMI SPRINGS

FL

331663832

2600.0

2008-01-25

37

```python--68b1c564-b4ae-4349-8440-9b6ec90c76cc
out=make_query("SELECT * FROM contributors WHERE amount > (select (MAX(amount) - 2300) FROM contributors);")
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

31

Buckel

Linda

None

PO Box 683130

None

Park City

UT

840683130

4600

2007-08-14

20

1

160

ABATE

MARIA

ELENA

1291 NIGHTINGALE AVENUE

None

MIAMI SPRINGS

FL

331663832

2600

2008-01-25

37

Aso `MIN`, `SUM`, `AVG`.

### GROUP-AGG

Being able to group data by the value of any column is critical functionality. This is how you understand your sampling, and the distributions of various quantities in your data.

```python--8425a13d-cc09-40d0-9fb2-88d5c16c6a4b
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

```python--4e0ada54-6f0d-4fdd-9acc-6ecd52242054
dfcwci.groupby("state")['amount'].mean()
```

```output--4e0ada54-6f0d-4fdd-9acc-6ecd52242054
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

```python--d19f9e6b-fe4a-4dfa-b078-a7fcb9f92c61
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

### DELETE

```python--633aef40-642e-4d32-92e7-1e8697f587c0
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

In-place drops

```python--5506e598-fae2-41ce-8bbd-2f3cedd75df3
df2=dfcwci.copy()
df2.set_index('last_name', inplace=True)
df2.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

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

last\_name

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

```python--325a0344-a2a3-429a-8cd2-b1c8e5c7e166
df2.drop(['Ahrens'], inplace=True)
df2.head()
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

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

last\_name

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

```python--5b7692a9-a6ac-4472-b332-3826e9632e1b
df2.reset_index(inplace=True)
df2.head()
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

The recommended way to do it is to create a new dataframe. This might be impractical if data is very large.

```python--06fc56de-c2dd-44a3-a999-ee028b32f324
dfcwci=dfcwci[dfcwci.last_name!='Ahrens']
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

10

Allison

John W.

NaN

P.O. Box 1089

NaN

Conway

AR

72033

1000.0

2007-05-18

16

11

Allison

Rebecca

NaN

3206 Summit Court

NaN

Little Rock

AR

72227

1000.0

2007-04-25

16

12

Allison

Rebecca

NaN

3206 Summit Court

NaN

Little Rock

AR

72227

200.0

2007-06-12

16

```python--f0cfb988-574e-4776-bb7c-02149a8ecfd1
drow="DELETE FROM contributors WHERE last_name=\"Ahrens\";"
db.cursor().execute(drow)
```

```python--7ff9bb3a-b6c5-42c3-8861-635035fb6f4e
db.commit()
out=make_query("SELECT * FROM contributors;")
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

500.0

2007-06-30

16

1

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

2

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

3

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

4

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

5

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

6

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

7

11

Allison

John W.

None

P.O. Box 1089

None

Conway

AR

72033

1000.0

2007-05-18

16

8

12

Allison

Rebecca

None

3206 Summit Court

None

Little Rock

AR

72227

1000.0

2007-04-25

16

9

13

Allison

Rebecca

None

3206 Summit Court

None

Little Rock

AR

72227

200.0

2007-06-12

16

### LIMIT

```python--bd27ad5e-bd09-418d-95f7-fdb33766f026
out=make_query("SELECT * FROM contributors LIMIT 3;")
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

500

2007-06-30

16

1

5

Akin

Charles

None

10187 Sugar Creek Road

None

Bentonville

AR

72712

100

2007-06-16

16

2

6

Akin

Mike

None

181 Baywood Lane

None

Monticello

AR

71655

1500

2007-05-18

16

```python--08b8a233-ea13-4860-a00d-7199e0e3e2de
dfcwci[0:3]
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

Denormalization of Relationships: Two Table Grammar of Data
-----------------------------------------------------------

We will soon see that to feed data to models, we want to denormalize it. Pointers to other tables make logical sense for storage, but not when we want to feed data, both for performance and array shape reasons. This denormalization is achived by a technique and a verb: JOIN.

JOINs are Cartesian Products followed by filterings. They come in different varieties, and all pay attention to the "left" element in the join. The standard Pandas merge is an inner join, and often you will see it being done with 2 dataframes on a commonly named column.

Here the `candidate_id` column in the contributors table is equivalent to the `id` in the candidate table, so we need to be explicit:

```python--06a4556b-9262-4c14-b54c-28f369b82f44
dfcwci.shape, dfcand.shape
```

```output--06a4556b-9262-4c14-b54c-28f369b82f44
((172, 11), (17, 5))
```

```python--d4d3029b-0696-4f35-b8e6-0e6227c9db81
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

```python--6cb0196a-f43e-4b4a-8eea-8cc79f8b0877
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

```python--56e29f91-0160-41f3-9d65-884af79b73bb
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

```python--72a63d94-bb58-44df-91d3-9fd7716b1f1b
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

```python--dea57a6f-c03f-4eeb-90fa-3b00ba9f9eb8
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

### Outer JOIN

#### left outer (contributors on candidates)

This makes sure that everything from the first table is present. Where there is data in the second table corresponding to that in the first table it is preserved, but when there isnt a match in the right table, nulls are used..

![](images/leftouterjoin.png)

![left outer](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_left.png)

```python--a3647d25-289a-4c3a-a461-433b5f3385b6
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id", how="left")[cols_wanted]
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

```python--65f4fcfd-b519-48af-97ea-a8c1dbae960a
explicitjoinsel="""
SELECT 
    COUNT(contributors.id), contributors.first_name, candidates.last_name,
        contributors.candidate_id, candidates.id
FROM 
    contributors LEFT OUTER JOIN candidates 
ON contributors.candidate_id = candidates.id

GROUP BY candidates.last_name;
"""
out=make_query(explicitjoinsel)
make_frame(out, legend=["count(contributors.id)", "contributors.first_name",  
            "contributors.candidate_id", "candidates.id", "candidates.last_name"])
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

count(contributors.id)

contributors.first\_name

contributors.candidate\_id

candidates.id

candidates.last\_name

0

25

Rebecca

Clinton

34

34

1

25

HERBERT

Giuliani

22

22

2

22

Steven

Huckabee

16

16

3

25

ZAINUL

McCain

37

37

4

25

Steve

Obama

20

20

5

25

Bryan

Paul

32

32

6

25

TRAVIS

Romney

35

35

#### right outer (contributors on candidates)

![right outer](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_right.png)

This one guarantees that all the rows in the right one are present. The rows on the left if matched are there, else the corresponding columns are full of nulls

```python--46374c7b-4044-455d-8c6c-7ee792153171
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id", how="right")[cols_wanted]
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name\_x

first\_name\_x

candidate\_id

id

last\_name\_y

0

NaN

NaN

NaN

33

Biden

1

NaN

NaN

NaN

36

Brownback

2

Aaronson

Rebecca

34.0

34

Clinton

3

Aarons

Elaine

34.0

34

Clinton

4

Aarons

Elaine

34.0

34

Clinton

...

...

...

...

...

...

177

ABBOTT

WELDON

35.0

35

Romney

178

ABBOTT

GERALD

35.0

35

Romney

179

ABBOTT

GERALD

35.0

35

Romney

180

NaN

NaN

NaN

38

Tancredo

181

NaN

NaN

NaN

41

Thompson

182 rows × 5 columns

Sqlite has no support for right outer or plain outer. If it did we could write:

```sql
SELECT 
    COUNT(contributors.id), contributors.first_name, candidates.last_name 
FROM 
    contributors RIGHT OUTER JOIN candidates 
ON contributors.candidate_id = candidates.id

GROUP BY candidates.last_name;
```

Instead we note that `right outer (contributors on candidates) = left outer (candidates on contributors)` and use that to make our join.

```python--99df9d78-b9aa-4cec-92b4-fa04b840f832
explicitjoinsel="""
SELECT 
    COUNT(contributors.id), contributors.first_name, candidates.last_name, 
        contributors.candidate_id, candidates.id
FROM 
    candidates LEFT OUTER JOIN contributors 
ON contributors.candidate_id = candidates.id

GROUP BY candidates.last_name;
"""
out=make_query(explicitjoinsel)
make_frame(out, legend=["count(contributors.id)", "contributors.first_name",  
                    "contributors.candidate_id", "candidates.id", "candidates.last_name"])
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

count(contributors.id)

contributors.first\_name

contributors.candidate\_id

candidates.id

candidates.last\_name

0

0

None

Biden

NaN

33

1

0

None

Brownback

NaN

36

2

25

Thomas

Clinton

34.0

34

3

0

None

Dodd

NaN

39

4

0

None

Edwards

NaN

26

5

25

WALTER

Giuliani

22.0

22

6

0

None

Gravel

NaN

24

7

22

William

Huckabee

16.0

16

8

0

None

Hunter

NaN

30

9

0

None

Kucinich

NaN

31

10

25

ZAINUL

McCain

37.0

37

11

25

Thomas

Obama

20.0

20

12

25

William

Paul

32.0

32

13

0

None

Richardson

NaN

29

14

25

WELDON

Romney

35.0

35

15

0

None

Tancredo

NaN

38

16

0

None

Thompson

NaN

41

#### full outer

![](images/outerjoin.png)

Here matching records from both sides are available. Where the other side does not match, we put in nulls.

```python--13d348e3-9562-426a-bbeb-d8ec46c77e91
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id", how="outer")[cols_wanted]
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

16.0

16

Huckabee

1

Akin

Charles

16.0

16

Huckabee

2

Akin

Mike

16.0

16

Huckabee

3

Akin

Rebecca

16.0

16

Huckabee

4

Aldridge

Brittni

16.0

16

Huckabee

...

...

...

...

...

...

177

NaN

NaN

NaN

30

Hunter

178

NaN

NaN

NaN

31

Kucinich

179

NaN

NaN

NaN

29

Richardson

180

NaN

NaN

NaN

38

Tancredo

181

NaN

NaN

NaN

41

Thompson

182 rows × 5 columns

![outer](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_outer.png)

also not supported by sqlite

```sql
SELECT 
    COUNT(contributors.id), contributors.first_name, candidates.last_name 
FROM 
    contributors FULL OUTER JOIN candidates 
ON contributors.candidate_id = candidates.id

GROUP BY candidates.last_name;
```

When to use which?

See this:

http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/

Some Other Useful patterns
--------------------------

### Simple subselect

We do one "select" and then use that in another one...

```python--be54a73c-a693-4e8c-92f3-66ae450c4001
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

```python--82fa4938-a65e-4c35-b202-75837a7c126d
obamaid=dfcand.query("last_name=='Obama'")['id'].values[0]
```

```python--ce953d85-0ee7-4e7b-b1b7-2475eb767643
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

```python--5fb4f4f0-6c1d-40be-b6c9-e8d6d9d3f7e3
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

```python--405e11f0-8487-48f7-8679-b8e53862a6d1
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

Let's expand to not just include Obama, so it looks more like a regular inner join

```python--a4e6cd7e-a917-4605-8b74-ebfdf189acf3
implicitjoinsel="""
SELECT 
    contributors.last_name, contributors.first_name, contributors.amount, candidates.last_name 
FROM 
    contributors, candidates 
WHERE contributors.candidate_id = candidates.id;
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

Agee

Steven

500.0

Huckabee

1

Akin

Charles

100.0

Huckabee

2

Akin

Mike

1500.0

Huckabee

3

Akin

Rebecca

500.0

Huckabee

4

Aldridge

Brittni

250.0

Huckabee

Pandas /SQL
-----------

Lastly, Pandas can execute SQL for you once you have a DBAPI2 connection! So you dont need the support code we wroe to display dataframes from SQL output.

```python--b2c1eb67-1175-4287-9349-dfc79126fef5
pd.read_sql("SELECT * FROM candidates WHERE party= 'D';", db)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

id

first\_name

last\_name

middle\_name

party

0

20

Barack

Obama

D

1

24

Mike

Gravel

D

2

26

John

Edwards

D

3

29

Bill

Richardson

D

4

31

Dennis

Kucinich

D

5

33

Joseph

Biden

D

6

34

Hillary

Clinton

R.

D

7

39

Christopher

Dodd

J.

D

```python--b2b7dd92-d830-43dd-ae45-3e4cbcb6840a
pd.read_sql(implicitjoinsel, db)
```

.dataframe tbody tr th:only-of-type { vertical-align: middle; } <pre><code>.dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; } </code></pre>

last\_name

first\_name

amount

last\_name

0

Agee

Steven

500.0

Huckabee

1

Akin

Charles

100.0

Huckabee

2

Akin

Mike

1500.0

Huckabee

3

Akin

Rebecca

500.0

Huckabee

4

Aldridge

Brittni

250.0

Huckabee

...

...

...

...

...

167

ABESHAUS

MERRILL

120.0

McCain

168

ABRAHAM

GEORGE

800.0

McCain

169

ABRAHAMSON

PETER

50.0

McCain

170

ABRAHAM

SALEM

1000.0

McCain

171

ABRAHAM

SALEM

1300.0

McCain

172 rows × 4 columns

This is very useful if the database is big and out of memory. Sqlite3 is the only db2api database supported. For any other database you should use `SQLAlchemy`. See, for eg: https://plot.ly/ipython-notebooks/big-data-analytics-with-pandas-and-sqlite/

```python--7a751f48-037f-4357-8e23-3199e45317d3
db.close()
```
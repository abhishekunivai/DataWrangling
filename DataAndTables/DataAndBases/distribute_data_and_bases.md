Data Types and Databases
========================

We'd like a data structure that can represent the columns in the data above by their name. In particular, we want a structure that can easily store variables of different types, that stores column names, and that we can reference by column name as well as by indexed position. And it would be nice this data structure came with built-in functions that we can use to manipulate it.

Pandas is a package/library that does all of this! The library is built on top of numpy. There are two basic pandas objects, _series_ and _dataframes_, which can be thought of as enhanced versions of 1D and 2D numpy arrays, respectively. Indeed Pandas attempts to keep all the efficiencies that `numpy` gives us.

For reference, here is a useful pandas [cheat sheet](https://drive.google.com/folderview?id=0ByIrJAE4KMTtaGhRcXkxNHhmY2M&usp=sharing) and the pandas [documentation](https://pandas.pydata.org/pandas-docs/stable/).

```python--b2c1a9a5-ae15-40f1-888b-cf4d0ad7f596
import pandas as pd
```

```python--d7620bfd-5cc2-496d-b5af-ce200c77c6ac
from collections import OrderedDict
def make_frame(list_of_tuples, legend):
    framelist=[]
    for i, cname in enumerate(legend):
        framelist.append((cname,[e[i] for e in list_of_tuples]))
    return pd.DataFrame.from_dict(OrderedDict(framelist)) 
```

Pandas and Tabular Data
-----------------------

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

```python--3257999a-fc2c-4252-bf7e-7f14198a40a9
dfcand=pd.read_csv("data/candidates.txt", sep='|')
dfcand
```

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

```python--27c1940d-b365-4105-bce7-f658c1f37d58
dfcwci=pd.read_csv("data/contributors_with_candidate_id.txt", sep="|")
dfcwci.head()
```

You'll notice that the contributions dont have the first column, so we will need to be cleaning things up a bit...

```python--07380c75-7ea6-41e6-9c6e-5c11da719332
del dfcwci['id']
dfcwci.head()
```

Pandas Data Types: Encoding
---------------------------

The pandas data types are the encodings for our data..you can see them here

```python--7b5085a7-5b1f-4d6f-b94f-e48698a94747
dfcand.dtypes
```

Since names can be many, we'll let them be strings. But the `party` is constrained in the values it can have.

```python--6c8aba96-34a2-42d0-810e-f4c2158126a4
dfcand.party.unique()
```

This is a prime candidate for converting to a categorical(nominal) variable.

```python--c9a14aab-492c-4c3e-a175-99ba2b7fd7af
dfcand['party'] = dfcand.party.astype('category')
```

Things change now

```python--a114f4fc-13b2-4761-b921-fffc50946e0c
dfcand.dtypes
```

```python--2ed7c3fe-66c6-4f43-81ba-2323c6a7a9ed
dfcand.party
```

The implementation is to associate numbers...

```python--128bb7ed-2854-4d89-b7a4-a377aef56bf3
dfcand.party.cat.codes
```

The categories are:

```python--b2c4af42-07d5-4c02-bf6f-3ccc42468c66
dfcand.party.cat.categories
```

And the ordering is False, as these are categoricals:

```python--5b9a5c8f-6694-4937-87c8-9c63567fe81b
dfcand.party.cat.ordered
```

What are good candidates for conversion to categorical here?

```python--a1ead452-5041-479e-adf5-8c562bb9479d
dfcwci.dtypes
```

What about Ordinal variables? We can use Pandas categoricals for this as well. And what if we did not have all the categories in our data?

```python--5fc74749-483f-4e8c-b650-bc3bfcd28c52
dfcwci.state.unique().shape
```

```python--cb8a4e1c-1030-48ef-9f6f-5d517317438f
states = ["AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "DC", "FL", "GA", "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"]
len(states)
```

```python--4c16b716-8617-493a-9ea7-a2bca2869a66
from pandas.api.types import CategoricalDtype
dfcwci['state'] = dfcwci.state.astype(CategoricalDtype(states))
```

```python--3cbb6d05-d2e0-4987-ad21-80cd017c1b3e
dfcwci.state.cat.codes
```

And if for some bizarre reason we encoded the states as ordinal, alphabetically (this is more useful for true ordinals such as restaurant ratings, grades, etc)

```python--87da9b77-3f1b-464f-842e-274c757bd506
dfcwci['state'] = dfcwci.state.astype(CategoricalDtype(states, ordered=True))
```

```python--97badca2-315d-4fa3-a838-fd526f8d05ff
dfcwci.state.cat.ordered
```

```python--d6565632-a475-449d-b177-df499a446d06
dfcwci.sort_values(by='state', ascending=False)
```

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

```python--945499f0-8e52-4f11-a9e9-4edc2f80f9f5
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

```python--0327c80e-1c31-495c-8c7e-32b22bb7b144
from sqlite3 import dbapi2 as sq3
from pathlib import Path
PATHSTART="."
def get_db(dbfile):
    sqlite_db = sq3.connect(Path(PATHSTART) / dbfile)
    return sqlite_db
```

(2) Set up the database with tables. Drop tables if they exist and create them.

```python--4ad6162a-668b-4991-ac7c-8604cc15c0e1
def init_db(dbfile, schema):
    """Creates the database tables."""
    db = get_db(dbfile) 
    db.cursor().executescript(schema)
    db.commit()
    return db
```

Initializing the database:

```python--e920dc9a-0f93-4a23-b6c6-ab6d95d1403b
db=init_db("/tmp/cancont.db", ourschema)
```

### Populating with Pandas!!

```python--eba611e6-0b10-49dd-8ae5-760d668880ca
dfcand.to_sql("candidates", db, if_exists="append", index=False)
```

```python--0c3c81ff-2de9-45f2-ab1f-f48dd1c5f5b2
dfcwci.to_sql("contributors", db, if_exists="append", index=False)
```

Now we can do queries in the lingua franca of databases: SQL

```python--7778633d-e00c-4606-b7a8-6c0f5cb6efbd
sel="""
SELECT * FROM candidates;
"""
c=db.cursor().execute(sel)
```

```python--7720c87a-1f17-4ecb-a771-03307606d71d
c.fetchall()
```

```python--58e48cd5-c2da-4b7b-9af9-d44326590b34
def make_query(sel):
    c=db.cursor().execute(sel)
    return c.fetchall()
```

```python--4dd818ba-5ccd-414b-895f-a9e5f619edce
make_query("SELECT * FROM candidates;")
```

```python--ab4205e6-fa6d-4075-97f7-15cf682fae9e
cont_cols = [e[1] for e in make_query("PRAGMA table_info(candidates);")]
cont_cols
```

```python--0197b13f-887a-4b50-9e7b-fb0a6747f05e
out=make_query("SELECT * FROM candidates;")
make_frame(out, legend=cont_cols)
```

Indexes
-------

```python--b6c862b5-52e1-4e7b-912f-da294842ea13
crind="CREATE INDEX amount_ix ON contributors(amount);"
db.cursor().execute(crind)
db.commit()
```

```python--5c642b43-0635-4bc7-9ad7-129aaa25d527
db.cursor().execute("SELECT sql FROM sqlite_master WHERE type='index'").fetchall()
```

```python--b3ad1275-2bae-4920-8f58-804d6d3f4707
db.cursor().execute("SELECT sql FROM sqlite_master WHERE type='table'").fetchall()
```

```python--59947ecb-1c10-4dfe-b3d8-946768e08013
out=make_query("SELECT * FROM contributors WHERE amount > 2000;")
make_frame(out, legend=cont_cols)
```

Useful Links
------------

*   http://sebastianraschka.com/Articles/sqlite3\_database.html and http://sebastianraschka.com/Articles/2014\_sqlite\_in\_python\_tutorial.html#unique\_indexes
*   https://github.com/tthibo/SQL-Tutorial
*   https://chrisalbon.com
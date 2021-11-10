Pandas, SQL, and the Grammar of Data
====================================

We'd like a data structure that can represent the columns in the data above by their name. In particular, we want a structure that can easily store variables of different types, that stores column names, and that we can reference by column name as well as by indexed position. And it would be nice this data structure came with built-in functions that we can use to manipulate it.

Pandas is a package/library that does all of this! The library is built on top of numpy. There are two basic pandas objects, _series_ and _dataframes_, which can be thought of as enhanced versions of 1D and 2D numpy arrays, respectively. Indeed Pandas attempts to keep all the efficiencies that `numpy` gives us.

For reference, here is a useful pandas [cheat sheet](https://drive.google.com/folderview?id=0ByIrJAE4KMTtaGhRcXkxNHhmY2M&usp=sharing) and the pandas [documentation](https://pandas.pydata.org/pandas-docs/stable/).

```python--05a1acf7-349e-44f5-9af6-77bff1dac714
import pandas as pd
```

```python--a4ea7417-2831-4e1c-af78-24e69f5647c2
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

```python--70882aea-534d-48cc-98e8-bcdf8550c88d
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

```python--7a3bb9b9-9d11-40e9-9e2a-a010680fb0c2
dfcwci=pd.read_csv("data/contributors_with_candidate_id.txt", sep="|")
dfcwci.head()
```

You'll notice that the contributions dont have the first column, so we will need to be cleaning things up a bit...

```python--f783b078-d0f6-40e5-89cc-e47b3c8b6fe9
del dfcwci['id']
dfcwci.head()
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

```python--e71ce8ca-5bf8-4050-8702-fd232c2ea515
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

```python--5ebd8a34-d7bf-428f-b05b-55d3a504b022
from sqlite3 import dbapi2 as sq3
from pathlib import Path
PATHSTART="."
def get_db(dbfile):
    sqlite_db = sq3.connect(Path(PATHSTART) / dbfile)
    return sqlite_db
```

(2) Set up the database with tables. Drop tables if they exist and create them.

```python--3aafe64a-aa67-4a5c-b50a-24886f32e160
def init_db(dbfile, schema):
    """Creates the database tables."""
    db = get_db(dbfile) 
    db.cursor().executescript(schema)
    db.commit()
    return db
```

Initializing the database:

```python--ff3081c3-3eff-445d-98ed-8a7ca4bba8aa
db=init_db("/tmp/cancont.db", ourschema)
```

### Populating with Pandas!!

```python--a245f564-6560-4b04-8656-01122de4d636
dfcand.to_sql("candidates", db, if_exists="append", index=False)
```

```python--2c29293e-68b0-47d5-b864-17122276de58
dfcwci.to_sql("contributors", db, if_exists="append", index=False)
```

Now we can do queries in the lingua franca of databases: SQL

```python--069a4528-60f9-4599-9aaf-eb685ce9764d
sel="""
SELECT * FROM candidates;
"""
c=db.cursor().execute(sel)
```

```python--aed51545-8825-4026-9695-b40717a3b5dd
c.fetchall()
```

```python--19ee4559-9ab3-43bc-b9bf-acfe78ab554c
def make_query(sel):
    c=db.cursor().execute(sel)
    return c.fetchall()
```

```python--0a32a4dc-6802-4d24-ba3a-f7034045e37c
make_query("SELECT * FROM candidates;")
```

```python--dd8d93ef-4633-4e3c-8477-b69daddc67b7
make_query("PRAGMA table_info(candidates);")
```

```python--39b5e62e-06db-4ebc-ad1d-65216ed56034
make_query("PRAGMA table_info(contributors);")
```

```python--bfc860c5-c8d2-4c08-baa9-14296d917ece
candidate_cols = [e[1] for e in make_query("PRAGMA table_info(candidates);")]
candidate_cols
```

```python--17e0defe-07d2-44df-9b32-8b92f6578206
contributor_cols = [e[1] for e in make_query("PRAGMA table_info(contributors);")]
contributor_cols
```

```python--30aa7d77-a3c4-460c-bb91-3f87d90a5559
out=make_query("SELECT * FROM candidates;")
make_frame(out, legend=candidate_cols)
```

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

```python--861a99ea-1e35-45c6-977d-bb7dd71800ed
dfcwci.query("20 <= amount <= 40")
```

```python--a3182dac-1730-4256-b923-87b5c02a3f78
out=make_query("SELECT * FROM contributors WHERE amount BETWEEN 20 AND 40;")
make_frame(out, legend=contributor_cols)
```

You can combine queries on different columns (here a numerical and a categorical):

```python--8cf7fe33-31fe-4dd4-988d-d85a31b037c5
dfcwci.query("state=='VA' & amount < 400")
```

```python--9e222183-d26e-4202-a46c-787ab77d5e79
dfcwci[(dfcwci.state=='VA') & (dfcwci.amount < 400)]
```

```python--25a521ea-8abf-4b08-a996-dbf0f7e755ba
out=make_query("SELECT * FROM contributors WHERE state='VA' AND amount < 400;")
make_frame(out, legend=contributor_cols)
```

Looking for data problems with nulls:

```python--f6741d4c-98e3-4b64-9688-0dfe86841338
dfcwci[dfcwci.state.isnull()]
```

```python--f9c5938a-b57b-4def-8467-569060fb077e
out=make_query("SELECT * FROM contributors WHERE state IS NULL;")
make_frame(out, legend=contributor_cols)
```

Or the other way....

```python--05e6a945-6cd8-4cb8-9850-98d3b39bf7f4
dfcwci[dfcwci.state.notnull()] # or dfcwci[~dfcwci.state.isnull()]
```

```python--4cf450d0-021b-4145-a834-10aada498b41
out=make_query("SELECT * FROM contributors WHERE state IS NOT NULL;")
make_frame(out, legend=contributor_cols)
```

Queries that look if things are in a list...useful for categorical variables or discrete valued numerical variables...

```python--4dba3779-6030-446e-93dd-164466b7eaf4
dfcwci[dfcwci.state.isin(['VA','WA'])].head(10)
```

```python--e9827d95-3b56-4372-929b-ce63a391ace4
out=make_query("SELECT * FROM contributors WHERE state IN ('VA','WA');")
make_frame(out, legend=contributor_cols).head(10)
```

### SORT

After possibly making a query, we want to sort our results...

```python--9d17f420-0678-4524-b518-0483b72cddac
dfcwci.sort_values("amount").head(10)
```

```python--3bf8eb01-cff9-43f8-a350-ad6ebfa79f99
dfcwci.sort_values("amount", ascending=False).head(10)
```

```python--cdb0c882-97ba-4dda-ae67-2b020281d1a0
out=make_query("SELECT * FROM contributors ORDER BY amount;")
make_frame(out, legend=contributor_cols).head(10)
```

```python--eb246b4e-7909-4705-85cc-8c64934739f1
out=make_query("SELECT * FROM contributors ORDER BY amount DESC;")
make_frame(out, legend=contributor_cols).head(10)
```

### SELECT-COLUMNS

Sometimes we only want to get a few columns, not the entire table

```python--f0e396ed-c652-4aa6-8185-263d0cd63201
dfcwci[['first_name', 'amount']].head(10)
```

```python--afc5594a-fac0-4fbb-a252-1fe2bcc7c7cb
out=make_query("SELECT first_name, amount FROM contributors;")
make_frame(out,['first_name', 'amount']).head(10)
```

### SELECT-DISTINCT

Once we have chosen certain columns we might want to drop rows which have duplicate values for some of these columns..

Selecting a distinct set is useful for cleaning. Here, we might wish to focus on contributors rather than contributions and see how many distinct contributors we have. Of-course we might be wrong, some people have identical names.

```python--2e04abc3-7427-4005-be1d-dcca810fbd7d
dfcwci[['last_name','first_name']].count()
```

```python--91bbb917-c454-43b3-82ec-d6e7caadba74
dfcwci[['last_name','first_name']].drop_duplicates().count()
```

```python--fc551153-8418-43b2-a1f7-8885d4439866
out=make_query("SELECT DISTINCT last_name, first_name FROM contributors;")
make_frame(out,['last_name', 'first_name'])
```

Creation and Alteration
-----------------------

So far, when we created the database, we did it using Pandas. Clearly, one ought to be able to populate a SQL database using SQL. We now turn to this use case, as well as the alteration of databases.

### Populate with SQL INSERT

Before we populate a the `candidates` table, lets delete all data from it...

```python--823a640f-57c2-4a97-98f7-86f57f19ce8e
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

```python--2c9e0fcc-eac4-4bbb-ae96-c88996a8dc7f
ins="""
INSERT INTO candidates (id, first_name, last_name, middle_name, party) \
    VALUES (?,?,?,?,?);
"""
```

Now we read the file line by line, not including the header line and slurp in the data. Notice that we only finish the transaction after we have slurped in all the lines. So its all lines or none. When we execute the cursor, the question marks are used a templates with a tuple provided in..

```python--d9cd55e1-7780-4c69-ab61-7d047e0e6017
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

```python--4b464031-126a-4330-a8d7-a3a78683a434
make_query("SELECT * FROM candidates;")
```

### Create new columns with ASSIGN

In Pandas it is simple to create a new column (`pd.Series`) in the dataframe:

```python--b25eb37d-3b4b-43cf-96d8-611d4b6b8dc5
dfcwci['name']=dfcwci['last_name']+", "+dfcwci['first_name']
dfcwci.head(10)
```

One can also use `assign`, which creates a new dataframe...

```python--8441ad21-3b5f-4f30-bd10-cce3ad5c283c
newdf = dfcwci.assign(ucname=dfcwci.last_name+":"+dfcwci.first_name).head(10)
newdf.head()
```

Will the above command actually change `dfcwci`? `assign` creates a whole new dataframe. The dictionary style assigns in memory.

**What if we wanted to change an existing assignment?**

In other words, we are not creating a new column, but rather changing the values associated with a column, based on some criterion

```python--6a602a6a-b1e1-4f68-871c-a44eaf09a89e
dfcwci[dfcwci.state=='VA']
```

Lets get the `name` column we just created...

```python--6fa5660a-d76d-4a21-b2ed-90fc5b87e72f
dfcwci.loc[dfcwci.state=='VA', 'name']
```

Now we set the names from Virginia to be "junk":

```python--af48d44b-e255-4e31-bb63-a18ca26992d0
dfcwci.loc[dfcwci.state=='VA', 'name']="junk"
```

```python--b07ce3a3-df1d-4aa5-8ae7-8c30071a9850
dfcwci.query("state=='VA'")['name']
```

* * *

Let us see the entire process in SQL

```python--3a5fb498-15f9-4500-a0f1-aa9bd6b91026
alt="ALTER TABLE contributors ADD COLUMN name;"
db.cursor().execute(alt)
db.commit()
```

```python--1e3b9f2d-c0b5-41fe-8820-53777cd87619
make_query("PRAGMA table_info(contributors);")
```

```python--597f2bd5-fff3-4905-9717-efad8533694a
out = make_query("SELECT id, last_name,first_name from contributors;")
out2 = [(e[1]+", "+e[2],e[0]) for e in out]
out2[:5]
```

```python--9c533ea5-e798-4c12-9b02-fa4e8bfddf21
alt2="UPDATE contributors SET name = ? WHERE id = ?;"
for ele in out2:
    db.cursor().execute(alt2, ele)
db.commit()
```

```python--81171bb7-5540-4977-b8a6-5a9edfbb7258
out=make_query("SELECT * from contributors;")
print(out[0])
make_frame(out,legend=contributor_cols+["name"]).head(10)
```

And lets now do an assignment to an existing column

```python--e592cfe1-1304-4310-8fbc-430c8e1259ab
upd="UPDATE contributors SET name = 'junk' WHERE state = 'VA';"
db.cursor().execute(upd)
db.commit()
```

```python--fd454398-f910-454b-ab5f-829b3e8d5e38
out=make_query("SELECT * from contributors where state='VA';")
make_frame(out,contributor_cols+["name"]).head(10)
```

### No DROP COLUMN in SQLITE

Its available in other databases. Here you must just re-create your database, or know about this gotcha from the start. (reasons here: https://www.quora.com/Why-cant-SQLite-drop-columns)

```python--9289acf5-9019-4797-9ba9-528bfe751e93
alt="ALTER TABLE contributors DROP COLUMN name;"
db.cursor().execute(alt)
db.commit()
```

Its much simpler in Pandas, of-course

```python--302440d5-60fa-4524-80d1-2a13b0f3bb6f
del dfcwci['name']
```

### AGGREGATE

```python--89f117ae-3b25-4c72-ad2e-aeb48875ef8e
dfcwci.describe()
```

```python--deb7769c-18a5-4420-ae6c-bd4192aa1d02
dfcwci.amount.max()
```

```python--4f21cbdd-c254-4f3d-a2a6-ee4643ab82df
dfcwci[dfcwci.amount==dfcwci.amount.max()]
```

SQL is actually simpler

```python--67a9ccac-6ee8-46b7-be31-9cfabfc2e6d4
out=make_query("SELECT MAX(amount) FROM contributors;")
out
```

```python--19690825-8521-4c8a-b5d4-be8f2225a96c
out=make_query("SELECT *, MAX(amount) AS maxamt FROM contributors;")
print(out)
make_frame(out, legend=contributor_cols+['name','maxamt'])
```

```python--3e5fb245-2543-4e1e-be0a-52b60754b2f4
out=make_query("SELECT COUNT(amount) AS AMOUNTCOUNT FROM contributors;")
print(out)
```

```python--55fc7ded-ef25-491f-a99e-c2b619b48994
dfcwci[dfcwci.amount > dfcwci.amount.max() - 2300]
```

```python--8e5bcc68-84e6-4259-905d-7481bddb518a
out=make_query("SELECT * FROM contributors WHERE amount > (select (MAX(amount) - 2300) FROM contributors);")
make_frame(out, legend=contributor_cols)
```

Aso `MIN`, `SUM`, `AVG`.

### GROUP-AGG

Being able to group data by the value of any column is critical functionality. This is how you understand your sampling, and the distributions of various quantities in your data.

```python--320f7aef-5b70-48aa-a3a5-54ff9cfd1c74
dfcwci.groupby("state").sum()
```

```python--ea4e43b3-cbde-40b5-b639-fa428491abbf
dfcwci.groupby("state")['amount'].mean()
```

```python--2d7a4703-be66-48e9-a92c-fc7b31691c8d
out=make_query("SELECT state,SUM(amount) FROM contributors GROUP BY state;")
make_frame(out, legend=['state','sum'])
```

### DELETE

```python--2ef195b7-a07a-43c4-8e71-561a0c7cbfe8
dfcwci.head()
```

In-place drops

```python--755fec16-9f9f-4654-9ebb-c08437a309f1
df2=dfcwci.copy()
df2.set_index('last_name', inplace=True)
df2.head()
```

```python--66edd806-dfc6-437e-87b8-c0f8590c7779
df2.drop(['Ahrens'], inplace=True)
df2.head()
```

```python--dbc94b9d-51b5-48cf-9f7f-8281ac2227d7
df2.reset_index(inplace=True)
df2.head()
```

The recommended way to do it is to create a new dataframe. This might be impractical if data is very large.

```python--3ab5ae0b-0316-4751-bc2d-156bc7ed77f6
dfcwci=dfcwci[dfcwci.last_name!='Ahrens']
dfcwci.head(10)
```

```python--a6187cdb-9437-4cee-a281-e33227a5f03b
drow="DELETE FROM contributors WHERE last_name=\"Ahrens\";"
db.cursor().execute(drow)
```

```python--9264acd5-81ad-4ec8-b6c3-f6cb4e7d208e
db.commit()
out=make_query("SELECT * FROM contributors;")
make_frame(out, legend=contributor_cols).head(10)
```

### LIMIT

```python--b72e024b-cb30-4c39-b572-36cb95ac3bcc
out=make_query("SELECT * FROM contributors LIMIT 3;")
make_frame(out, legend=contributor_cols).head(10)
```

```python--896ff433-aa10-4f24-98d6-11fb85afe8fa
dfcwci[0:3]
```

Denormalization of Relationships: Two Table Grammar of Data
-----------------------------------------------------------

We will soon see that to feed data to models, we want to denormalize it. Pointers to other tables make logical sense for storage, but not when we want to feed data, both for performance and array shape reasons. This denormalization is achived by a technique and a verb: JOIN.

JOINs are Cartesian Products followed by filterings. They come in different varieties, and all pay attention to the "left" element in the join. The standard Pandas merge is an inner join, and often you will see it being done with 2 dataframes on a commonly named column.

Here the `candidate_id` column in the contributors table is equivalent to the `id` in the candidate table, so we need to be explicit:

```python--e672ee21-f542-4021-8e53-e8034eb5f95f
dfcwci.shape, dfcand.shape
```

```python--00f9ae6e-3ec3-4d18-b922-3d97dc37b06a
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id")
```

This command repeats information about the candidate on each contributor to that candidate. Now you have a flat table.

If you do it in the opposite direction, the result is symmetric, since the `id` is guaranteed to match the `candidate_id` in out case

```python--5e42ff37-e83b-4959-a20d-938391cb2bdb
dfcand.merge(dfcwci, right_on="candidate_id", left_on="id")
```

### Explicit INNER JOIN

The notion above (and the default) in Pandas is an inner join. Think of a cartesian product of the left table by the right one, 16 choices, followed by a drop of all the unmatched rows. Thus it gives us rows that are in both tables:

![](images/innerjoin.png)

(The set images are from http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/ which also has a very nice description of these joins).

![inner join](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_inner.png)

(from http://pandas.pydata.org/pandas-docs/stable/merging.html)

```python--f03d07b7-0c35-4cca-ba8f-74594bc08988
cols_wanted=['last_name_x', 'first_name_x', 'candidate_id', 'id', 'last_name_y']
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id")[cols_wanted]
```

```python--dc8abbe7-d97e-4b01-904a-51d553704ccd
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

Here is an usage example:

```python--09023818-f6f3-4cb5-87d1-69c7c0e6120f
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

### Outer JOIN

#### left outer (contributors on candidates)

This makes sure that everything from the first table is present. Where there is data in the second table corresponding to that in the first table it is preserved, but when there isnt a match in the right table, nulls are used..

![](images/leftouterjoin.png)

![left outer](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_left.png)

```python--2e905a45-b32b-42e8-900e-536ec40b6815
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id", how="left")[cols_wanted]
```

```python--d3f509a5-1c45-4be0-b62e-29ecd875fd43
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

#### right outer (contributors on candidates)

![right outer](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_right.png)

This one guarantees that all the rows in the right one are present. The rows on the left if matched are there, else the corresponding columns are full of nulls

```python--df5cbdfa-0e01-4207-8dfc-7d6ba8298169
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id", how="right")[cols_wanted]
```

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

```python--e314adf7-9d7d-4c34-a141-f66d7cfbbe04
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

#### full outer

![](images/outerjoin.png)

Here matching records from both sides are available. Where the other side does not match, we put in nulls.

```python--18d8f464-f06e-4bcc-a2f7-aeedd9b18517
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id", how="outer")[cols_wanted]
```

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

```python--c4b9bd4e-2b82-4d9c-80ea-22047dfa937a
dfcand.head()
```

```python--1fd7150d-b9a3-456b-9521-cd8fd3ab6ab6
obamaid=dfcand.query("last_name=='Obama'")['id'].values[0]
```

```python--367fc535-a6f0-4b3c-9840-96e0949948b3
obamacontrib=dfcwci.query("candidate_id==%i" % obamaid)
obamacontrib.head()
```

The SQL syntax makes this look like a russian doll scenario where there is a select inside a select..

```python--8f3b18d6-22da-428c-9c07-be3cfd4839d1
russiandollsel="""
SELECT * FROM contributors WHERE 
    candidate_id = (SELECT id from candidates WHERE last_name = 'Obama');
"""
out=make_query(russiandollsel)
make_frame(out, legend=contributor_cols)
```

### Implicit join

This is a SQL only construct which is nevertheless an often seen pattern where we dont do an explicit inner join...

```python--798b70d0-28e8-481d-ac29-5de916e2872e
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

Let's expand to not just include Obama, so it looks more like a regular inner join

```python--a3b2b571-2dc0-4314-a1c8-4f9ffa00c396
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

Pandas /SQL
-----------

Lastly, Pandas can execute SQL for you once you have a DBAPI2 connection! So you dont need the support code we wroe to display dataframes from SQL output.

```python--8dd95635-03b5-4333-adc2-cf0c4d15c5f0
pd.read_sql("SELECT * FROM candidates WHERE party= 'D';", db)
```

```python--cdff9c21-769b-4ede-b80b-60b1c0f07a91
pd.read_sql(implicitjoinsel, db)
```

This is very useful if the database is big and out of memory. Sqlite3 is the only db2api database supported. For any other database you should use `SQLAlchemy`. See, for eg: https://plot.ly/ipython-notebooks/big-data-analytics-with-pandas-and-sqlite/

```python--0a4808d0-8c81-4045-a2c7-1362c08edf12
db.close()
```
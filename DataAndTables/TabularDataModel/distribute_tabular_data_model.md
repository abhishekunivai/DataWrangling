The Tabular Data Model
======================

```python--d30f23ed-bdf9-417c-ad46-7bf4748608e3
import pandas as pd
```

```python--a3819437-b468-426c-b16c-da2613398888
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

```python--032cb28c-ae88-4baa-960f-baaaffaec3c1
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

```python--28f5a34b-2470-4e5b-ac0d-c75195019fec
dfcwci=pd.read_csv("data/contributors_with_candidate_id.txt", sep="|")
dfcwci.head()
```

You'll notice that the contributions dont have the first column, so we will need to be cleaning things up a bit...

```python--6e7c4d78-9ed0-4fc7-bb56-28ce57b276cb
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

```python--fef85cf1-6a8b-4c9c-ae92-d2c1c8466ed7
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

```python--9dda710b-6c64-4fd1-9b9b-475884bb81b5
from sqlite3 import dbapi2 as sq3
from pathlib import Path
PATHSTART="."
def get_db(dbfile):
    sqlite_db = sq3.connect(Path(PATHSTART) / dbfile)
    return sqlite_db
```

(2) Set up the database with tables. Drop tables if they exist and create them.

```python--f89d6af3-1e31-4b0f-8b00-e34cc879f0e5
def init_db(dbfile, schema):
    """Creates the database tables."""
    db = get_db(dbfile) 
    db.cursor().executescript(schema)
    db.commit()
    return db
```

Initializing the database:

```python--bf2076f0-14c3-4c86-afee-3fb2b7903733
db=init_db("/tmp/cancont.db", ourschema)
```

### Populating with Pandas!!

```python--0d98e251-6bf0-49fc-b97d-945e9abb2d5d
dfcand.to_sql("candidates", db, if_exists="append", index=False)
```

```python--95790263-af9e-41ab-9dd8-251c2453c4fd
dfcwci.to_sql("contributors", db, if_exists="append", index=False)
```

Now we can do queries in the lingua franca of databases: SQL

```python--65d83895-bab5-4fcd-a32c-cfb9a0418998
sel="""
SELECT * FROM candidates;
"""
c=db.cursor().execute(sel)
```

```python--fb74c7e9-d4e4-4635-9662-551fa244b569
c.fetchall()
```

```python--1c966835-3b45-4fc6-bd41-58f748be755a
def make_query(sel):
    c=db.cursor().execute(sel)
    return c.fetchall()
```

```python--9852c685-0988-4dba-9bfc-85a164403391
make_query("SELECT * FROM candidates;")
```

```python--9558a98d-5285-424f-a40a-0a6976f62b2f
make_query("PRAGMA table_info(candidates);")
```

```python--24e09232-6566-4fad-91a1-5c91de979221
make_query("PRAGMA table_info(contributors);")
```

```python--525643ec-61d3-4973-aaa3-adffccc4453a
candidate_cols = [e[1] for e in make_query("PRAGMA table_info(candidates);")]
candidate_cols
```

```python--a4515613-4f30-4923-b6d8-c1f9e9ca618d
contributor_cols = [e[1] for e in make_query("PRAGMA table_info(contributors);")]
contributor_cols
```

```python--a16ece9a-ce6e-4523-b392-bfd0ee567883
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

```python--dce77a7e-9aef-4679-a2ca-6377e433c2aa
dfcwci.query("20 <= amount <= 40")
```

```python--790abc00-90f9-42f1-b07a-77ce79b188e0
out=make_query("SELECT * FROM contributors WHERE amount BETWEEN 20 AND 40;")
make_frame(out, legend=contributor_cols)
```

You can combine queries on different columns (here a numerical and a categorical):

```python--dd8d2dc5-4e4b-4d16-b57d-af24ac9d483e
dfcwci.query("state=='VA' & amount < 400")
```

```python--ae6ddbaf-5494-4ca5-9097-166c6e4d9a93
dfcwci[(dfcwci.state=='VA') & (dfcwci.amount < 400)]
```

```python--5cfa8f09-c38a-4f4c-ac70-ec2e58641a8c
out=make_query("SELECT * FROM contributors WHERE state='VA' AND amount < 400;")
make_frame(out, legend=contributor_cols)
```

Queries that look if things are in a list...useful for categorical variables or discrete valued numerical variables...

```python--7dbbba11-1b47-4f0a-9cb3-5cd13414f615
dfcwci[dfcwci.state.isin(['VA','WA'])].head(10)
```

```python--8360bb00-829d-46e3-9602-617660c29c92
out=make_query("SELECT * FROM contributors WHERE state IN ('VA','WA');")
make_frame(out, legend=contributor_cols).head(10)
```

### SELECT-COLUMNS

Sometimes we only want to get a few columns, not the entire table

```python--9c280c70-74e1-4722-8e6c-e67cd1ed4da7
dfcwci[['first_name', 'amount']].head(10)
```

```python--0c4f8534-2e13-4dc1-bebf-8329627a87b0
out=make_query("SELECT first_name, amount FROM contributors;")
make_frame(out,['first_name', 'amount']).head(10)
```

### AGGREGATE

```python--a11ea881-4250-4985-b2e2-b57a1eddcaef
dfcwci.describe()
```

```python--114d7e96-9956-4548-802d-a6790ff6da61
dfcwci.amount.max()
```

SQL is actually simpler

```python--d2cbeb63-ef48-4fdc-a3c0-011275f0ce8c
out=make_query("SELECT MAX(amount) FROM contributors;")
out
```

Aso `MIN`, `SUM`, `AVG`.

### GROUP-AGG

Being able to group data by the value of any column is critical functionality. This is how you understand your sampling, and the distributions of various quantities in your data.

```python--9a77049e-4e2e-4966-9a78-5fb2e5045b34
dfcwci.groupby("state").sum()
```

```python--e00495f2-c21c-467d-979e-fc79245f441f
dfcwci.groupby("state")['amount'].mean()
```

```python--e9b74858-3c75-4b19-b880-70800b3e8612
out=make_query("SELECT state,SUM(amount) FROM contributors GROUP BY state;")
make_frame(out, legend=['state','sum'])
```

Creation and Alteration
-----------------------

So far, when we created the database, we did it using Pandas. Clearly, one ought to be able to populate a SQL database using SQL. We now turn to this use case, as well as the alteration of databases.

### Populate with SQL INSERT

Before we populate a the `candidates` table, lets delete all data from it...

```python--84f6a58a-faaf-4a94-8407-96bc43f1883d
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

```python--a321ef16-38fd-41be-898a-a259ed3bf337
ins="""
INSERT INTO candidates (id, first_name, last_name, middle_name, party) \
    VALUES (?,?,?,?,?);
"""
```

Now we read the file line by line, not including the header line and slurp in the data. Notice that we only finish the transaction after we have slurped in all the lines. So its all lines or none. When we execute the cursor, the question marks are used a templates with a tuple provided in..

```python--ea18531c-5e84-483f-a3ef-3ffd346bc86d
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

```python--616a2fb7-61e0-4d20-ba36-a70ba09d048b
make_query("SELECT * FROM candidates;")
```

### Create new columns with ASSIGN

In Pandas it is simple to create a new column (`pd.Series`) in the dataframe:

```python--1398bd45-415e-44e8-8a50-4a1ccb408b96
dfcwci['name']=dfcwci['last_name']+", "+dfcwci['first_name']
dfcwci.head(10)
```

One can also use `assign`, which creates a new dataframe...

```python--8b9a018f-eae3-4173-85c5-edff357f9700
newdf = dfcwci.assign(ucname=dfcwci.last_name+":"+dfcwci.first_name).head(10)
newdf.head()
```

Will the above command actually change `dfcwci`? `assign` creates a whole new dataframe. The dictionary style assigns in memory.

**What if we wanted to change an existing assignment?**

In other words, we are not creating a new column, but rather changing the values associated with a column, based on some criterion

```python--97c5acec-811d-41e2-bbaf-ee5f106a40db
dfcwci[dfcwci.state=='VA']
```

Lets get the `name` column we just created...

```python--991cf763-2ba7-475b-97a8-1fbb821d9559
dfcwci.loc[dfcwci.state=='VA', 'name']
```

Now we set the names from Virginia to be "junk":

```python--42186896-ada0-49bd-a35f-4a5500b7bfcf
dfcwci.loc[dfcwci.state=='VA', 'name']="junk"
```

```python--5497426f-6a38-4cff-90f6-5d167083901e
dfcwci.query("state=='VA'")['name']
```

* * *

Let us see the entire process in SQL

```python--54dcb473-b574-4d37-9361-e6235eb8cec6
alt="ALTER TABLE contributors ADD COLUMN name;"
db.cursor().execute(alt)
db.commit()
```

```python--2d4987dc-2bea-4f43-9d42-f87fad41817e
make_query("PRAGMA table_info(contributors);")
```

```python--28b277b7-f8a5-4366-b4b3-5af002b303b4
out = make_query("SELECT id, last_name,first_name from contributors;")
out2 = [(e[1]+", "+e[2],e[0]) for e in out]
out2[:5]
```

```python--5a846b0d-6963-47f5-836d-3e264b615686
alt2="UPDATE contributors SET name = ? WHERE id = ?;"
for ele in out2:
    db.cursor().execute(alt2, ele)
db.commit()
```

```python--b2e48679-edfd-40f3-b73d-cdb0b7a67e83
out=make_query("SELECT * from contributors;")
print(out[0])
make_frame(out,legend=contributor_cols+["name"]).head(10)
```

And lets now do an assignment to an existing column

```python--639b53c4-65c3-492d-af5e-491dcd5f89d8
upd="UPDATE contributors SET name = 'junk' WHERE state = 'VA';"
db.cursor().execute(upd)
db.commit()
```

```python--5c367053-9d52-4755-ab1a-3c2c770f93c0
out=make_query("SELECT * from contributors where state='VA';")
make_frame(out,contributor_cols+["name"]).head(10)
```

Denormalization of Relationships: Two Table Grammar of Data
-----------------------------------------------------------

We will soon see that to feed data to models, we want to denormalize it. Pointers to other tables make logical sense for storage, but not when we want to feed data, both for performance and array shape reasons. This denormalization is achived by a technique and a verb: JOIN.

JOINs are Cartesian Products followed by filterings. They come in different varieties, and all pay attention to the "left" element in the join. The standard Pandas merge is an inner join, and often you will see it being done with 2 dataframes on a commonly named column.

Here the `candidate_id` column in the contributors table is equivalent to the `id` in the candidate table, so we need to be explicit:

```python--54de2c78-4215-41bb-8fb7-f8b9158d03b5
dfcwci.shape, dfcand.shape
```

```python--83e89897-8b46-40b0-8903-83c01d3eeda5
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id")
```

This command repeats information about the candidate on each contributor to that candidate. Now you have a flat table.

If you do it in the opposite direction, the result is symmetric, since the `id` is guaranteed to match the `candidate_id` in out case

```python--54a4ee7d-3d6c-4f29-9b50-0cff0fc5dcf6
dfcand.merge(dfcwci, right_on="candidate_id", left_on="id")
```

### Explicit INNER JOIN

The notion above (and the default) in Pandas is an inner join. Think of a cartesian product of the left table by the right one, 16 choices, followed by a drop of all the unmatched rows. Thus it gives us rows that are in both tables:

![](images/innerjoin.png)

(The set images are from http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/ which also has a very nice description of these joins).

![inner join](http://pandas.pydata.org/pandas-docs/stable/_images/merging_merge_on_key_inner.png)

(from http://pandas.pydata.org/pandas-docs/stable/merging.html)

```python--2e2db9f7-6e31-4290-8f5f-695c70945fff
cols_wanted=['last_name_x', 'first_name_x', 'candidate_id', 'id', 'last_name_y']
dfcwci.merge(dfcand, left_on="candidate_id", right_on="id")[cols_wanted]
```

```python--00d24978-2d7e-4800-bc98-dbd8d4d37faa
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

```python--05d2ac07-ae54-46d6-b4ee-a7e689bebcfc
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

Some Other Useful patterns
--------------------------

### Simple subselect

We do one "select" and then use that in another one...

```python--d8feca41-dd41-4d68-81d7-0ccb1aa09954
dfcand.head()
```

```python--1168c69f-df25-4ffc-a233-ace69e406887
obamaid=dfcand.query("last_name=='Obama'")['id'].values[0]
```

```python--cda0d000-3200-46e5-9d63-6222e6d4a459
obamacontrib=dfcwci.query("candidate_id==%i" % obamaid)
obamacontrib.head()
```

The SQL syntax makes this look like a russian doll scenario where there is a select inside a select..

```python--96e0bee0-d864-4a9b-9d03-39207e56ffed
russiandollsel="""
SELECT * FROM contributors WHERE 
    candidate_id = (SELECT id from candidates WHERE last_name = 'Obama');
"""
out=make_query(russiandollsel)
make_frame(out, legend=contributor_cols)
```

### Implicit join

This is a SQL only construct which is nevertheless an often seen pattern where we dont do an explicit inner join...

```python--295941d4-769b-406e-959c-f8c43a42a5d4
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

```python--0aa916d2-ede9-46e6-af11-40d74f18d41a
db.close()
```
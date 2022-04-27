#Python MongoDB

Python can be used in database applications.

One of the most popular NoSQL database is MongoDB.

##1.1 Introduction


**MongoDB**

MongoDB stores data in JSON-like documents, which makes the database very flexible and scalable.

To be able to experiment with the code examples, you will need access to a MongoDB database.

You can download a free MongoDB database at https://www.mongodb.com.

Or get started right away with a MongoDB cloud service at https://www.mongodb.com/cloud/atlas.

**PyMongo**

Python needs a MongoDB driver to access the MongoDB database.
We will use the MongoDB driver "PyMongo".
We recommend that you use PIP to install "PyMongo".

**Test PyMongo**
To test if the installation was successful, or if you already have "pymongo" installed, create a Python page with the following content:



```python
import pymongo
```

If the above code was executed with no errors, "pymongo" is installed and ready to be used.

##1.2 Create Database

To create a database in MongoDB, start by creating a MongoClient object, then specify a connection URL with the correct ip address and the name of the database you want to create.

MongoDB will create the database if it does not exist, and make a connection to it.

Example
Create a database called "mydatabase":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")

mydb = myclient["mydatabase"]
```

MongoDB waits until you have created a collection (table), with at least one document (record) before it actually creates the database (and collection).

You can check if a database exist by listing all databases in you system:

```
print(myclient.list_database_names())
```

Or you can check a specific database by name:

Example
Check if "mydatabase" exists:

```
dblist = myclient.list_database_names()
if "mydatabase" in dblist:
  print("The database exists.")
```


##1.3 Create Collection

**Creating a Collection**

To create a collection in MongoDB, use database object and specify the name of the collection you want to create.

MongoDB will create the collection if it does not exist.

Example
Create a collection called "customers":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

mycol = mydb["customers"]
```

MongoDB waits until you have inserted a document before it actually creates the collection.

Check if Collection Exists

You can check if a collection exist in a database by listing all collections:

Example
Return a list of all collections in your database:

```
print(mydb.list_collection_names())
```

##1.4 Insert Document

**Insert Into Collection**

To insert a record, or document as it is called in MongoDB, into a collection, we use the insert_one() method.

The first parameter of the insert_one() method is a dictionary containing the name(s) and value(s) of each field in the document you want to insert.

Example
Insert a record in the "customers" collection:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydict = { "name": "John", "address": "Highway 37" }

x = mycol.insert_one(mydict)
```
```
Result:

<pymongo.results.InsertOneResult object at 0x03D62918>
```


**Return the _id Field**

The insert_one() method returns a InsertOneResult object, which has a property, inserted_id, that holds the id of the inserted document.

Example
Insert another record in the "customers" collection, and return the value of the _id field:

```
mydict = { "name": "Peter", "address": "Lowstreet 27" }

x = mycol.insert_one(mydict)

print(x.inserted_id)
```

```
Result:

5b1910482ddb101b7042fcd7
```

If you do not specify an _id field, then MongoDB will add one for you and assign a unique id for each document.

In the example above no _id field was specified, so MongoDB assigned a unique _id for the record (document).

**Insert Multiple Documents**

To insert multiple documents into a collection in MongoDB, we use the insert_many() method.

The first parameter of the insert_many() method is a list containing dictionaries with the data you want to insert:

```
Example
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mylist = [
  { "name": "Amy", "address": "Apple st 652"},
  { "name": "Hannah", "address": "Mountain 21"},
  { "name": "Michael", "address": "Valley 345"},
  { "name": "Sandy", "address": "Ocean blvd 2"},
  { "name": "Betty", "address": "Green Grass 1"},
  { "name": "Richard", "address": "Sky st 331"},
  { "name": "Susan", "address": "One way 98"},
  { "name": "Vicky", "address": "Yellow Garden 2"},
  { "name": "Ben", "address": "Park Lane 38"},
  { "name": "William", "address": "Central st 954"},
  { "name": "Chuck", "address": "Main Road 989"},
  { "name": "Viola", "address": "Sideway 1633"}
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)
```

```
Result:
[ObjectId('5b19112f2ddb101964065487'), ObjectId('5b19112f2ddb101964065488'), ObjectId('5b19112f2ddb101964065489'), ObjectId('5b19112f2ddb10196406548a'), ObjectId('5b19112f2ddb10196406548b'), ObjectId('5b19112f2ddb10196406548c'), ObjectId('5b19112f2ddb10196406548d'), ObjectId('5b19112f2ddb10196406548e'), ObjectId('5b19112f2ddb10196406548f'), ObjectId('5b19112f2ddb101964065490'), ObjectId('5b19112f2ddb101964065491'), ObjectId('5b19112f2ddb101964065492')]
```

The insert_many() method returns a InsertManyResult object, which has a property, inserted_ids, that holds the ids of the inserted documents.

**Insert Multiple Documents, with Specified IDs**

If you do not want MongoDB to assign unique ids for you document, you can specify the _id field when you insert the document(s).

Remember that the values has to be unique. Two documents cannot have the same _id.

Example

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mylist = [
  { "_id": 1, "name": "John", "address": "Highway 37"},
  { "_id": 2, "name": "Peter", "address": "Lowstreet 27"},
  { "_id": 3, "name": "Amy", "address": "Apple st 652"},
  { "_id": 4, "name": "Hannah", "address": "Mountain 21"},
  { "_id": 5, "name": "Michael", "address": "Valley 345"},
  { "_id": 6, "name": "Sandy", "address": "Ocean blvd 2"},
  { "_id": 7, "name": "Betty", "address": "Green Grass 1"},
  { "_id": 8, "name": "Richard", "address": "Sky st 331"},
  { "_id": 9, "name": "Susan", "address": "One way 98"},
  { "_id": 10, "name": "Vicky", "address": "Yellow Garden 2"},
  { "_id": 11, "name": "Ben", "address": "Park Lane 38"},
  { "_id": 12, "name": "William", "address": "Central st 954"},
  { "_id": 13, "name": "Chuck", "address": "Main Road 989"},
  { "_id": 14, "name": "Viola", "address": "Sideway 1633"}
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)
```

```
Result:
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

###Q1.4.1 Insert a Single Record in Customers collection
Write a Mongo query to insert a single record in Customers collection.


```python
#db.customers.insert_one({"name": "John", "address": "Highway 37"}); 
```

###Q1.4.2 Use loop to Insert multiple Single Records in Customers collection
Write a Mongo query to insert multiple single records in Customers collection.


```python
name_l = ["John", "Amy", "Hannah"]
address_l = ["Highway 37", "Apple st 652", "Mountain 21"]

for name, address in zip(name_l, address_l):
  db.customers.insert_one({"name": name, "address": address}); 
```

###Q1.4.3 Insert Multiple records in customer collection
Write a mongo query to insert multiple records in Customers Collection.


```python
'''
db.customers.insert_many(
 [
  { "name": "Amy", "address": "Apple st 652"},
  { "name": "Hannah", "address": "Mountain 21"},
  { "name": "Michael", "address": "Valley 345"},
  { "name": "Sandy", "address": "Ocean blvd 2"},
  { "name": "Betty", "address": "Green Grass 1"},
  { "name": "Richard", "address": "Sky st 331"},
  { "name": "Susan", "address": "One way 98"},
  { "name": "Vicky", "address": "Yellow Garden 2"},
  { "name": "Ben", "address": "Park Lane 38"},
  { "name": "William", "address": "Central st 954"},
  { "name": "Chuck", "address": "Main Road 989"},
  { "name": "Viola", "address": "Sideway 1633"}
]
);
'''
```

###Q1.4.4 Insert a Single Record in Customers collection with custom ID
Write a Mongo query to insert a single record in Customers collection with custom ID.


```python
'''
db.customers.insert_one({"_id": "100", "name": "John", "address": "Highway 37"});
'''
```

###Q1.4.5 Insert Multiple records in customer collection with custom ID
Write a mongo query to insert multiple records in Customers Collection with custom ID


```python
'''
db.customers.insert_many(
  [
    { "_id":"200","name": "Amy", "address": "Apple st 652"},
    { "_id":"201","name": "Hannah", "address": "Mountain 21"},
    { "_id":"202","name": "Michael", "address": "Valley 345"},
    { "_id":"203","name": "Sandy", "address": "Ocean blvd 2"},
    { "_id":"204","name": "Betty", "address": "Green Grass 1"},
    { "_id":"205","name": "Richard", "address": "Sky st 331"},
    { "_id":"206","name": "Susan", "address": "One way 98"},
    { "_id":"207","name": "Vicky", "address": "Yellow Garden 2"},
    { "_id":"208","name": "Ben", "address": "Park Lane 38"},
    { "_id":"209","name": "William", "address": "Central st 954"},
    { "_id":"210","name": "Chuck", "address": "Main Road 989"},
    { "_id":"211","name": "Viola", "address": "Sideway 1633"}
  ]
  );
  '''
```

##1.5 Find



In MongoDB we use the find and findOne methods to find data in a collection.

Just like the SELECT statement is used to find data in a table in a MySQL database.

Example
Find the first document in the customers collection:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

x = mycol.find_one()

print(x)
```

```
Result:
{'_id': 1, 'name': 'John', 'address': 'Highway37'}
```

**Find All**

To select data from a table in MongoDB, we can also use the find() method.

The find() method returns all occurrences in the selection.

The first parameter of the find() method is a query object. In this example we use an empty query object, which selects all documents in the collection.

**Note: No parameters in the find() method gives you the same result as SELECT * in MySQL.**


```
Example
Return all documents in the "customers" collection, and print each document:

import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

for x in mycol.find():
  print(x)
```
```
Result:
{'_id': 1, 'name': 'John', 'address': 'Highway37'}
{'_id': 2, 'name': 'Peter', 'address': 'Lowstreet 27'}
{'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
{'_id': 4, 'name': 'Hannah', 'address': 'Mountain 21'}
{'_id': 5, 'name': 'Michael', 'address': 'Valley 345'}
{'_id': 6, 'name': 'Sandy', 'address': 'Ocean blvd 2'}
{'_id': 7, 'name': 'Betty', 'address': 'Green Grass 1'}
{'_id': 8, 'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 9, 'name': 'Susan', 'address': 'One way 98'}
{'_id': 10, 'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 13, 'name': 'Chuck', 'address': 'Main Road 989'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
```

**Return Only Some Fields**

The second parameter of the find() method is an object describing which fields to include in the result.

This parameter is optional, and if omitted, all fields will be included in the result.

Example
Return only the names and addresses, not the _ids:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

for x in mycol.find({},{ "_id": 0, "name": 1, "address": 1 }):
  print(x)
```
```
Result:
{'name': 'John', 'address': 'Highway37'}
{'name': 'Peter', 'address': 'Lowstreet 27'}
{'name': 'Amy', 'address': 'Apple st 652'}
{'name': 'Hannah', 'address': 'Mountain 21'}
{'name': 'Michael', 'address': 'Valley 345'}
{'name': 'Sandy', 'address': 'Ocean blvd 2'}
{'name': 'Betty', 'address': 'Green Grass 1'}
{'name': 'Richard', 'address': 'Sky st 331'}
{'name': 'Susan', 'address': 'One way 98'}
{'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'name': 'Ben', 'address': 'Park Lane 38'}
{'name': 'William', 'address': 'Central st 954'}
{'name': 'Chuck', 'address': 'Main Road 989'}
{'name': 'Viola', 'address': 'Sideway 1633'}
```




**Structure of 'restaurants' collection:**

```
{
  "address": {
     "building": "1007",
     "coord": [ -73.856077, 40.848447 ],
     "street": "Morris Park Ave",
     "zipcode": "10462"
  },
  "borough": "Bronx",
  "cuisine": "Bakery",
  "grades": [
     { "date": { "$date": 1393804800000 }, "grade": "A", "score": 2 },
     { "date": { "$date": 1378857600000 }, "grade": "A", "score": 6 },
     { "date": { "$date": 1358985600000 }, "grade": "A", "score": 10 },
     { "date": { "$date": 1322006400000 }, "grade": "A", "score": 9 },
     { "date": { "$date": 1299715200000 }, "grade": "B", "score": 14 }
  ],
  "name": "Morris Park Bake Shop",
  "restaurant_id": "30075445"
}
```

###Q1.5.1 Display all the documents in the collection
Write a MongoDB query to display all the documents in the collection restaurants.


```python
#db.restaurants.find();
```

###Q1.5.2 Display specific fields of a document
Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine for all the documents in the collection restaurant.


```python
#db.restaurants.find({},{"restaurant_id" : 1,"name":1,"borough":1,"cuisine" :1});
```

###1.5.3 Display specific fields and exclude the field _id for all the documents in the collection
Q. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine, but exclude the field _id for all the documents in the collection restaurant.


```python
#db.restaurants.find({},{"restaurant_id" : 1,"name":1,"borough":1,"cuisine" :1,"_id":0});
```

### 1.5.4 Display specific fields of a document
Q. Write a MongoDB query to display the fields restaurant_id, name, borough and zip code, but exclude the field _id for all the documents in the collection restaurant.


```python
#db.restaurants.find({},{"restaurant_id" : 1,"name":1,"borough":1,"address.zipcode" :1,"_id":0});
```

###1.5.5 Display specific field with conditions
Q. Write a MongoDB query to display all the restaurant which is in the borough Bronx.


```python
#db.restaurants.find({"borough": "Bronx"});
```

##1.6 Query

**Filter the Result**

When finding documents in a collection, you can filter the result by using a query object.

The first argument of the find() method is a query object, and is used to limit the search.

Example
Find document(s) with the address "Park Lane 38":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Park Lane 38" }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)
```
```
Result:
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}
```

**Advanced Query**

To make advanced queries you can use modifiers as values in the query object.

E.g. to find the documents where the "address" field starts with the letter "S" or higher (alphabetically), use the greater than modifier: {"$gt": "S"}:

Example
Find documents where the address starts with the letter "S" or higher:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$gt": "S" } }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)
```
```
Result:
{'_id': 5, 'name': 'Michael', 'address': 'Valley 345'}
{'_id': 8, 'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 10, 'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
```

Filter With Regular Expressions
You can also use regular expressions as a modifier.

Regular expressions can only be used to query strings.

To find only the documents where the "address" field starts with the letter "S", use the regular expression {"$regex": "^S"}:

Example
Find documents where the address starts with the letter "S":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)
```
```
Result:
{'_id': 10, 'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
```


###Q1.6.1 Test whether all the addresses contains the street or not
Write a MongoDB query to know whether all the addresses contains the street or not.


```python
'''
db.restaurants.find(
                     {"address.street" : 
                         { $exists : true } 
                     } 
                   );
'''
```

###Q1.6.2 Find Documents where the coord field value is double
Write a MongoDB query which will select all documents in the restaurants collection where the coord field value is double.


```python
'''
db.restaurants.find(
                    {"address.coord" : 
                       {$type : 1}
                    }
                   );
'''
```

###Q1.6.3 Query to find specific fields using regex
Write a MongoDB query to find the restaurant name, borough, longitude and attitude and cuisine for those restaurants which contains 'mon' as three letters somewhere in its name.


```python
'''
db.restaurants.find(
                   { name : 
                     { $regex : "mon.*", $options: "i" } 
                   },
                       {
                         "name":1,
                         "borough":1,
                         "address.coord":1,
                         "cuisine" :1
                        }
                   );
'''
```

###Q1.6.4 Query to find specific field using regex
Write a MongoDB query to find the restaurant name, borough, longitude and latitude and cuisine for those restaurants which contain 'Mad' as first three letters of its name.


```python
'''
db.restaurants.find(
                   { name : 
                     { $regex : /^Mad/i, } 
                   },
                       {
                         "name":1,
                         "borough":1,
                         "address.coord":1,
                         "cuisine" :1
                        }
                   );
'''
```

###Q1.6.5 Query on multiple fields
Write a MongoDB query to find the restaurants that do not prepare any cuisine of 'American' and their grade score more than 70 and latitude less than -65.754168.


```python
'''
db.restaurants.find(
               {$and:
                    [
                       {"cuisine" : {$ne :"American "}},
                       {"grades.score" : {$gt : 70}},
                       {"address.coord" : {$lt : -65.754168}}
                    ]
                }
                    );
'''
```

##1.7 Sort

**Sort the Result**

Use the sort() method to sort the result in ascending or descending order.

The sort() method takes one parameter for "fieldname" and one parameter for "direction" (ascending is the default direction).

Example
Sort the result alphabetically by name:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydoc = mycol.find().sort("name")

for x in mydoc:
  print(x)
```

**Sort Descending**

Use the value -1 as the second parameter to sort descending.

sort("name", 1) #ascending
sort("name", -1) #descending

Example
Sort the result reverse alphabetically by name:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydoc = mycol.find().sort("name", -1)

for x in mydoc:
  print(x)
```


###Q1.7.1 Sort name of the restaurants
Write a MongoDB query to arrange the name of the restaurants in ascending order along with all the columns.


```python
#db.restaurants.find().sort({"name":1});
```

###Q1.7.2 Sort name of the restaurants in descending order
Write a MongoDB query to arrange the name of the restaurants in descending along with all the columns.


```python
'''
db.restaurants.find().sort(
                          {"name":-1}
                          );
'''
```

###Q1.7.3 Sort cuisine in ascending and for that same cuisine borough should be in descending order.
Write a MongoDB query to arranged the name of the cuisine in ascending order and for that same cuisine borough should be in descending order.


```python
'''
db.restaurants.find().sort(
                           {"cuisine":1,"borough" : -1,}
                          );
'''
```

###Q1.7.4 Query to find restaurants and sort the document in descending order.
Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American ' and achieved a grade point 'A' not belongs to the borough Brooklyn. The document must be displayed according to the cuisine in descending order.


```python
'''
db.restaurants.find( {
                             "cuisine" : {$ne : "American "},
                             "grades.grade" :"A",
                             "borough": {$ne : "Brooklyn"}
                       } 
                    ).sort({"cuisine":-1});
'''
```

##1.8 Delete Document or Collection

**Delete Document**

To delete one document, we use the delete_one() method.

The first parameter of the delete_one() method is a query object defining which document to delete.

Note: If the query finds more than one document, only the first occurrence is deleted.

Example
Delete the document with the address "Mountain 21":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Mountain 21" }

mycol.delete_one(myquery)
```

```
Result:
{'_id': 1, 'name': 'John', 'address': 'Highway37'}
{'_id': 2, 'name': 'Peter', 'address': 'Lowstreet 27'}
{'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
{'_id': 5, 'name': 'Michael', 'address': 'Valley 345'}
{'_id': 6, 'name': 'Sandy', 'address': 'Ocean blvd 2'}
{'_id': 7, 'name': 'Betty', 'address': 'Green Grass 1'}
{'_id': 8, 'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 9, 'name': 'Susan', 'address': 'One way 98'}
{'_id': 10, 'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 13, 'name': 'Chuck', 'address': 'Main Road 989'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
```


**Delete Many Documents**

To delete more than one document, use the delete_many() method.

The first parameter of the delete_many() method is a query object defining which documents to delete.

Example
Delete all documents were the address starts with the letter S:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": {"$regex": "^S"} }

x = mycol.delete_many(myquery)

print(x.deleted_count, " documents deleted.")
```

```
Result:
2 documents deleted.
```

**Delete All Documents in a Collection**

To delete all documents in a collection, pass an empty query object to the delete_many() method:

Example
Delete all documents in the "customers" collection:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

x = mycol.delete_many({})

print(x.deleted_count, " documents deleted.")
```

```
Result:
11 documents deleted.
```


###Q1.8.1 Delete a Document in the collection based on street

Write a query to delete a document which contains Street in its address.


```python
'''
db.restaurants.delete_one(
                     {"address.street" : 
                         { $exists : true } 
                     } 
                   );
'''
```

###Q1.8.2 Delete a Document in the collection based on zipcode
Write a query to delete a document which contains Street in its address.


```python
'''
db.restaurants.delete_one(
                     {"address.zipcode" : 
                         { $exists : true } 
                     } 
                   );
'''
```

###Q1.8.3 Delete many Document in the collection
Write a query to delte all documents which contains Street in its address.


```python
'''
db.restaurants.delete_many(
                     {"address.street" : 
                         { $exists : true } 
                     } 
                   );
'''
```

**Delete Collection**

You can delete a table, or collection as it is called in MongoDB, by using the drop() method.

Example
Delete the "customers" collection:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mycol.drop()
```

The drop() method returns true if the collection was dropped successfully, and false if the collection does not exist.



###Q1.8.4 Delete the restaurant collection
Write a query to drop the restaurant collection.


```python
'''
db.restaurants.drop();
'''
```

###Q1.8.5 Delete the Customer collection
Write a query to drop the customer collection.


```python
'''
db.customers.drop();
'''
```

##1.10 Update Collection

**Update Collection**

You can update a record, or document as it is called in MongoDB, by using the update_one() method.

The first parameter of the update_one() method is a query object defining which document to update.

Note: If the query finds more than one record, only the first occurrence is updated.

The second parameter is an object defining the new values of the document.

Example
Change the address from "Valley 345" to "Canyon 123":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Valley 345" }
newvalues = { "$set": { "address": "Canyon 123" } }

mycol.update_one(myquery, newvalues)

#print "customers" after the update:
for x in mycol.find():
  print(x)
```

```
Result:
{'_id': 1, 'name': 'John', 'address': 'Highway37'}
{'_id': 2, 'name': 'Peter', 'address': 'Lowstreet 27'}
{'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
{'_id': 4, 'name': 'Hannah', 'address': 'Mountain 21'}
{'_id': 5, 'name': 'Michael', 'address': 'Canyon 123'}
{'_id': 6, 'name': 'Sandy', 'address': 'Ocean blvd 2'}
{'_id': 7, 'name': 'Betty', 'address': 'Green Grass 1'}
{'_id': 8, 'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 9, 'name': 'Susan', 'address': 'One way 98'}
{'_id': 10, 'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 13, 'name': 'Chuck', 'address': 'Main Road 989'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
```

**Update Many**

To update all documents that meets the criteria of the query, use the update_many() method.

Example
Update all documents where the address starts with the letter "S":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }
newvalues = { "$set": { "name": "Minnie" } }

x = mycol.update_many(myquery, newvalues)

print(x.modified_count, "documents updated.")
```
```
Result:
2 documents updated.
```


**Customers collection**

{
{'_id': 1, 'name': 'John', 'address': 'Highway37'}
{'_id': 2, 'name': 'Peter', 'address': 'Lowstreet 27'}
{'_id': 3, 'name': 'Amy', 'address': 'Apple st 652'}
{'_id': 4, 'name': 'Hannah', 'address': 'Mountain 21'}
{'_id': 5, 'name': 'Michael', 'address': 'Canyon 123'}
{'_id': 6, 'name': 'Sandy', 'address': 'Ocean blvd 2'}
{'_id': 7, 'name': 'Betty', 'address': 'Green Grass 1'}
{'_id': 8, 'name': 'Richard', 'address': 'Sky st 331'}
{'_id': 9, 'name': 'Susan', 'address': 'One way 98'}
{'_id': 10, 'name': 'Vicky', 'address': 'Yellow Garden 2'}
{'_id': 11, 'name': 'Ben', 'address': 'Park Lane 38'}
{'_id': 12, 'name': 'William', 'address': 'Central st 954'}
{'_id': 13, 'name': 'Chuck', 'address': 'Main Road 989'}
{'_id': 14, 'name': 'Viola', 'address': 'Sideway 1633'}
}

###Q1.10.1 Update a Documnet in the collection
Write a query to chnage the name of John to Andrew in customer collection.



```python
'''
db.customers.update_one("name": "John","$set": { "name": "Andrew" })
'''
```

###Q1.10.2 Update many Documents in the collection
Write a query to Update the name of all the documents to 'Michael' where the address starts with the letter "M".


```python
'''
 db.customers.update_many("address": { "$regex": "^M" }, "$set": { "name": "Michael" })
'''
```

#Basic SQL

Python can be used in database applications.

One of the most popular databases is MySQL.

##2.1 Introduction

**MySQL Database**

To be able to experiment with the code examples, you should have MySQL installed on your computer.

You can download a free MySQL database at https://www.mysql.com/downloads/.

**Install MySQL Driver**

Python needs a MySQL driver to access the MySQL database.

In this tutorial we will use the driver "MySQL Connector".

We recommend that you use PIP to install "MySQL Connector".

**Test MySQL Connector**

To test if the installation was successful, or if you already have "MySQL Connector" installed, create a Python page with the following content:


```python
import mysql.connector
```

If the above code was executed with no errors, "MySQL Connector" is installed and ready to be used.

Create Connection
Start by creating a connection to the database.

Use the username and password from your MySQL database:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword"
)

print(mydb)
```
```
Result:
<mysql.connector.connection.MySQLConnection object ar 0x016645F0>
```

Now you can start querying the database using SQL statements.

##2.2 Create Database

**Creating a Database**

To create a database in MySQL, use the "CREATE DATABASE" statement:

Example
create a database named "mydatabase":
```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword"
)

mycursor = mydb.cursor()

mycursor.execute("CREATE DATABASE mydatabase")
```
If the above code was executed with no errors, you have successfully created a database.

**Check if Database Exists**

You can check if a database exist by listing all databases in your system by using the "SHOW DATABASES" statement:

Example
Return a list of your system's databases:
```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword"
)

mycursor = mydb.cursor()

mycursor.execute("SHOW DATABASES")

for x in mycursor:
  print(x)
```
Or you can try to access the database when making the connection:

Example
Try connecting to the database "mydatabase":
```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)
```
If the database does not exist, you will get an error.

##2.3 Create Table

**Creating a Table**

To create a table in MySQL, use the "CREATE TABLE" statement.

Make sure you define the name of the database when you create the connection

Example
Create a table named "customers":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("CREATE TABLE customers (name VARCHAR(255), address VARCHAR(255))")
```
If the above code was executed with no errors, you have now successfully created a table.

Check if Table Exists
You can check if a table exist by listing all tables in your database with the "SHOW TABLES" statement:

Example
Return a list of your system's databases:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SHOW TABLES")

for x in mycursor:
  print(x)
```
```
Result:
('customers',)
```

**Primary Key**
When creating a table, you should also create a column with a unique key for each record.

This can be done by defining a PRIMARY KEY.

We use the statement "INT AUTO_INCREMENT PRIMARY KEY" which will insert a unique number for each record. Starting at 1, and increased by one for each record.

Example
Create primary key when creating the table:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("CREATE TABLE customers (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255), address VARCHAR(255))")
```
If the table already exists, use the ALTER TABLE keyword:

Example
Create primary key on an existing table:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("ALTER TABLE customers ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY")
```


###Q2.3.1 Create a simple table countries including columns country_id,country_name and region_id
Write a SQL statement to create a simple table countries including columns country_id,country_name and region_id.


```python
'''
CREATE TABLE countries( 
COUNTRY_ID varchar(2),
COUNTRY_NAME varchar(40),
REGION_ID decimal(10,0)
);
'''
```

###Q2.3.2 Create the structure of a table duplicate_countries similar to countries
Write a SQL statement to create the structure of a table dup_countries similar to countries.


```python
'''
CREATE TABLE IF NOT EXISTS duplicate_countries
LIKE countries;
'''
```

###Q2.3.3 Create a duplicate copy of countries table including structure and data by name dup_countries
Write a SQL statement to create a duplicate copy of countries table including structure and data by name dup_countries.


```python
'''
CREATE TABLE IF NOT EXISTS dup_countries
AS SELECT * FROM  countries;
'''
```

###Q2.3.4 Create a table countries set a constraint NOT NULL
Write a SQL statement to create a table countries set a constraint NOT NULL.


```python
'''
CREATE TABLE IF NOT EXISTS countries ( 
COUNTRY_ID varchar(2) NOT NULL,
COUNTRY_NAME varchar(40) NOT NULL,
REGION_ID decimal(10,0) NOT NULL
);
'''
```

###Q2.3.5 Create a table jobs, and check one of it column max_salary amount exceeding the upper limit 25000
Write a SQL statement to create a table named jobs including columns job_id, job_title, min_salary, max_salary and check whether the max_salary amount exceeding the upper limit 25000.


```python
'''
CREATE TABLE IF NOT EXISTS jobs ( 
JOB_ID varchar(10) NOT NULL , 
JOB_TITLE varchar(35) NOT NULL, 
MIN_SALARY decimal(6,0), 
MAX_SALARY decimal(6,0) 
CHECK(MAX_SALARY<=25000)
);
'''
```

##2.4 Insert

**Insert Into Table**

To fill a table in MySQL, use the "INSERT INTO" statement.

Example
Insert a record in the "customers" table:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("John", "Highway 21")
mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record inserted.")
```
```
Result:
1 record inserted.
```

**Important!: Notice the statement: mydb.commit(). It is required to make the changes, otherwise no changes are made to the table.**

**Insert Multiple Rows**

To insert multiple rows into a table, use the executemany() method.

The second parameter of the executemany() method is a list of tuples, containing the data you want to insert:

Example
Fill the "customers" table with data:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = [
  ('Peter', 'Lowstreet 4'),
  ('Amy', 'Apple st 652'),
  ('Hannah', 'Mountain 21'),
  ('Michael', 'Valley 345'),
  ('Sandy', 'Ocean blvd 2'),
  ('Betty', 'Green Grass 1'),
  ('Richard', 'Sky st 331'),
  ('Susan', 'One way 98'),
  ('Vicky', 'Yellow Garden 2'),
  ('Ben', 'Park Lane 38'),
  ('William', 'Central st 954'),
  ('Chuck', 'Main Road 989'),
  ('Viola', 'Sideway 1633')
]

mycursor.executemany(sql, val)

mydb.commit()

print(mycursor.rowcount, "was inserted.")

```
```
Result:
13 record was inserted.
```

**Get Inserted ID**

You can get the id of the row you just inserted by asking the cursor object.

Note: If you insert more than one row, the id of the last inserted row is returned.

Example
Insert one row, and return the ID:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)"
val = ("Michelle", "Blue Village")
mycursor.execute(sql, val)

mydb.commit()

print("1 record inserted, ID:", mycursor.lastrowid)
```
```
Result:
1 record inserted, ID: 15
```



###Q2.4.1 Insert a record with your own value into the table countries against each columns



Write a SQL statement to insert a record with your own value into the table countries against each columns.

Structure of the table countries.
```
+--------------+---------------+------+-----+---------+-------+
| Field        | Type          | Null | Key | Default | Extra |
+--------------+---------------+------+-----+---------+-------+
| COUNTRY_ID   | varchar(2)    | YES  |     | NULL    |       |
| COUNTRY_NAME | varchar(40)   | YES  |     | NULL    |       |
| REGION_ID    | decimal(10,0) | YES  |     | NULL    |       |
+--------------+---------------+------+-----+---------+-------+	
```


```python
'''
INSERT INTO countries VALUES('C1','India',1001);
'''
```

###Q2.4.2 Insert NULL values against region_id column for a row of countries table
Write a SQL statement to insert NULL values against region_id column for a row of countries table.


```python
'''
INSERT INTO countries (country_id,country_name,region_id) VALUES('C1','India',NULL);
'''
```

###Q2.4.3 Insert 3 rows by a single insert statement
Write a SQL statement to insert 3 rows by a single insert statement into the table countries.
Structure of the table countries.
```
+--------------+---------------+------+-----+---------+-------+
| Field        | Type          | Null | Key | Default | Extra |
+--------------+---------------+------+-----+---------+-------+
| COUNTRY_ID   | varchar(2)    | YES  |     | NULL    |       |
| COUNTRY_NAME | varchar(40)   | YES  |     | NULL    |       |
| REGION_ID    | decimal(10,0) | YES  |     | NULL    |       |
+--------------+---------------+------+-----+---------+-------+	
```


```python
'''
INSERT INTO countries VALUES('C0001','India',1001),
('C0002','USA',1007),('C0003','UK',1003);
'''
```

###Q2.4.4 Insert rows from country_new table to countries table
Write a SQL statement insert rows from country_new table to countries table.

Here is the rows for country_new table. Assume that, the countries table is empty.
```
+------------+--------------+-----------+
| COUNTRY_ID | COUNTRY_NAME | REGION_ID |
+------------+--------------+-----------+
| C0001      | India        |      1001 |
| C0002      | USA          |      1007 |
| C0003      | UK           |      1003 |
+------------+--------------+-----------+
```


```python
'''
INSERT INTO countries
SELECT * FROM country_new;
'''
```

###Q2.4.5 Create duplicate of countries table named country_new with all structure and data
Write a SQL statement to create duplicate of countries table named country_new with all structure and data.

Here in the following is the structure of the table countries.

```
+--------------+---------------+------+-----+---------+-------+
| Field        | Type          | Null | Key | Default | Extra |
+--------------+---------------+------+-----+---------+-------+
| COUNTRY_ID   | varchar(2)    | YES  |     | NULL    |       |
| COUNTRY_NAME | varchar(40)   | YES  |     | NULL    |       |
| REGION_ID    | decimal(10,0) | YES  |     | NULL    |       |
+--------------+---------------+------+-----+---------+-------+	
```


```python
'''
CREATE TABLE IF NOT EXISTS country_new
AS SELECT * FROM countries;
'''
```

##2.5 Select Statements

**Select From a Table**

To select from a table in MySQL, use the "SELECT" statement:

Example
Select all records from the "customers" table, and display the result:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
```
Result:
(1, 'John', 'Highway 21')
(2, 'Peter', 'Lowstreet 27')
(3, 'Amy', 'Apple st 652')
(4, 'Hannah', 'Mountain 21')
(5, 'Michael', 'Valley 345')
(6, 'Sandy', 'Ocean blvd 2')
(7, 'Betty', 'Green Grass 1')
(8, 'Richard', 'Sky st 331')
(9, 'Susan', 'One way 98')
(10, 'Vicky', 'Yellow Garden 2')
(11, 'Ben', 'Park Lane 38')
(12, 'William', 'Central st 954')
(13, 'Chuck', 'Main Road 989')
(14, 'Viola', 'Sideway 1633')
(15, 'Michelle', 'Blue Village')
```

Note: We use the fetchall() method, which fetches all rows from the last executed statement.

**Selecting Columns**

To select only some of the columns in a table, use the "SELECT" statement followed by the column name(s):

Example
Select only the name and address columns:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT name, address FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
```
Result:
('John', 'Highway 21')
('Peter', 'Lowstreet 27')
('Amy', 'Apple st 652')
('Hannah', 'Mountain 21')
('Michael', 'Valley 345')
('Sandy', 'Ocean blvd 2')
('Betty', 'Green Grass 1')
('Richard', 'Sky st 331')
('Susan', 'One way 98')
('Vicky', 'Yellow Garden 2')
('Ben', 'Park Lane 38')
('William', 'Central st 954')
('Chuck', 'Main Road 989')
('Viola', 'Sideway 1633')
('Michelle', 'Blue Village')
```

**Using the fetchone() Method**

If you are only interested in one row, you can use the fetchone() method.

The fetchone() method will return the first row of the result:

Example
Fetch only one row:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchone()

print(myresult)
```
```
Result:
(1, 'John', 'Highway 21')
```

###Q2.5.1 Display particular columns of the Table
Write a SQL query to find the name and year of the movies. Return movie title, movie release year. (Refer to the Movie table of the Movie Database in section 2.11 )


```python
'''
SELECT mov_title, mov_year
FROM movie;
'''
```

###Q2.5.2 Find the year when the movie American Beauty released
From the Movie table, write a SQL query to find when the movie ‘American Beauty’ released. Return movie release year.(Refer section 2.11 for database)


```python
'''
SELECT mov_year
FROM movie
WHERE mov_title='American Beauty';
'''
```

##2.6 Where Clause

**Select With a Filter**

When selecting records from a table, you can filter the selection by using the "WHERE" statement:

Example
Select record(s) where the address is "Park Lane 38": result:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address ='Park Lane 38'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

```
Result:
(11, 'Ben', 'Park Lane 38')
```

**Wildcard Characters**

You can also select the records that starts, includes, or ends with a given letter or phrase.

Use the %  to represent wildcard characters:

Example
Select records where the address contains the word "way":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address LIKE '%way%'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
```
Result:
(1, 'John', 'Highway 21')
(9, 'Susan', 'One way 98')
(14, 'Viola', 'Sideway 1633')
```

**Prevent SQL Injection**

When query values are provided by the user, you should escape the values.

This is to prevent SQL injections, which is a common web hacking technique to destroy or misuse your database.

The mysql.connector module has methods to escape query values:

Example
Escape query values by using the placholder %s method:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )

mycursor.execute(sql, adr)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
```
Result:
(10, 'Vicky', 'Yellow Garden 2')
```


###Q26.1 Find the movie which was released before 1998
From the Movie table, write a SQL query to find those movies, which was released before 1998. Return movie title. (Refer section 2.11 for database)


```python
'''
SELECT mov_title
FROM movie
WHERE mov_year<=1998;
'''
```

###Q2.6.2 Find the name of all reviewers who have rated 7 or more stars to their rating.
From the Reviewers and Rating tables, write a SQL query to find all reviewers who have rated 7 or more stars to their rating. Return reviewer name. (For database refer Section 2.11)



```python
'''
SELECT reviewer.rev_name
FROM reviewer, rating
WHERE rating.rev_id = reviewer.rev_id
AND rating.rev_stars>=7 
AND reviewer.rev_name IS NOT NULL;
'''
```

###Q2.6.3 Find the titles of the movies with ID 905, 907, 917
From the Movie table, write a SQL query to find the movies with ID 905 or 907 or 917. Return movie title. (Refer section 2.11 for database)


```python
'''
SELECT mov_title
FROM movie
WHERE mov_id in (905, 907, 917);
'''
```

###Q2.6.4 Find the ID number for the actor whose first name is 'Woody' and the last name is 'Allen'
Find the ID number for the actor whose first name is 'Woody' and the last name is 'Allen'. (Refer section 2.11 for database)


```python
'''
SELECT act_id
FROM actor 
WHERE act_fname='Woody' 
AND act_lname='Allen';
'''
```

###Q2.6.5 Find all the movies which released in the country other than UK
From the Movie table, write a SQL query to find those movies, which released in the country besides UK. Return movie title, movie year, movie time, date of release, releasing country. (Refer Section 2.11 for database)


```python
'''
SELECT mov_title, mov_year, mov_time, 
mov_dt_rel AS Date_of_Release, 
mov_rel_country AS Releasing_Country
FROM movie
WHERE mov_rel_country<>'UK';
'''
```

##2.7 Order By Clause

**Sort the Result**

Use the ORDER BY statement to sort the result in ascending or descending order.

The ORDER BY keyword sorts the result ascending by default. To sort the result in descending order, use the DESC keyword.

Example
Sort the result alphabetically by name: result:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers ORDER BY name"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)

```
```
Result:
(3, 'Amy', 'Apple st 652')
(11, 'Ben', 'Park Lane 38')
(7, 'Betty', 'Green Grass 1')
(13, 'Chuck', 'Main Road 989')
(4, 'Hannah', 'Mountain 21')
(1, 'John', 'Highway 21')
(5, 'Michael', 'Valley 345')
(15, 'Michelle', 'Blue Village') (2, 'Peter', 'Lowstreet 27')
(8, 'Richard', 'Sky st 331')
(6, 'Sandy', 'Ocean blvd 2')
(9, 'Susan', 'One way 98')
(10, 'Vicky', 'Yellow Garden 2')
(14, 'Viola', 'Sideway 1633')
(12, 'William', 'Central st 954')
```

**ORDER BY DESC**

Use the DESC keyword to sort the result in a descending order.

Example
Sort the result reverse alphabetically by name:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers ORDER BY name DESC"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
```
Result:
(12, 'William', 'Central st 954') (14, 'Viola', 'Sideway 1633')
(10, 'Vicky', 'Yellow Garden 2')
(9, 'Susan', 'One way 98')
(6, 'Sandy', 'Ocean blvd 2')
(8, 'Richard', 'Sky st 331')
(2, 'Peter', 'Lowstreet 27')
(15, 'Michelle', 'Blue Village') (5, 'Michael', 'Valley 345')
(1, 'John', 'Highway 21')
(4, 'Hannah', 'Mountain 21')
(13, 'Chuck', 'Main Road 989')
(7, 'Betty', 'Green Grass 1')
(11, 'Ben', 'Park Lane 38')
(3, 'Amy', 'Apple st 652')
```

###2.7.1 Find all the years which produced at least one movie and that received a rating of more than 3 stars
From the Movie and Rating tables, write a SQL query to find those years, which produced at least one movie and that, received a rating of more than three stars. Sort the result-set in ascending order by movie year. Return movie year. (Refer Section 2.11 for database)


```python
'''
SELECT DISTINCT mov_year 
FROM movie 
WHERE mov_id IN (
SELECT mov_id 
FROM rating 
WHERE rev_stars>3) 
ORDER BY mov_year;
'''
```

###2.7.2 Find the reviewer name, movie title, and stars for those movies which reviewed by a reviewer and must be rated
From the following tables, write a SQL query to find those movies, which reviewed by a reviewer and got a rating. Sort the result-set in ascending order by reviewer name, movie title, review Stars. Return reviewer name, movie title, review Stars. (Refer Section 2.11 for database)


```python
'''
SELECT rev_name, mov_title, rev_stars 
 FROM reviewer, rating, movie 
  WHERE reviewer.rev_id=rating.rev_id 
   AND movie.mov_id=rating.mov_id 
     AND reviewer.rev_name IS NOT NULL 
       AND rating.rev_stars IS NOT NULL
ORDER BY rev_name, mov_title, rev_stars;
'''
```

Sample table: orders (For Q2.7.3, Q2.7.4 and Q2.7.5)
```
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```

###Q2.7.3 Display the orders according to the order number arranged by ascending order
From the ORDERS table, write a SQL query to find all the orders. Sort the result-set in ascending order by ord_no. Return all fields.




```python
'''
SELECT * 
FROM orders ORDER BY ord_no;
'''
```

###Q2.7.4 Arrange the orders according to the order date
From the ORDERS table, write a SQL query to find all the orders. Sort the result-set in descending order by ord_date. Return all fields.




```python
'''
SELECT * 
FROM orders 
ORDER BY ord_date DESC;
'''
```

###Q2.7.5 Display the orders according to older date with highest purchase amount will come first
From the Orders table, write a SQL query to find all the orders. Sort the result-set in descending order by ord_date and purch_amt. Return all fields.


```python
'''
SELECT * 
FROM orders 
ORDER BY ord_date, purch_amt DESC;
'''
```

##2.8 Update

**Update Table**

You can update existing records in a table by using the "UPDATE" statement:

Example
Overwrite the address column from "Valley 345" to "Canyon 123":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'"

mycursor.execute(sql)

mydb.commit()

print(mycursor.rowcount, "record(s) affected")
```
```
Result:
1 record(s) affected
```

Important!: Notice the statement: mydb.commit(). It is required to make the changes, otherwise no changes are made to the table.

Notice the WHERE clause in the UPDATE syntax: The WHERE clause specifies which record or records that should be updated. If you omit the WHERE clause, all records will be updated!

**Prevent SQL Injection**

It is considered a good practice to escape the values of any query, also in update statements.

This is to prevent SQL injections, which is a common web hacking technique to destroy or misuse your database.

The mysql.connector module uses the placeholder %s to escape values in the delete statement:

Example
Escape values by using the placeholder %s method:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "UPDATE customers SET address = %s WHERE address = %s"
val = ("Valley 345", "Canyon 123")

mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record(s) affected")
```
```
Result:
1 record(s) affected
```


Sample Table Employees (For Q2.8.1 to Q2.8.5)

```
+-------------+-------------+-------------+----------+--------------------+------------+------------+----------+----------------+------------+---------------+
| EMPLOYEE_ID | FIRST_NAME  | LAST_NAME   | EMAIL    | PHONE_NUMBER       | HIRE_DATE  | JOB_ID     | SALARY   | COMMISSION_PCT | MANAGER_ID | DEPARTMENT_ID |
+-------------+-------------+-------------+----------+--------------------+------------+------------+----------+----------------+------------+---------------+
|         100 | Steven      | King        | SKING    | 515.123.4567       | 1987-06-17 | AD_PRES    | 24000.00 |           0.00 |          0 |   		  90 |
|         101 | Neena       | Kochhar     | NKOCHHAR | 515.123.4568       | 1987-06-18 | AD_VP      | 17000.00 |           0.00 |        100 |            90 |
|         102 | Lex         | De Haan     | LDEHAAN  | 515.123.4569       | 1987-06-19 | AD_VP      | 17000.00 |           0.00 |        100 |            90 |
|         103 | Alexander   | Hunold      | AHUNOLD  | 590.423.4567       | 1987-06-20 | IT_PROG    |  9000.00 |           0.00 |        102 |            60 |
|         104 | Bruce       | Ernst       | BERNST   | 590.423.4568       | 1987-06-21 | IT_PROG    |  6000.00 |           0.00 |        103 |            60 |
|         105 | David       | Austin      | DAUSTIN  | 590.423.4569       | 1987-06-22 | IT_PROG    |  4800.00 |           0.00 |        103 |            60 |
|         106 | Valli       | Pataballa   | VPATABAL | 590.423.4560       | 1987-06-23 | IT_PROG    |  4800.00 |           0.00 |        103 |            60 |
|         107 | Diana       | Lorentz     | DLORENTZ | 590.423.5567       | 1987-06-24 | IT_PROG    |  4200.00 |           0.00 |        103 |            60 |
|         108 | Nancy       | Greenberg   | NGREENBE | 515.124.4569       | 1987-06-25 | FI_MGR     | 12000.00 |           0.00 |        101 |           100 |
|         109 | Daniel      | Faviet      | DFAVIET  | 515.124.4169       | 1987-06-26 | FI_ACCOUNT |  9000.00 |           0.00 |        108 |           100 |
|         110 | John        | Chen        | JCHEN    | 515.124.4269       | 1987-06-27 | FI_ACCOUNT |  8200.00 |           0.00 |        108 |           100 |
|         111 | Ismael      | Sciarra     | ISCIARRA | 515.124.4369       | 1987-06-28 | FI_ACCOUNT |  7700.00 |           0.00 |        108 |           100 |
|         112 | Jose Manuel | Urman       | JMURMAN  | 515.124.4469       | 1987-06-29 | FI_ACCOUNT |  7800.00 |           0.00 |        108 |           100 |
|         113 | Luis        | Popp        | LPOPP    | 515.124.4567       | 1987-06-30 | FI_ACCOUNT |  6900.00 |           0.00 |        108 |           100 |
|         114 | Den         | Raphaely    | DRAPHEAL | 515.127.4561       | 1987-07-01 | PU_MAN     | 11000.00 |           0.00 |        100 |            30 |
|         115 | Alexander   | Khoo        | AKHOO    | 515.127.4562       | 1987-07-02 | PU_CLERK   |  3100.00 |           0.00 |        114 |            30 |
|         116 | Shelli      | Baida       | SBAIDA   | 515.127.4563       | 1987-07-03 | PU_CLERK   |  2900.00 |           0.00 |        114 |            30 |
|         117 | Sigal       | Tobias      | STOBIAS  | 515.127.4564       | 1987-07-04 | PU_CLERK   |  2800.00 |           0.00 |        114 |            30 |
|         118 | Guy         | Himuro      | GHIMURO  | 515.127.4565       | 1987-07-05 | PU_CLERK   |  2600.00 |           0.00 |        114 |            30 |
|         119 | Karen       | Colmenares  | KCOLMENA | 515.127.4566       | 1987-07-06 | PU_CLERK   |  2500.00 |           0.00 |        114 |            30 |
|         120 | Matthew     | Weiss       | MWEISS   | 650.123.1234       | 1987-07-07 | ST_MAN     |  8000.00 |           0.00 |        100 |            50 |
|         121 | Adam        | Fripp       | AFRIPP   | 650.123.2234       | 1987-07-08 | ST_MAN     |  8200.00 |           0.00 |        100 |            50 |
|         122 | Payam       | Kaufling    | PKAUFLIN | 650.123.3234       | 1987-07-09 | ST_MAN     |  7900.00 |           0.00 |        100 |            50 |
|         123 | Shanta      | Vollman     | SVOLLMAN | 650.123.4234       | 1987-07-10 | ST_MAN     |  6500.00 |           0.00 |        100 |            50 |
|         124 | Kevin       | Mourgos     | KMOURGOS | 650.123.5234       | 1987-07-11 | ST_MAN     |  5800.00 |           0.00 |        100 |            50 |
|         125 | Julia       | Nayer       | JNAYER   | 650.124.1214       | 1987-07-12 | ST_CLERK   |  3200.00 |           0.00 |        120 |            50 |
|         126 | Irene       | Mikkilineni | IMIKKILI | 650.124.1224       | 1987-07-13 | ST_CLERK   |  2700.00 |           0.00 |        120 |            50 |
|         127 | James       | Landry      | JLANDRY  | 650.124.1334       | 1987-07-14 | ST_CLERK   |  2400.00 |           0.00 |        120 |            50 |
|         128 | Steven      | Markle      | SMARKLE  | 650.124.1434       | 1987-07-15 | ST_CLERK   |  2200.00 |           0.00 |        120 |            50 |
|         129 | Laura       | Bissot      | LBISSOT  | 650.124.5234       | 1987-07-16 | ST_CLERK   |  3300.00 |           0.00 |        121 |            50 |
|         130 | Mozhe       | Atkinson    | MATKINSO | 650.124.6234       | 1987-07-17 | ST_CLERK   |  2800.00 |           0.00 |        121 |            50 |
|         131 | James       | Marlow      | JAMRLOW  | 650.124.7234       | 1987-07-18 | ST_CLERK   |  2500.00 |           0.00 |        121 |            50 |
|         132 | TJ          | Olson       | TJOLSON  | 650.124.8234       | 1987-07-19 | ST_CLERK   |  2100.00 |           0.00 |        121 |            50 |
|         133 | Jason       | Mallin      | JMALLIN  | 650.127.1934       | 1987-07-20 | ST_CLERK   |  3300.00 |           0.00 |        122 |            50 |
|         134 | Michael     | Rogers      | MROGERS  | 650.127.1834       | 1987-07-21 | ST_CLERK   |  2900.00 |           0.00 |        122 |            50 |
|         135 | Ki          | Gee         | KGEE     | 650.127.1734       | 1987-07-22 | ST_CLERK   |  2400.00 |           0.00 |        122 |            50 |
|         136 | Hazel       | Philtanker  | HPHILTAN | 650.127.1634       | 1987-07-23 | ST_CLERK   |  2200.00 |           0.00 |        122 |            50 |
|         137 | Renske      | Ladwig      | RLADWIG  | 650.121.1234       | 1987-07-24 | ST_CLERK   |  3600.00 |           0.00 |        123 |            50 |
|         138 | Stephen     | Stiles      | SSTILES  | 650.121.2034       | 1987-07-25 | ST_CLERK   |  3200.00 |           0.00 |        123 |            50 |
|         139 | John        | Seo         | JSEO     | 650.121.2019       | 1987-07-26 | ST_CLERK   |  2700.00 |           0.00 |        123 |            50 |
|         140 | Joshua      | Patel       | JPATEL   | 650.121.1834       | 1987-07-27 | ST_CLERK   |  2500.00 |           0.00 |        123 |            50 |
|         141 | Trenna      | Rajs        | TRAJS    | 650.121.8009       | 1987-07-28 | ST_CLERK   |  3500.00 |           0.00 |        124 |            50 |
|         142 | Curtis      | Davies      | CDAVIES  | 650.121.2994       | 1987-07-29 | ST_CLERK   |  3100.00 |           0.00 |        124 |            50 |
|         143 | Randall     | Matos       | RMATOS   | 650.121.2874       | 1987-07-30 | ST_CLERK   |  2600.00 |           0.00 |        124 |            50 |
|         144 | Peter       | Vargas      | PVARGAS  | 650.121.2004       | 1987-07-31 | ST_CLERK   |  2500.00 |           0.00 |        124 |            50 |
|         145 | John        | Russell     | JRUSSEL  | 011.44.1344.429268 | 1987-08-01 | SA_MAN     | 14000.00 |           0.40 |        100 |            80 |
|         146 | Karen       | Partners    | KPARTNER | 011.44.1344.467268 | 1987-08-02 | SA_MAN     | 13500.00 |           0.30 |        100 |            80 |
|         147 | Alberto     | Errazuriz   | AERRAZUR | 011.44.1344.429278 | 1987-08-03 | SA_MAN     | 12000.00 |           0.30 |        100 |            80 |
|         148 | Gerald      | Cambrault   | GCAMBRAU | 011.44.1344.619268 | 1987-08-04 | SA_MAN     | 11000.00 |           0.30 |        100 |            80 |
|         149 | Eleni       | Zlotkey     | EZLOTKEY | 011.44.1344.429018 | 1987-08-05 | SA_MAN     | 10500.00 |           0.20 |        100 |            80 |
|         150 | Peter       | Tucker      | PTUCKER  | 011.44.1344.129268 | 1987-08-06 | SA_REP     | 10000.00 |           0.30 |        145 |            80 |
|         151 | David       | Bernstein   | DBERNSTE | 011.44.1344.345268 | 1987-08-07 | SA_REP     |  9500.00 |           0.25 |        145 |            80 |
|         152 | Peter       | Hall        | PHALL    | 011.44.1344.478968 | 1987-08-08 | SA_REP     |  9000.00 |           0.25 |        145 |            80 |
|         153 | Christopher | Olsen       | COLSEN   | 011.44.1344.498718 | 1987-08-09 | SA_REP     |  8000.00 |           0.20 |        145 |            80 |
|         154 | Nanette     | Cambrault   | NCAMBRAU | 011.44.1344.987668 | 1987-08-10 | SA_REP     |  7500.00 |           0.20 |        145 |            80 |
|         155 | Oliver      | Tuvault     | OTUVAULT | 011.44.1344.486508 | 1987-08-11 | SA_REP     |  7000.00 |           0.15 |        145 |            80 |
|         156 | Janette     | King        | JKING    | 011.44.1345.429268 | 1987-08-12 | SA_REP     | 10000.00 |           0.35 |        146 |            80 |
|         157 | Patrick     | Sully       | PSULLY   | 011.44.1345.929268 | 1987-08-13 | SA_REP     |  9500.00 |           0.35 |        146 |            80 |
|         158 | Allan       | McEwen      | AMCEWEN  | 011.44.1345.829268 | 1987-08-14 | SA_REP     |  9000.00 |           0.35 |        146 |            80 |
|         159 | Lindsey     | Smith       | LSMITH   | 011.44.1345.729268 | 1987-08-15 | SA_REP     |  8000.00 |           0.30 |        146 |            80 |
|         160 | Louise      | Doran       | LDORAN   | 011.44.1345.629268 | 1987-08-16 | SA_REP     |  7500.00 |           0.30 |        146 |            80 |
|         161 | Sarath      | Sewall      | SSEWALL  | 011.44.1345.529268 | 1987-08-17 | SA_REP     |  7000.00 |           0.25 |        146 |            80 |
|         162 | Clara       | Vishney     | CVISHNEY | 011.44.1346.129268 | 1987-08-18 | SA_REP     | 10500.00 |           0.25 |        147 |            80 |
|         163 | Danielle    | Greene      | DGREENE  | 011.44.1346.229268 | 1987-08-19 | SA_REP     |  9500.00 |           0.15 |        147 |            80 |
|         164 | Mattea      | Marvins     | MMARVINS | 011.44.1346.329268 | 1987-08-20 | SA_REP     |  7200.00 |           0.10 |        147 |            80 |
|         165 | David       | Lee         | DLEE     | 011.44.1346.529268 | 1987-08-21 | SA_REP     |  6800.00 |           0.10 |        147 |            80 |
|         166 | Sundar      | Ande        | SANDE    | 011.44.1346.629268 | 1987-08-22 | SA_REP     |  6400.00 |           0.10 |        147 |            80 |
|         167 | Amit        | Banda       | ABANDA   | 011.44.1346.729268 | 1987-08-23 | SA_REP     |  6200.00 |           0.10 |        147 |            80 |
|         168 | Lisa        | Ozer        | LOZER    | 011.44.1343.929268 | 1987-08-24 | SA_REP     | 11500.00 |           0.25 |        148 |            80 |
|         169 | Harrison    | Bloom       | HBLOOM   | 011.44.1343.829268 | 1987-08-25 | SA_REP     | 10000.00 |           0.20 |        148 |            80 |
|         170 | Tayler      | Fox         | TFOX     | 011.44.1343.729268 | 1987-08-26 | SA_REP     |  9600.00 |           0.20 |        148 |            80 |
|         171 | William     | Smith       | WSMITH   | 011.44.1343.629268 | 1987-08-27 | SA_REP     |  7400.00 |           0.15 |        148 |            80 |
|         172 | Elizabeth   | Bates       | EBATES   | 011.44.1343.529268 | 1987-08-28 | SA_REP     |  7300.00 |           0.15 |        148 |            80 |
|         173 | Sundita     | Kumar       | SKUMAR   | 011.44.1343.329268 | 1987-08-29 | SA_REP     |  6100.00 |           0.10 |        148 |            80 |
|         174 | Ellen       | Abel        | EABEL    | 011.44.1644.429267 | 1987-08-30 | SA_REP     | 11000.00 |           0.30 |        149 |            80 |
|         175 | Alyssa      | Hutton      | AHUTTON  | 011.44.1644.429266 | 1987-08-31 | SA_REP     |  8800.00 |           0.25 |        149 |            80 |
|         176 | Jonathon    | Taylor      | JTAYLOR  | 011.44.1644.429265 | 1987-09-01 | SA_REP     |  8600.00 |           0.20 |        149 |            80 |
|         177 | Jack        | Livingston  | JLIVINGS | 011.44.1644.429264 | 1987-09-02 | SA_REP     |  8400.00 |           0.20 |        149 |            80 |
|         178 | Kimberely   | Grant       | KGRANT   | 011.44.1644.429263 | 1987-09-03 | SA_REP     |  7000.00 |           0.15 |        149 |             0 |
|         179 | Charles     | Johnson     | CJOHNSON | 011.44.1644.429262 | 1987-09-04 | SA_REP     |  6200.00 |           0.10 |        149 |            80 |
|         180 | Winston     | Taylor      | WTAYLOR  | 650.507.9876       | 1987-09-05 | SH_CLERK   |  3200.00 |           0.00 |        120 |            50 |
|         181 | Jean        | Fleaur      | JFLEAUR  | 650.507.9877       | 1987-09-06 | SH_CLERK   |  3100.00 |           0.00 |        120 |            50 |
|         182 | Martha      | Sullivan    | MSULLIVA | 650.507.9878       | 1987-09-07 | SH_CLERK   |  2500.00 |           0.00 |        120 |            50 |
|         183 | Girard      | Geoni       | GGEONI   | 650.507.9879       | 1987-09-08 | SH_CLERK   |  2800.00 |           0.00 |        120 |            50 |
|         184 | Nandita     | Sarchand    | NSARCHAN | 650.509.1876       | 1987-09-09 | SH_CLERK   |  4200.00 |           0.00 |        121 |            50 |
|         185 | Alexis      | Bull        | ABULL    | 650.509.2876       | 1987-09-10 | SH_CLERK   |  4100.00 |           0.00 |        121 |            50 |
|         186 | Julia       | Dellinger   | JDELLING | 650.509.3876       | 1987-09-11 | SH_CLERK   |  3400.00 |           0.00 |        121 |            50 |
|         187 | Anthony     | Cabrio      | ACABRIO  | 650.509.4876       | 1987-09-12 | SH_CLERK   |  3000.00 |           0.00 |        121 |            50 |
|         188 | Kelly       | Chung       | KCHUNG   | 650.505.1876       | 1987-09-13 | SH_CLERK   |  3800.00 |           0.00 |        122 |            50 |
|         189 | Jennifer    | Dilly       | JDILLY   | 650.505.2876       | 1987-09-14 | SH_CLERK   |  3600.00 |           0.00 |        122 |            50 |
|         190 | Timothy     | Gates       | TGATES   | 650.505.3876       | 1987-09-15 | SH_CLERK   |  2900.00 |           0.00 |        122 |            50 |
|         191 | Randall     | Perkins     | RPERKINS | 650.505.4876       | 1987-09-16 | SH_CLERK   |  2500.00 |           0.00 |        122 |            50 |
|         192 | Sarah       | Bell        | SBELL    | 650.501.1876       | 1987-09-17 | SH_CLERK   |  4000.00 |           0.00 |        123 |            50 |
|         193 | Britney     | Everett     | BEVERETT | 650.501.2876       | 1987-09-18 | SH_CLERK   |  3900.00 |           0.00 |        123 |            50 |
|         194 | Samuel      | McCain      | SMCCAIN  | 650.501.3876       | 1987-09-19 | SH_CLERK   |  3200.00 |           0.00 |        123 |            50 |
|         195 | Vance       | Jones       | VJONES   | 650.501.4876       | 1987-09-20 | SH_CLERK   |  2800.00 |           0.00 |        123 |            50 |
|         196 | Alana       | Walsh       | AWALSH   | 650.507.9811       | 1987-09-21 | SH_CLERK   |  3100.00 |           0.00 |        124 |            50 |
|         197 | Kevin       | Feeney      | KFEENEY  | 650.507.9822       | 1987-09-22 | SH_CLERK   |  3000.00 |           0.00 |        124 |            50 |
|         198 | Donald      | OConnell    | DOCONNEL | 650.507.9833       | 1987-09-23 | SH_CLERK   |  2600.00 |           0.00 |        124 |            50 |
|         199 | Douglas     | Grant       | DGRANT   | 650.507.9844       | 1987-09-24 | SH_CLERK   |  2600.00 |           0.00 |        124 |            50 |
|         200 | Jennifer    | Whalen      | JWHALEN  | 515.123.4444       | 1987-09-25 | AD_ASST    |  4400.00 |           0.00 |        101 |            10 |
|         201 | Michael     | Hartstein   | MHARTSTE | 515.123.5555       | 1987-09-26 | MK_MAN     | 13000.00 |           0.00 |        100 |            20 |
|         202 | Pat         | Fay         | PFAY     | 603.123.6666       | 1987-09-27 | MK_REP     |  6000.00 |           0.00 |        201 |            20 |
|         203 | Susan       | Mavris      | SMAVRIS  | 515.123.7777       | 1987-09-28 | HR_REP     |  6500.00 |           0.00 |        101 |            40 |
|         204 | Hermann     | Baer        | HBAER    | 515.123.8888       | 1987-09-29 | PR_REP     | 10000.00 |           0.00 |        101 |            70 |
|         205 | Shelley     | Higgins     | SHIGGINS | 515.123.8080       | 1987-09-30 | AC_MGR     | 12000.00 |           0.00 |        101 |           110 |
|         206 | William     | Gietz       | WGIETZ   | 515.123.8181       | 1987-10-01 | AC_ACCOUNT |  8300.00 |           0.00 |        205 |           110 |
+-------------+-------------+-------------+----------+--------------------+------------+------------+----------+----------------+------------+---------------+
```

###2.8.1 Change the email column of employees table with 'not available' for all employees
From the Movie table, write a SQL query to Rename UK to UNITED KINGDOM in the column movie 


```python
'''
UPDATE employees SET email='not available';
'''
```

###2.8.2 Change salary of employee to 8000 whose ID is 105, if the existing salary is less than 5000.
Write a SQL statement to change salary of employee to 8000 whose ID is 105, if the existing salary is less than 5000.


```python
'''
UPDATE employees SET SALARY = 8000 WHERE employee_id = 105 AND salary < 5000;
'''
```

###Q2.8.3 Change the email and commission_pct column of employees table with 'not available' and 0.10 for all employees
Write a SQL statement to change the email and commission_pct column of employees table with 'not available' and 0.10 for all employees.


```python
'''
UPDATE employees SET email='not available',
commission_pct=0.10;
'''
```

###Q2.8.4 Change the email column of employees table with 'not available' for all employees
Write a SQL statement to change the email and commission_pct column of employees table with 'not available' and 0.10 for those employees whose department_id is 110.


```python
'''
UPDATE employees 
SET email='not available',
commission_pct=0.10 
WHERE department_id=110;
'''
```

###Q2.8.5 Change the email column of employees table with 'not available' for employees of department_id is 80 and commission less than .20 percent
Write a SQL statement to change the email column of employees table with 'not available' for those employees whose department_id is 80 and gets a commission is less than .20%.


```python
'''
UPDATE employees 
SET email='not available'
WHERE department_id=80 AND commission_pct<.20;
'''
```

##2.9 Join

**Join Two or More Tables**

You can combine rows from two or more tables, based on a related column between them, by using a JOIN statement.

Consider you have a "users" table and a "products" table:
```
users
{ id: 1, name: 'John', fav: 154},
{ id: 2, name: 'Peter', fav: 154},
{ id: 3, name: 'Amy', fav: 155},
{ id: 4, name: 'Hannah', fav:},
{ id: 5, name: 'Michael', fav:}
products
{ id: 154, name: 'Chocolate Heaven' },
{ id: 155, name: 'Tasty Lemons' },
{ id: 156, name: 'Vanilla Dreams' }
```
These two tables can be combined by using users' fav field and products' id field.

Example
Join users and products to see the name of the users favorite product:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  INNER JOIN products ON users.fav = products.id"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
```
Result:
('John', 'Chocolate Heaven')
('Peter', 'Chocolate Heaven')
('Amy', 'Tasty Lemon')
```

Note: You can use JOIN instead of INNER JOIN. They will both give you the same result.

**LEFT JOIN**

In the example above, Hannah, and Michael were excluded from the result, that is because INNER JOIN only shows the records where there is a match.

If you want to show all users, even if they do not have a favorite product, use the LEFT JOIN statement:

Example
Select all users and their favorite product:

```
sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  LEFT JOIN products ON users.fav = products.id"
```
```
Result:
('John', 'Chocolate Heaven')
('Peter', 'Chocolate Heaven')
('Amy', 'Tasty Lemon')
('Hannah', None)
('Michael', None)
```

**RIGHT JOIN**

If you want to return all products, and the users who have them as their favorite, even if no user have them as their favorite, use the RIGHT JOIN statement:

Example
Select all products, and the user(s) who have them as their favorite:

```
sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  RIGHT JOIN products ON users.fav = products.id"
```

```
Result:
('John', 'Chocolate Heaven')
('Peter', 'Chocolate Heaven')
('Amy', 'Tasty Lemon')
('Hannah', None)
('Michael', None)
```

Note: Hannah and Michael, who have no favorite product, are not included in the result.



###Q2.9.1 Find the titles of all movies directed by James Cameron.
From the movie, movie_direction and director tables, write a SQL query to find the movies directed by 'James Cameron'. Return movie title. (Refer Section 2.11 for database)


```python
'''
SELECT mov_title FROM movie 
JOIN  movie_direction 
 ON movie.mov_id=movie_direction.mov_id
JOIN  director 
 ON movie_direction.dir_id=director.dir_id
WHERE dir_fname = 'James' AND dir_lname='Cameron';
'''
```

###Q2.9.2 Find the name of all reviewers who have rated their ratings with a NULL value
From the reviewer and rating tables, write a SQL query to find the name of all reviewers who have rated their ratings with a NULL value. Return reviewer name. (Refer Section 2.11 for database)


```python
'''
SELECT rev_name
FROM reviewer
INNER JOIN rating USING(rev_id)
WHERE rev_stars IS NULL;
'''
```

###Q2.9.3 Find the first and last names of all the actors who were cast in the movie 'Annie Hall', and the roles they played in that production
From the actor, movie_cast and movie tables, write a SQL query to find the actors who were cast in the movie 'Annie Hall'. Return actor first name, last name and role.(Refer Section 2.11 for database)


```python
'''
SELECT act_fname,act_lname,role
  FROM actor 
	  JOIN movie_cast ON actor.act_id=movie_cast.act_id
		JOIN movie ON movie_cast.mov_id=movie.mov_id 
		  AND movie.mov_title='Annie Hall';
'''
```

###Q2.9.4 Find the name of movie and director who directed a movie that casted a role for 'Eyes Wide Shut'
From the director, movie_direction, movie and movie_cast tables, write a SQL query to find the director who directed a movie that casted a role for 'Eyes Wide Shut'. Return director first name, last name and movie title.(Refer Section 2.11 for database)


```python
'''
SELECT dir_fname, dir_lname, mov_title
FROM  director 
JOIN movie_direction
JOIN movie
JOIN movie_cast
WHERE role IS  NOT NULL
AND mov_title = 'Eyes Wide Shut';
'''
```

###Q2.9.5 Find all the actors who have not acted in any movie between 1990 and 2000
From the actor, movie_cast and movie tables, write a SQL query to find the actors who have not acted in any movie between1990 and 2000 (Begin and end values are included.). Return actor first name, last name, movie title and release year. (Refer Section 2.11 for database)



```python
'''
SELECT act_fname, act_lname, mov_title, mov_year
FROM actor
JOIN movie_cast 
ON actor.act_id=movie_cast.act_id
JOIN movie 
ON movie_cast.mov_id=movie.mov_id
WHERE mov_year NOT BETWEEN 1990 and 2000;
'''
```

Better Way


```python
'''
SELECT a.act_fname, a.act_lname, c.mov_title, c.mov_year
FROM actor a, movie_cast b, movie c
WHERE a.act_id=b.act_id
AND b.mov_id=c.mov_id
AND c.mov_year NOT BETWEEN 1990 and 2000;
'''
```

##2.10 Delete Records and Drop Table

**Delete Record**

You can delete records from an existing table by using the "DELETE FROM" statement:

Example
Delete any record where the address is "Mountain 21":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DELETE FROM customers WHERE address = 'Mountain 21'"

mycursor.execute(sql)

mydb.commit()

print(mycursor.rowcount, "record(s) deleted")
```
```
Result:
1 record(s) deleted
```

**Important!: Notice the statement: mydb.commit(). It is required to make the changes, otherwise no changes are made to the table.**

Notice the WHERE clause in the DELETE syntax: The WHERE clause specifies which record(s) that should be deleted. If you omit the WHERE clause, all records will be deleted!


**Prevent SQL Injection**

It is considered a good practice to escape the values of any query, also in delete statements.

This is to prevent SQL injections, which is a common web hacking technique to destroy or misuse your database.

The mysql.connector module uses the placeholder %s to escape values in the delete statement:

Example
Escape values by using the placeholder %s method:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DELETE FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )

mycursor.execute(sql, adr)

mydb.commit()

print(mycursor.rowcount, "record(s) deleted")
```
```
Result:
1 record(s) deleted
```


###Q2.10.1 Delete all the movies which were released on or before 1958.
Write a SQL query to delete all the movies which were released on or before 1958.


```python
'''
Delete from movie where mov_year <= 1958;
'''
```

###Q2.10.2 Delete all the movies of director Alfred Hitchcock.
Write a SQL query to delte all the movies which were directed by Alfred Hithcock.


```python
'''
Delete from movie where mov_id in (Select mov_id from movie_direction md,director d 
where md.dir_id = d.dir_id and d.dir_fmane = 'Alfred' and d.last_name = 'Hithcock');
'''
```

###Q2.10.3 Delete actors with first name James
Write a SQL query to delte all the actors with first name James.


```python
'''
Delete from actor where act_fname = 'James';
'''
```

**Delete a Table**

You can delete an existing table by using the "DROP TABLE" statement:

Example
Delete the table "customers":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DROP TABLE customers"

mycursor.execute(sql)

```
```
#If this page was executed with no error(s), you have successfully deleted the "customers" table.
```

**Drop Only if Exist**

If the the table you want to delete is already deleted, or for any other reason does not exist, you can use the IF EXISTS keyword to avoid getting an error.

Example
Delete the table "customers" if it exists:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DROP TABLE IF EXISTS customers"

mycursor.execute(sql)
```
```
#If this page was executed with no error(s), you have successfully deleted the "customers" table.
```


###Q2.10.4. Drop the movie table.
Write a SQL query to drop the MOVIE table.


```python
'''
DROP TABLE MOVIE;
'''
```

###Q2.10.5. Drop the table movie_cast  if exist.
Write a SQL query to drop the movie_cast table, if the table exist.


```python
'''
DROP TABLE IF EXISTS MOVIE_CAST
'''
```

Q

##2.11 Movie Database
Refer to this database for all the exercises of Basic SQL.

**Movie Database**


![image.png](data:image/png;base64,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)

**Sample table: movie**

```
mov_id |                     mov_title                      | mov_year | mov_time |    mov_lang     | mov_dt_rel | mov_rel_country
--------+----------------------------------------------------+----------+----------+-----------------+------------+-----------------
    901 | Vertigo                                            |     1958 |      128 | English         | 1958-08-24 | UK
    902 | The Innocents                                      |     1961 |      100 | English         | 1962-02-19 | SW
    903 | Lawrence of Arabia                                 |     1962 |      216 | English         | 1962-12-11 | UK
    904 | The Deer Hunter                                    |     1978 |      183 | English         | 1979-03-08 | UK
    905 | Amadeus                                            |     1984 |      160 | English         | 1985-01-07 | UK
    906 | Blade Runner                                       |     1982 |      117 | English         | 1982-09-09 | UK
    907 | Eyes Wide Shut                                     |     1999 |      159 | English         |            | UK
    908 | The Usual Suspects                                 |     1995 |      106 | English         | 1995-08-25 | UK
    909 | Chinatown                                          |     1974 |      130 | English         | 1974-08-09 | UK
    910 | Boogie Nights                                      |     1997 |      155 | English         | 1998-02-16 | UK
    911 | Annie Hall                                         |     1977 |       93 | English         | 1977-04-20 | USA
    912 | Princess Mononoke                                  |     1997 |      134 | Japanese        | 2001-10-19 | UK
    913 | The Shawshank Redemption                           |     1994 |      142 | English         | 1995-02-17 | UK
    914 | American Beauty                                    |     1999 |      122 | English         |            | UK
    915 | Titanic                                            |     1997 |      194 | English         | 1998-01-23 | UK
    916 | Good Will Hunting                                  |     1997 |      126 | English         | 1998-06-03 | UK
    917 | Deliverance                                        |     1972 |      109 | English         | 1982-10-05 | UK
    918 | Trainspotting                                      |     1996 |       94 | English         | 1996-02-23 | UK
    919 | The Prestige                                       |     2006 |      130 | English         | 2006-11-10 | UK
    920 | Donnie Darko                                       |     2001 |      113 | English         |            | UK
    921 | Slumdog Millionaire                                |     2008 |      120 | English         | 2009-01-09 | UK
    922 | Aliens                                             |     1986 |      137 | English         | 1986-08-29 | UK
    923 | Beyond the Sea                                     |     2004 |      118 | English         | 2004-11-26 | UK
    924 | Avatar                                             |     2009 |      162 | English         | 2009-12-17 | UK
    926 | Seven Samurai                                      |     1954 |      207 | Japanese        | 1954-04-26 | JP
    927 | Spirited Away                                      |     2001 |      125 | Japanese        | 2003-09-12 | UK
    928 | Back to the Future                                 |     1985 |      116 | English         | 1985-12-04 | UK
    925 | Braveheart                                         |     1995 |      178 | English  
```

**Sample table: reviewer**

```
 rev_id |            rev_name
--------+--------------------------------
   9001 | Righty Sock
   9002 | Jack Malvern
   9003 | Flagrant Baronessa
   9004 | Alec Shaw
   9005 |
   9006 | Victor Woeltjen
   9007 | Simon Wright
   9008 | Neal Wruck
   9009 | Paul Monks
   9010 | Mike Salvati
   9011 |
   9012 | Wesley S. Walker
   9013 | Sasha Goldshtein
   9014 | Josh Cates
   9015 | Krug Stillo
   9016 | Scott LeBrun
   9017 | Hannah Steele
   9018 | Vincent Cadena
   9019 | Brandt Sponseller
   9020 | Richard Adams
```

**Sample table: rating**

 mov_id | rev_id | rev_stars | num_o_ratings
--------+--------+-----------+---------------
    901 |   9001 |      8.40 |        263575
    902 |   9002 |      7.90 |         20207
    903 |   9003 |      8.30 |        202778
    906 |   9005 |      8.20 |        484746
    924 |   9006 |      7.30 |
    908 |   9007 |      8.60 |        779489
    909 |   9008 |           |        227235
    910 |   9009 |      3.00 |        195961
    911 |   9010 |      8.10 |        203875
    912 |   9011 |      8.40 |
    914 |   9013 |      7.00 |        862618
    915 |   9001 |      7.70 |        830095
    916 |   9014 |      4.00 |        642132
    925 |   9015 |      7.70 |         81328
    918 |   9016 |           |        580301
    920 |   9017 |      8.10 |        609451
    921 |   9018 |      8.00 |        667758
    922 |   9019 |      8.40 |        511613
    923 |   9020 |      6.70 |         13091

**Sample table: actor**

```
 act_id |      act_fname       |      act_lname       | act_gender
--------+----------------------+----------------------+------------
    101 | James                | Stewart              | M
    102 | Deborah              | Kerr                 | F
    103 | Peter                | OToole               | M
    104 | Robert               | De Niro              | M
    105 | F. Murray            | Abraham              | M
    106 | Harrison             | Ford                 | M
    107 | Nicole               | Kidman               | F
    108 | Stephen              | Baldwin              | M
    109 | Jack                 | Nicholson            | M
    110 | Mark                 | Wahlberg             | M
    111 | Woody                | Allen                | M
    112 | Claire               | Danes                | F
    113 | Tim                  | Robbins              | M
    114 | Kevin                | Spacey               | M
    115 | Kate                 | Winslet              | F
    116 | Robin                | Williams             | M
    117 | Jon                  | Voight               | M
    118 | Ewan                 | McGregor             | M
    119 | Christian            | Bale                 | M
    120 | Maggie               | Gyllenhaal           | F
    121 | Dev                  | Patel                | M
    122 | Sigourney            | Weaver               | F
    123 | David                | Aston                | M
    124 | Ali                  | Astin                | F
```

**Sample table: movie_cast**

```
 act_id | mov_id |              role
--------+--------+--------------------------------
    101 |    901 | John Scottie Ferguson
    102 |    902 | Miss Giddens
    103 |    903 | T.E. Lawrence
    104 |    904 | Michael
    105 |    905 | Antonio Salieri
    106 |    906 | Rick Deckard
    107 |    907 | Alice Harford
    108 |    908 | McManus
    110 |    910 | Eddie Adams
    111 |    911 | Alvy Singer
    112 |    912 | San
    113 |    913 | Andy Dufresne
    114 |    914 | Lester Burnham
    115 |    915 | Rose DeWitt Bukater
    116 |    916 | Sean Maguire
    117 |    917 | Ed
    118 |    918 | Renton
    120 |    920 | Elizabeth Darko
    121 |    921 | Older Jamal
    122 |    922 | Ripley
    114 |    923 | Bobby Darin
    109 |    909 | J.J. Gittes
    119 |    919 | Alfred Borden
```

**Sample table: director**

```
 dir_id |      dir_fname       |      dir_lname
--------+----------------------+----------------------
    201 | Alfred               | Hitchcock
    202 | Jack                 | Clayton
    203 | David                | Lean
    204 | Michael              | Cimino
    205 | Milos                | Forman
    206 | Ridley               | Scott
    207 | Stanley              | Kubrick
    208 | Bryan                | Singer
    209 | Roman                | Polanski
    210 | Paul                 | Thomas Anderson
    211 | Woody                | Allen
    212 | Hayao                | Miyazaki
    213 | Frank                | Darabont
    214 | Sam                  | Mendes
    215 | James                | Cameron
    216 | Gus                  | Van Sant
    217 | John                 | Boorman
    218 | Danny                | Boyle
    219 | Christopher          | Nolan
    220 | Richard              | Kelly
    221 | Kevin                | Spacey
    222 | Andrei               | Tarkovsky
    223 | Peter                | Jackson
```

**Sample table: movie_direction**


```
Sample table: movie_direction
 dir_id | mov_id
--------+--------
    201 |    901
    202 |    902
    203 |    903
    204 |    904
    205 |    905
    206 |    906
    207 |    907
    208 |    908
    209 |    909
    210 |    910
    211 |    911
    212 |    912
    213 |    913
    214 |    914
    215 |    915
    216 |    916
    217 |    917
    218 |    918
    219 |    919
    220 |    920
    218 |    921
    215 |    922
    221 |    923
```



```python

```

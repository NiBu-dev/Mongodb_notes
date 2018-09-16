# Mongodb_notes
## Install mongo db on ubuntu

    $ sudo apt update
    $ sudo apt install -y mongodb

## Check the service status

    $ sudo systemctl status mongodb

## Start/Stop/Restart/enable/disable

    $ sudo systemctl start/stop/restart/enable/disable mongodb

# Enter mongodb shell:

    $ mongo

## Create database/ switch to a database

    > use students

## Show database informations

    > show collections 

or

    > show tables

or

    > db.getCollectionNames();

## Insert an element in database:

    > db.students.insert({name:'Jenny'});

## Insert multiple elements in a database

    > db.students.insertMany([{name:'Tom'}, {name:'Michael'}, {name:'Christine'}]);

# Update

Updates the entire object.

    > db.students.update({name:'Tom'}, {age:29, name:'Tom'});

    > db.students.updateOne({},{});//will update the first matching

    > db.students.updateMany({}, {});// will update all the matching documents
	
### Update a single field of a document

    > db.students.update({name:'Tom'}, {$set: {age:29}});

### Update multiple documents simultaneously 

    > db.students.update({name:'Tom'}, {$set: {age:29}},{multi: true});
or use updateOne or updateMany

### Replace the document

    > db.students.replaceOne({key:value}, {key:value});

# Delete

    > db.students.deleteMany({key:value});

    > db.students.remove({key:value});

    > db.students.deleteOne({key:value});

    > db.students.remove() and db.students.remove({}) will remove all documents from the collection

# Read

    > db.students.find({name:'Tom'});

    > db.students.findOne({name:'Tom'});\\finds one

    > db.people.find({name: 'Tom'}, {_id: 0, age: 1}); \\ will exclude docs with _id and include only the age field

    > db.students.find().pretty(); // displays the collection

# Update of Embedded documents

for this document:

    {name: 'Tom', age: 28, marks: [50, 60, 70]}
updates Tom's marks to55 where marks are 5
0
    db.people.update({name: "Tom", marks: 50}, {"$set": {"marks.$": 55}})

### Updates values in array

for the document:

    { "_id" : 1, "grades" : [ 80, 85, 90 ] }

    db.students.update({ _id: 1, grades: 80 },{ $set: { "grades.$" : 82 } }

    db.people.update({name: 'Tom'}, {$push: {nicknames: 'Tommy'}});
    // This adds the string 'Tommy' into the nicknames array in Tom's document.

    db.people.update({name: 'Tom'}, {$pull: {nicknames: 'Tommy'}});
    // This removes the string 'Tommy' from the nicknames array in Tom's document.         


# Quering for data

retrieve al elements in a collection

    > db.collection.find({});

retrieve documents in a collection using a condition ( similar to WHERE in MYSQL )

    > db.collection.find({key: value});

retrieve documents in a collection using Boolean conditions (Query Operators)

    > db.collection.find( {$and: [{ key: value }, { key: value }]}); //AND

    > db.collection.find( {$or: [{ key: value }, { key: value }]}); //OR

    > db.inventory.find( { key: { $not: value } } ); //NOT

### FindOne()

 the querying functionality is similar to find() but this will end execution the moment it finds one document matching
its condition , if used with and empty object , it will fetch the first document and return it.

To list the collection:

    > db.collection.find({});

To skip first 3 documents:

    > db.collection.find({}).skip(3);

To sort descending by the field name:

    > db.collection.find({}).sort({ "name" : -1});

To count the results:

    > db.collection.find({}).count();

### AND Queries

    > db.people.find({$and: [{"name":"Tom"}, {"age":{"$gte":25}}]});

### OR Queries

    > db.students.find({"$or": [{"firstName": "Prosen"}, {"age": {"$gte": 23}}]});

# Aggregation

Get the number of occurencies

    > db.collections.count({key:value});

or

    > db.collections.find({key:value}).length();

## SUM
calculate the sum for the specified objects data identifiers

$group - take in consideration the group stage

  >  db.students.aggregate([{$group:{_id:124,total:{$sum:'$balance'}}}]);

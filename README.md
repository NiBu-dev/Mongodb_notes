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

    > db.students.replaceOne({obj}, {obj});

# Delete

    > db.students.deleteMany({obj});

    > db.students.remove({obj});

    > db.students.deleteOne({obj});

    > db.students.remove() and db.students.remove({}) will remove all documents 
from the collection

# Read

    > db.students.find({name:'Tom'});

    > db.students.findOne({name:'Tom'});\\finds one

    > db.people.find({name: 'Tom'}, {_id: 0, age: 1}); \\ will exclude docs with _id and
 include only the age field

    > db.students.find().pretty(); // displays the collection

# Update of Embedded documents

   for this document:
    {name: 'Tom', age: 28, marks: [50, 60, 70]}
   updates Tom's marks to55 where marks are 50
     db.people.update({name: "Tom", marks: 50}, {"$set": {"marks.$": 55}})

### Updates values in array

   for the document:
    { "_id" : 1, "grades" : [ 80, 85, 90 ] }

    db.students.update({ _id: 1, grades: 80 },{ $set: { "grades.$" : 82 } }

    db.people.update({name: 'Tom'}, {$push: {nicknames: 'Tommy'}});
    // This adds the string 'Tommy' into the nicknames array in Tom's document.

    db.people.update({name: 'Tom'}, {$pull: {nicknames: 'Tommy'}});
    // This removes the string 'Tommy' from the nicknames array in Tom's document.         




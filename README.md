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




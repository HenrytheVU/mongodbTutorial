# mongodbTutorial

## Installation

Get mongoDB from https://www.mongodb.org/

On Windows-machine:
- Install the latest version for 'Windows 2008 R2+'
- Click through the setup menu -> 'Complete Installation'

On MacOS
Easiest way:
- Get Homebrew - a kickass package manager for OS X
- Go to www.brew.sh and check out the installation guide (very easy and quick)
- Or put this in the Terminal prompt: 
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
- After installing Homebrew just type this in the Terminal prompt: brew install mongodb

Otherwise:
- Download the installation file for your MacOS version
- Unpack to your selected path


## Run MongoDB server

Go to your installation path of MongoDB
Windows:
- Double click on mongod.exe or run at CMD

MacOS:
- Terminal:
```bash
mongod --dbpath data/db
```

## Run the MongoDB command shell interface

Windows:
- run mongo.exe

MacOS:
- run mongo.sh


## Import the bank_data.json

- Get the bank_data.json.zip in the bank_data folder on this repository
- Unzip
- Run within the mongodb/bin folder
```bash
mongoimport <path to bank_data.json> --jsonArray --collection bank_data
```

This will fill up your mongodb instance with 50000 bank account documents

## Now lets play with some simple queries

Go back to the mongo command line interface


```
# shows collections in database
show collections
```


The output of your command will look similar to:

```bash
> show collections
bank_data
system.indexes
```

To get the collection object, we can use the **db** reference to the current database.

```bash
db.bank_data
```
To see how many documents we loaded into the mongodb collection we can use the **count()** function on the collection object:

```bash
> db.bank_data.count()
50000
```

There's much more you can do with a collection. Checkout the collections help by doing:

```bash
db.bank_data.help()
```

To find one entity in the collection:

```bash
db.bank_data.findOne()
```
You can pass specified paramter to the query:

To find all accounts with last name "SMITH" -> just pass the json object to the query:

```json
{last_name : "SMITH"}
```

```bash
db.bank_data.find({last_name : "SMITH"})
```


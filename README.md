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
Make sure the data/db directory exists, depends on where you run the mongod prozess
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

```js
{last_name : "SMITH"}
```

```bash
db.bank_data.find({last_name : "SMITH"})
```

#### AND Queries

We can achieve an AND query by simply specifying another parameter:
	
```js
db.bank_data.find({last_name: "SMITH", first_name: "JAMES"})
```

#### OR Queries

OR queries are different because they require the **$or** operator


Say that we wanted to get any person whose last name is SMITH or MARTINEZ:

```js
db.bank_data.find({$or: [ { last_name: "MARTINEZ"}, {last_name: "SMITH"} ]})
```

Only show the first_name and last_name for a cleaner output:
```js
db.bank_data.find({$or: [ { last_name: "MARTINEZ"}, {last_name: "SMITH"} ]}, {first_name: 1, last_name: 1})
```

### Greater Than, Less Than, Not Equal To Operators

MongoDB also offers the following operators
**$gt** = greater than
**$lt** = less than
**$gte** = greater than or equal to
**$lte** = less than or equal to
**$ne** = not equal to

Here's an example for all the accounts with a acount_balance greater than 9000000 any currency :D
```js
db.bank_data.find({ 'accounts.account_balance': {$gt: 9000000} })
```
Ok 9000000 'money unit' doesn't really mean anything. If the account has 9 Millis YEN, it's peanuts ;) Let's say we want to see who has more than $9000000

```js
db.bank_data.find({ 'accounts.account_balance': {$gt: 9000000}, 'accounts.currency': 'USD' })
```

### Sorting

We can sort the output by using the **sort()** function

Say we want to sort all the JIMMY's by last_name:

```js
db.bank_data.find({first_name: "JIMMY"}, {first_name: 1, last_name: 1}).sort({last_name: 1 })
```
The 1 after last_name means by ascending order. For a descending order use -1
```js
{last_name: 1 }
```



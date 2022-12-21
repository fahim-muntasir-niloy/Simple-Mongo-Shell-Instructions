
# Simple Mongo Shell Instructions

In mongo shell run following for getting local database.
```js
Please enter a MongoDB connection string (Default: mongodb://localhost/): mongodb
```

This will reply with the localhost information
```js
Current Mongosh Log ID: 63a3543791742f7626d8b2be
Connecting to:          mongodb://127.0.0.1:27017/mongodb?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+1.6.0
Using MongoDB:          6.0.2
Using Mongosh:          1.6.0

For mongosh info see: https://docs.mongodb.com/mongodb-shell/
```

The `mongodb://127.0.0.1:27017/`  part is the link to local mongo server. it can be connected into compass for GUI application.

### Showing all database

```js
// command
mongodb> show dbs

//output shows all the databases in the server
admin           40.00 KiB
config          72.00 KiB
local           80.00 KiB
office          80.00 KiB
products        44.00 KiB
top_management  44.00 KiB

// the top 3 are built in db, below 3 were locally generated.
```

### Selecting a particular database
```js
// command
mongodb> use *dbname*

// if the given 'dbname' exists, shell shifts to that database.
// if no database exists, new database called 'dbname' is created and shell shifts to that

// command
mongodb> use products

// output
switched to db products


// A database can have any number of collections. We can search through them as well.

// command
products> use office
switched to db office

// viewing collections
office> show collections
office
top_management

// So office db had 2 collections.
```

### Insert data to database
```js
// insertOne() is used to insert a single data, insertMany() is used for array of data

// command
top_management> db.top_management.insertOne({"name":"maliha","position":"planner"})

// output
{
  acknowledged: true,
  insertedId: ObjectId("63a35ad0ee3123708fdc7a6e")
}

// This means data insertion was done correctly.
```


### View Data from database
```js
// To view all the data, find() is used.
// the generic convention is as followed:
	db.collectionName.find()

// command
	office> db.office.find()


// output
[
  {
    _id: ObjectId("63a32fd38d2806072e19a987"),
    name: 'niloy',
    position: 'Programmer'
  },
  {
    _id: ObjectId("63a330378d2806072e19a989"),
    name: 'Akib',
    position: 'manager'
  },
  {
    _id: ObjectId("63a330588d2806072e19a98a"),
    name: 'wasif',
    position: 'ceo'
  }
]

// we can use findOne({parameter}) to view only the first matching data. 
```

### Projection and Viewing
```js
// To view all the data matching a certain parameter, find({json param}) is used.

// The generic convention is as followed:
	db.collectionName.find({json parameter},{Projection Parameters})
	
// For Projection, the columns which needs to be included are assigned 1. Other columns are automatically given 0, so they are not shown.

// example
// without projection

	products> db.products.find({"Occassion":"Party"})

//output
[
  {
    _id: ObjectId("63a33bf71e110df033193711"),
    'Product ID': 8137,
    SKU: 'PCH-8705',
    Name: 'Once Upon A Time Lace Dress',
    'Product URL': 'https://www.domain.com/product/pch-8705',
    Price: 50,
    'Retail Price': 108,
    'Thumbnail URL': 'https://www.domain.com/images/pch-8705_600x600.png',
    'Search Keywords': 'lorem, ipsum, dolor, ...',
    Description: 'Sociosqu facilisis duis ...',
    Category: 'Dresses>Lace Dresses|Dresses>All Dresses|New Arrivals',
    'Category ID': '222|201|510',
    Brand: 'Oasis',
    'Child SKU': 'PCH-8705-WHT-SM|PCH-8705-WHT-MD|PCH-8705-WHT-LG|PCH-8705-BLK-SM|PCH-8705-BLK-MD|PCH-8705-BLK-LG|PCH-8705-LTBL-SM|PCH-8705-LTBL-MD|PCH-8705-LTBL-LG',
    'Child Price': '50|72|108',
    Color: 'White|Black|Light Blue',
    'Color Family': 'White|Black|Blue',
    'Color Swatches': '[{"color":"White", "family":"White", "swatch_hex":"#ffffff", "thumbnail":"/images/pch-8705-wht-sm_600x600.png", "price":50}, {"color":"Black", "family":"Black", "swatch_hex":"#000000", "thumbnail":"/images/pch-8705-blk-sm_600x600.png", "price":108}, {"color":"Light Blue", "family":"Blue", "swatch_img":"/swatches/light_blue.png", "thumbnail":"/images/pch-8705-ltbl-sm_600x600.png", "price":72}]',
    Size: 'Small|Medium|Large',
    'Shoe Size': '',
    'Pants Size': '',
    Occassion: 'Party',
    Season: '',
    Badges: '',
    'Rating Avg': 5,
    'Rating Count': 4,
    'Inventory Count': 0,
    'Date Created': '2019-02-15 20:33:28'
  },
  {
    _id: ObjectId("63a33bf71e110df033193712"),
    'Product ID': 10018,
    SKU: 'PGF-ESS',
    Name: 'Lovey Dovey Maxi Dress',
    'Product URL': 'https://www.domain.com/product/pgf-ess',
    Price: 68,
    'Retail Price': 68,
    'Thumbnail URL': 'https://www.domain.com/images/pgf-ess_600x600.png',
    'Search Keywords': 'lorem, ipsum, dolor, ...',
    Description: 'Sociosqu facilisis duis ...',
    Category: 'Dresses>Maxi Dresses|Dresses>All Dresses|New Arrivals',
    'Category ID': '223|201|510',
    Brand: 'Oasis',
    'Child SKU': 'PGF-ESS-FUOR-SM|PGF-ESS-FUOR-MD|PGF-ESS-FUOR-LG|PGF-ESS-PRPT-SM|PGF-ESS-PRPT-MD|PGF-ESS-PRPT-LG',
    'Child Price': '',
    Color: 'Fuschia Orange|Perfect Petals|Island Time',
    'Color Family': 'Orange|Pink|Yellow|Multi',
    'Color Swatches': '[{"color":"Fuschia Orange", "family":["Orange","Pink"], "swatch_img":"/swatches/fuschia_orange.png", "thumbnail":"/images/pgf-ess-fuor-sm_600x600.png", "price":68}, {"color":"Perfect Petals", "family":"Pink", "swatch_img":"/swatches/perfect_petals.png", "thumbnail":"/images/pgf-ess-prpt-sm_600x600.png", "price":68}, {"color":"Island Time", "family":["Yellow","Orange","Multi"], "swatch_img":"/swatches/island_time.png", "thumbnail":"/images/pgf-ess-istm-sm_600x600.png", "price":68}]',
    Size: 'Small|Medium|Large',
    'Shoe Size': '',
    'Pants Size': '',
    Occassion: 'Party',
    Season: '',
    Badges: '',
    'Rating Avg': 4.8,
    'Rating Count': 12,
    'Inventory Count': 24,
    'Date Created': '2019-02-20 21:38:02'
  }
]

// So each of the data have many columns. As we dont need all of them to be shown, projection can help us.
// with projection
	products> db.products.find({"Occassion":"Party"},{_id:0,Name:1,Price:1,Category:1,Occassion:1})

//output
[
  {
    Name: 'Once Upon A Time Lace Dress',
    Price: 50,
    Category: 'Dresses>Lace Dresses|Dresses>All Dresses|New Arrivals',
    Occassion: 'Party'
  },
  {
    Name: 'Lovey Dovey Maxi Dress',
    Price: 68,
    Category: 'Dresses>Maxi Dresses|Dresses>All Dresses|New Arrivals',
    Occassion: 'Party'
  }
]
```

### Delete Database
In our database, we accidentally created `top_management` collection in office. So, we should delete that. To do so, drop() command is used. 
```js
// generic convention
db.collectionName.drop()

// command
	office> db.top_management.drop()
// output
	true

// This means the collection was deleted. To check this:

	// command
	office> show collections
	//output
	office

// top_management collection was dropped successfully.
```

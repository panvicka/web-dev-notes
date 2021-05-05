## Mongo DB Crashcourse

- following `Mongo DB Crash Course` by `Traversy Media`
- NoSQL, Not Only SQL
- SQL are data in tables
- noSQL are data in collections, looks like JS object 
- BSON (binary JSON) -> binary encoding of JSON-like documents 
- scalable, scales horizontally (cheap machines can be added to increase size), fast, flexible
```
show dbs
use test
show collections
db.dropDatabase()
db.createCollection()
upsert:true -> when updating, if the thing doesn't exist, please create it 
$set -> operator if we want to update a field without overwriting other stuff 
$inc -> increase operator 
$rename -> to rename fields

```
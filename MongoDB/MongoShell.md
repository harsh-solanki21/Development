# MongoDB Command Reference

| Command                                                                         | Description                                       |
| ------------------------------------------------------------------------------- | ------------------------------------------------- |
| `mongosh`                                                                       | Enter MongoDB shell                               |
| `exit`                                                                          | Exit MongoDB shell and return to cmd              |
| `cls`                                                                           | Clear screen                                      |
| `show dbs`                                                                      | Display all databases                             |
| `db`                                                                            | Show current database                             |
| `use database_name`                                                             | Switch to or create a database                    |
| `show collections`                                                              | Display all collections in the current database   |
| `db.dropDatabase()`                                                             | Delete the current database                       |
|                                                                                 |                                                   |
| `db.collection.insertOne({...})`                                                | Insert one document into a collection             |
| `db.collection.insertMany([{...}, {...}])`                                      | Insert multiple documents into a collection       |
|                                                                                 |                                                   |
| `db.collection.find()`                                                          | Display all documents in a collection             |
| `db.collection.find().limit(n)`                                                 | Limit the number of results displayed             |
| `db.collection.find().sort({field: 1})`                                         | Sort results (1 for ascending, -1 for descending) |
| `db.collection.find({condition})`                                               | Find documents matching a condition               |
| `db.collection.find({}, {field1: 1, field2: 1})`                                | Project specific fields in results                |
| `db.collection.find().count()`                                                  | Count documents in a collection                   |
| `db.collection.find({condition: {$gt: value}})`                                 | Greater than query                                |
| `db.collection.find({condition: {$lt: value}})`                                 | Less than query                                   |
| `db.collection.find({$or: [{cond1}, {cond2}]})`                                 | OR query                                          |
| `db.collection.find({field: {$in: [val1, val2]}})`                              | Match any of the values in an array               |
| `db.collection.find({field: {$nin: [val1, val2]}})`                             | Not match any of the values in an array           |
| `db.collection.find({array: element})`                                          | Find documents with a specific array element      |
| `db.collection.find({array: [element]})`                                        | Find documents with an exact array match          |
| `db.collection.find({array: {$all: [el1, el2]}})`                               | Find documents containing all specified elements  |
| `db.collection.find({'nestedObj.field': value})`                                | Query nested objects                              |
|                                                                                 |                                                   |
| `db.collection.updateOne({condition}, {$inc: {field: value}})`                  | Increment a field's value                         |
| `db.collection.updateOne({condition}, {$pull: {array: value}})`                 | Remove an element from an array                   |
| `db.collection.updateOne({condition}, {$push: {array: value}})`                 | Add an element to an array                        |
| `db.collection.updateOne({condition}, {$push: {array: {$each: [val1, val2]}}})` | Add multiple elements to an array                 |
|                                                                                 |                                                   |
| `db.collection.find({field: new RegExp(pattern)})`                              | Use regex in queries                              |
| `db.collection.find({field: new RegExp(pattern, 'i')})`                         | Case-insensitive regex query                      |
| `db.members.find(name: new RegExp('^' + search + '$'))`                         | For exact search, case sensitive                  |
| `db.members.find(name: new RegExp('^' + search + '$', 'i'))`                    | For exact search, case insensitive                |

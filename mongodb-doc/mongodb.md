# mongodb常用命令
#### linux 安装
```bash
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-i686-3.2.7.tgz
tar -zxvf mongodb-linux-86_64-amazon-3.2.7.tgz
mv mongodb-linux-x86_64-3.2.7 /usr/local/mongodb
export PATH=/usr/local/mongodb/bin:$PATH
sudo mkdir -p /data/db
mongod
```

#### windows添加到环境变量
> 电脑 属性 高级系统设置 高级 环境变量 系统变量 path 编辑 添加 ;C:\Program Files\MongoDB\Server\3.2\bin\

#### mongo shell
```bash
mongo
show dbs	#显示数据库
use test	#使用test数据库
db.dropDatabase()	#删除数据库
db.collection.drop()	#删除集合
```

#### Create Operations
```bash
db.collection.insert()
db.collection.insertOne() #new 3.2
db.collection.insertMany() #new 3.2
db.collection.insert({name: "sue", age: 26, status: "A"})
db.collection.insertMany([{name: "sue"}, {name: "suee"}])
```

#### Read Operations
```bash
db.collection.find()
db.collection.findOne()
db.collection.find({age: {$gt: 18}}, {name: 1, address: 1}).limit(5)
```

#### Update Operations
```bash
db.collection.update()
db.collection.updateOne() #new 3.2
db.collection.updateMany() #new 3.2
db.collection.replaceOne() #new 3.2
db.collection.update({age: {$gt: 18}}, {$set: {status: "A"}}, {multi: true})
db.collection.findOneAndReplace()
db.collection.findOneAndUpdate()
db.collection.save()
db.collection.buldWrite()
```

#### Delete Operations
```bash
db.collection.remove()
db.collection.deleteOne() #new 3.2
db.collection.deleteMany() #new 3.2
db.collection.remove({status: "D"})
db.collection.findOneAndDelete()
db.collection.findOneAndModify()
db.collection.bulkWrite()
```

```bash
db.users.count()
db.users.find().count()
db.users.count({user_id: {$exists: true}})
db.users.distinct("status") #返回不重复值[]
db.users.find().limit(5).skip(10)
```

```bash
# Comparison Query Operators
$eq, $gt, $gte, $lt, $lte, $ne, $in, $nin

#Logical Query Operators
$or, $and, $not, $nor

#Element Query Operators
$exists
$type

#Evaluation Query Operators
$mod, $regex, $text, $where

#Geospatial Query Operators
$geoWithin, $geoIntersects, $near, $nearSphere
$geometry, $inDistance, $maxDistance, $center, $centerSphere, $box, $polygon, $uniqueDocs

#Query Operator Array
$all, $elemMatch, $size

#Bitwise Query Operators
$bitsAllSet, $bitsAnySet, $bitsAllClear, $bitAnyClear

#Projection Operators
$, $elementMatch, $meta, $slice

#Field Update Operators
$inc, $mul, $rename, $serOnInsert, $set, $unset, $min, $max, $currentDate

#Array Update Operators
$, $addToSet, $pop, $pullAll, $pull, $pushAll, $push, $each, $slice, $sort, $position

#Bitwise Update Operato
$bit

#Isolation Update Operator
$isolated
```

# node-mongodb-native
```javascript
var MongoClient = require('mongodb').MongoClient
var url = 'mongodb://localhost:27017/myproject'
MongoClient.connect(url, function(err, db) {
  db.collection('users').find({a:1}).skip(1).limit(2).sort([['a', 1]]).toArray(function(err, docs){})
  db.collection('users').insertOne({a:1}, function(err, r){})
  db.collection('users').insertMany([{a:1}, {a:3}], function(err, r){})
  db.collection('users').updateOne({a:1}, {$set:{b:1}}, function(err, r){})
  db.collection('users').updateMany({a:2}, {$set:{b:1}}, function(err, r){})
  db.collection('users').deleteOne({a:1}, function(err,r){})
  db.collcetion('users').deleteMany({a:2}, function(err, r){})
  db.collections('users').findOneAndUpdate({a:1}, {$set:{b:1}}, function(err,r){})
  db.collections('users').findOneAndDelete({a:1}, function(err,r){})

  db.close()
})

//es6 connecting
var MongoClient = require('mongodb').MongoClient,
  co = require('co')
co(function*() {
  var url = 'mongodb://localhost:27017/myproject'
  var db = yield MongoClient.connect(url)
  //
  db.close();
}).catch(function(err) {
  console.log(err.stack)
})

})
```

# mongoose
```javascript
var mongoose = require('mongoose')
mongoose.Promise = global.Promise
mongoose.connect(dbURL)
  .then(() => console.log('mongoose connection successful'))
  .catch((error) => console.error(error))
```
### mongoose Model methods
```javascript
var tankSchema = new mongoose.Schema({
  name: String,
  size: String
})
// Schema Types
String Number Date Buffer Boolean Mixed ObjectId Array
// Instace methods
tankSchema.methods.speak = function () {}
// Static methods
tankSchema.statics.getFive = function () {}

var Tank = mongoose.model('Tank', tankSchema)


var small = new Tank({size: 'bbb'})
small.save(function (err) {
  if (err) return console.error(err)
  // saved!
})

Model.create(doc, [callback(error, doc)])
Model.find(query, [fields], [options], [callback(error, docs)])
Model.update(query, update, [options], [callbcak(error, affectedCount, raw)])
Model.remove(query, [callback(error)])

Model.populate(docs, options, [callbcak(error, doc)])

Model.findOne(query, [fields], [options], [callback(error, doc)])
Model.findOndeAndUpdate(query, update, [options], [callback(error, doc)])
Model.findOndeAndRemove(query, [options], [callback(error, doc)])

Model.findById(id, [fields], [options], [callback(error, doc)])
Model.findByIdAndUpdate(id, update, [options], [callback(error, doc)])
Model.findByIdAndRemove(id, [options], [callback(error, doc)])

Model.find(query).limit(10).exec(callback)
```

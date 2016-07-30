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
  //
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

//Insert Documents
var MongoClient = require('mongodb').MongoClient
 , assert = require('assert')

var url = 'mongodb://localhost:27017/myproject'
MongoClient.connect(url, function(err, db) {
  assert.equal(null, err)
  console.log("Connected correctly to server")
  
  // Insert document
  db.collection('users').insertOne({a:1}, function(err, r) {
    assert.equal(null, err)
    assert.equal(1, r.insertedCount)
    db.close()
  })
  db.collection('users').insertMany([{a:2}, {a:3}], function(err, r) {
    assert.equal(null, err)
    assert.equal(2, r.insertedCount)
    db.close()
  })
  
  // Update documents
  db.collection('users').updateOne({a:1}, {$set: {b: 1}}, function(err, r) {
    assert.equal(null, err)
    assert.equal(1, r.matchedCount)
    assert.equal(1, r.modifiedCount)
  })
  db.collection('users').updateOne({a:3}, {$set: {b: 1}}, {
      upsert: true
    }, function(err, r) {
      assert.equal(null, err);
      assert.equal(0, r.matchedCount);
      assert.equal(1, r.upsertedCount);
      db.close()
    }
  )
  
  //Removing Documents
  db.collection('users').deleteOne({a:1}, function(err, r) {
    assert.equal(null, err)
    assert.equal(1, r.deletedCount)
  })
  
  db.collection('users').findOneAndUpdate({a:1}, {$set: {b: 1}},
    {
      returnOriginal: false,
      sort: [[a,1]],
      upsert: true
    }, function(err, r) {
      assert.equal(null, err);
      assert.equal(1, r.value.b);
    }
  )
  
  //Read Documents
  db.collection('users').find({a:1}).limit(2).toArray(function(err, docs) {
    assert.equal(null, err)
    assert.equal(2, docs.length)
    db.close()
  })
  
})
```
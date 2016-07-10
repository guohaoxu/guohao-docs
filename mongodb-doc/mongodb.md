# mongodb常用命令
### linux 安装
> curl -O https://fastdl.mongodb.org/linux/mongodb-linux-i686-3.2.7.tgz
> tar -zxvf mongodb-linux-86_64-amazon-3.2.7.tgz
> mv mongodb-linux-x86_64-3.2.7 /usr/local/mongodb
> export PATH=/usr/local/mongodb/bin:$PATH
> sudo mkdir -p /data/db
> mongod

### windows添加到环境变量
> 电脑 属性 高级系统设置 高级 环境变量 系统变量 path 编辑 添加 ;C:\Program Files\MongoDB\Server\3.2\bin\

### mongo shell
> mongo
> show dbs	*显示数据库*
> use test	*使用test数据库*
> db.dropDatabase	*删除数据库*
> db.collection.drop()	*删除集合*

### MongoDB CRUD Operations

#### Create Operations
> db.collection.insert()
> db.collection.insertOne()
> db.collection.insertMany()
> db.users.insert({name: "sue", age: 26, status: "A"})
> db.users.insertMany([{name: "sue", age: 26, status: "A"}, {name: "suee", age: 28, status: "B"}])

#### Read Operations
> db.collection.find()
> db.collection.findOne()
> db.users.find({age: {$gt: 18}}, {name: 1, address: 1}).limit(5)

#### Update Operations
> db.collection.update()
> db.collection.updateOne()
> db.collection.updateMany()
> db.collection.replaceOne()
> db.users.update({age: {$gt: 18}}, {$set: {status: "A"}}, {multi: true})

#### Delete Operations
> db.collection.remove()
> db.collection.deleteOne()
> db.collection.deleteMany()
> db.collection.remove({status: "D"})
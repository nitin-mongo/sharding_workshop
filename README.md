# sharding_workshop

**Step : 1 Create 2 shard M30 Cluster on MongoDB Atlas **
 - Make sure mongo shell is installed on the local m/c
 
 - Create User and whitelist your IP to connect to Atlas
 
 - try to connect to MongoDB cluster from local m/c
 
      mongosh "mongodb+srv://DNS" --username <username>
      Password : 
 
 ******** While this is getting created Lets recap the concepts of sharding **************
 
 - What is sharding
 
 - MongoDB sharding Architecture
 
 - When to Shard
 
**Step 2 : Verify sharding status **
 
 connect to mongodb shell and run below commands :
 
  -  sh.status()
 
  -  db.adminCommand( { listDatabases : 1 } )
 
 Step 3 : Load sample dataset from Atlas and repeat step 2
 
 - Discussion on observations
 
 - is cluster balanced ? How did we idenfy it ? what can be done incase not balanced ?
 
 Step 4 :  Make cluster balanced using movePrimary command
 
 - db.adminCommand( { movePrimary: <databaseName>, to: <newPrimaryShard> } )
 
  - db.adminCommand( { movePrimary : "sample_weatherdata", to : "atlas-8yjvx3-shard-0" } ) (example)
 
 --> What actually happens when we run movePrimary a
 
 This is OK for current data balancing but how do we make sure this does not happen in future 
 
 - sh.enableSharding( <database>, <primary shard> )
 
   - sh.enableSharding( "test","atlas-8yjvx3-shard-0") - While creating the database
 
 Step 5 : Lets discuss types of sharding in MongoDB
  - Hashed Sharding
 
  - Range Hsarding
 
  - Zone Sharding
 
 Step 6 : Choosing Shard Key - Properties of Good Shard Key
 
 Step 7 : Now we will showcase how MongoDB can distribute the data automatically by sharding collections
 
 =============================
 
 Data Needed to be loaded for Sharding
 
 Download compass importable json file or mongorestore dump file

https://drive.google.com/file/d/1zoziIc0J4M_TxjnxVIU2UdYjHjzIWT-S/view?usp=drive_link

./mongorestore --uri mongodb+srv://user:passwd@shardtest.pyuze.mongodb.net /path/dump/shard/products.bson
 
 ===============================
 
 
 ** Hash shardng **

Verify : sh.status()
 
db.adminCommand( { listDatabases : 1 } )
 
db.products.getShardDistribution()

 Shard Database :

sh.enableSharding("shard")

Shard Collection : 
 
Use shard
 
db.products.createIndex({"sku": "hashed"})

sh.shardCollection("shard.products", { "sku":"hashed" })


- Load Data After enabling sharding – Equal
 
- Load Data Before enabling sharding ( add more data) – Equal with bigger chunks
 
- Reduce chunk size and load data again – Lots of chunk
 
Use config
 
db.settings.updateOne(
   { _id: "chunksize" },
   { $set: { _id: "chunksize", value: 2 } },
   { upsert: true }
)
 
 ** Range Sharding **

Load Data to the cluster : Products.json (  either through compass or via mongorestore)

Verify : sh.status()
db.adminCommand( { listCollections : 1 } )


Shard Database :

sh.enableSharding("shard")

Shard Collection : Talk about choosing shard key

sh.shardCollection("shard.products", { "sku":1 })
 
Step 8 :
 
 Jumbo Chunk

sh.enableSharding(“shard”)
 
sh.shardCollection("shard.example", {"last_name" : 1, "first_name": 1 } )
 
Use shard
 
for ( i = 0; i<=100; i++) { db.example.insertOne({ last_name : "Cross", first_name : "Will"})}


All in one shard :

db.example.getShardDistribution()

sh.splitAt("m312.example", { last_name : "E", first_name : "Minkey" }) – Now distribution is equal

 
 Step 9 : Querying Data in sharded Clusters
 
  - Scatter- Gather Queries Vs Targeted Queries

                    db.products.find({"type" : "movie"}).explain()
                    db.products.find({"sku" : 28792188}).explain() 

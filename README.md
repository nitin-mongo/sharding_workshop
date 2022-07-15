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
  - db.adminCommand( { movePrimary : "test", to : "shard0001" } ) (example)
 
 --> What actually happens when we run movePrimary a
 
 This is OK for current data balancing but how do we make sure this does not happen in future 
 
 - sh.enableSharding( <database>, <primary shard> )
   - sh.enableSharding( test, shard0001 ) - While creating the database
 
 Step 5 : Lets discuss types of sharding in MongoDB
  - Hashed Sharding
  - Range Hsarding
  - Zone Sharding
 
 Step 6 : Choosing Shard Key
 
 Step 7 : Now we will showcase how MongoDB can distribute the data automatically by sharding collections
 
 ** Hash shardng **
 - Create sharded database 
 - shard collection with shard key(Hashed)
 - insert sample data
 - Verify Data Distribution 
 
 Discuss Challenges with Hash Shard Key
 
 ** Range SHarding **
  - Create sharded database 
  - shard collection with shard key(Hashed)
  - insert sample data
  - Verify Data Distribution 
 
 Step 8 : Querying Data in sharded Clusters
 
  - Scatter- Gather Queries Vs Targeted Queries
 
 Step 9 : Performance Tips for sharded Clusters

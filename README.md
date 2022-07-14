# sharding_workshop

**Step : 1 Create 2 shard M30 Cluster on MongoDB Atlas **
 - Make sure mongo shell is installed on the loacal m/c
 - try to connect to MongoDB cluster from local m/c
      mongosh "mongodb+srv://shardtest.pyuze.mongodb.net/myFirstDatabase" --username <username>
      Password : 
 
**Step 2 : Verify sharding status **
 
 connect to mongodb shell and run below commands :
  -  sh.status()
  -  db.adminCommand( { listDatabases : 1 } )

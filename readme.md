## How to Deploy your WebAPP with a MongoDB
---

[MongoDB-Atlas](https://www.mongodb.com/cloud/atlas)

1.  We currently have been accessing our localhost via
    - http://localhost:3000 
2.  We were interacting with the DB by conecting to 
    - mongodb://localhost:27017

- This is great for local development but if we want users to interact with our applications we need to get these files hosted. 
- Previously we used Heroku to host our app but this will not let the app interact with our local DB. 
- MongoDB Atlas allows us to host our server DB like Heroku does our webapp. Allowing our Application to perform CRUD operations. 


### Setting Up your FREE Cluster
---

1. Signup for a free account at MongoDB Cloud Atlas
2. Create a free Cluster
3. Select > AWS > N Virginia (free)
4. Cluster Tier > M0 Free Tier
5. This allows us to not have to enter payment details and not have to worry about a surprise bill. 
6. Create a user profile form the database access Security area (admin-mike)
7. IP Whitelist 0.0.0.0/0 from your network access Security area


### Connecting your FREE Cluster from the SHELL
---

1. Click Connect from the Clusters Panel on the Cluster we want to use.
2. Connect with the mongo shell
3. Install the Shell if you don't already have it installed.
4. Use this connection string in your application:
mongo "mongodb+srv://mycluster1.ewevp.mongodb.net/myFirstDatabase" --username admin-mike
5. Enter Password
6. Shell should show us connected now.
7. We are connected so we don't need to type mongod like we did before during local testing
8. show dbs to confirm were connected.


### Creating a Document from the cloud interface
---

1. From the atlas>clusters page click on collections.
2. Create a test collection
3. insert a document
4. go back to mongo shell> show dbs> use test > show collections 
5. db.test.find() // to confirm our entry is in the test db test collection.


### Connecting your FREE Cluster from the Application
---

1. Previously we had to type mongod to start the mongodb server then we had to run nodemon app.js to run our Application
2. To swap out our local DB we first want to shut down our local server by control+c if its running, if you rs from terminal running nodemon you will get a ton of errors as we just shut down the server.
3. Go back to the Atlas cloud dashboard and click connect again on our cluster. Click on Connect your Application
4. Driver node.js Version 3.6 or later
5. Copy th SRV address: mongodb+srv://<username>:<password>@mycluster1.ewevp.mongodb.net/myFirstDatabase?retryWrites=true&w=majority

```
mongoose.connect("mongodb+srv://admin-mike:<password>@mycluster1.ewevp.mongodb.net/todolistDB", {useNewUrlParser: true, useUnifiedTopology: true })
```

6. Remove myFirstDatabase?retryWrites=true&w=majority from the url
7. Run nodemon app.js again and you should be able to connect.
8. go to localhost:3000 and add an item
9. Now we can go to the cloud and confirm that the DB Item we added is in the new collection.

### Deploying an APP with a DATABASE to a collection
---
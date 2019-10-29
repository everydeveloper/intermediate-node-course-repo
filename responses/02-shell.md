You got it! Mongoose models come with a lot of useful methods (such as create) that make it easy to query for user documents in our user collection.

You can use the [mongo shell](https://docs.mongodb.com/manual/mongo/) to visualize your database and manipulate it through the command line. Before setting up our express routes with mongoose, try doing the following mongo shell commands:

1. Open a new console and type in the `mongo` command. 
2. Select our database: `use userData`
3. Insert a new user into a users collection:`db.users.insertOne({name:"octocat",email:"octo@cat.com",password:"password"})` 
4. Find all users: `db.users.find()`
5. Delete all users: `db.users.drop()`

This is a good place for a commit. If a user was successfully saved to the database, **push your code to GitHub** to continue:

```console
git add .
git commit -m"add user model and connect to db"
git push origin master
```
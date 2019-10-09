Correct! In this case, emails need to be unique. It makes sense to have at least one unique value, to avoid errors with authentication later on.

Let's start using this model to create some users. Go to your server.js file and add this line after all the libraries are imported.

```javascript
const User=require('./models/User');
mongoose.connect('mongodb://localhost/userData')
```

The first line is going to import the User model we just made, and the second is going to connect us to a local mongoDB database called: *userData*. If this does not exist yet, it will create it for you. Make sure you use different database names if you work on other projects. 

In the server.js file, you will notice some place-holder routes for the '/users' endpoint. It should look like this:

```javascript

app.route('/users')
.post((req,res)=>{
  // code goes here
})
.get((req,res)=>{
  // code goes here
})
.put((req,res)=>{
  // code goes here
})
.delete((req,res)=>{
  // code goes here
})

```
We are using route chaining here as a shorthand. All of these routes will use the '/users' endpoint. Insert this in the post route so it looks like this:

```javascript
.post((req,res)=>{
  User.create(
    {
      name:req.body.user.name,
      email:req.body.user.email,
      password:req.body.user.password
    },
    (err,data)=>{
    if (err){
      res.json({success: false,message: err})
    } else if (!data){
      res.json({success: false,message: "Not Found"})
    } else {
      res.json({success: true,data: data})
    }
  })
})
```
When you want to make a new *document* in MongoDB, you can simply call the "create" method on your mongoose model. Its first argument is an object containing the values for the new document. The next argument is a callback function, which handles the response from the database.

In the function above, what does *User* represent?

a. A MongoDB document
b. A MongoDB collection
c. A Mongoose Model
d. Data sent in the request body

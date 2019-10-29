Correct! In this case, emails need to be unique. It makes sense to have at least one unique value, to avoid errors with authentication later on.


Here we are using route chaining as a shorthand for the "get", "put", and "delete" routes, since they all use the '/users/:id' endpoint. Remember that in 'users/:id' endpoint, id is a variable which can be accessed in the "req.params".

Now that we have a model, let's import it and connect to our database. Go to your server.js file and add these lines after all the libraries are imported.

```javascript
const User=require('./models/User');
mongoose.connect('mongodb://localhost/userData')
```

The first line makes our User model available to use in express routes. The second line connects us to a local mongoDB database called: *userData*. 

In the server.js file, you will notice some *express* routes set up for our users. It should look like this:

```javascript
// CREATE
app.post('/users',(req,res)=>{
  // User.create()
})

app.route('/users/:id')
// READ
.get((req,res)=>{
  // User.findById()
})
// UPDATE
.put((req,res)=>{
  // User.findByIdAndUpdate()
})
// DELETE
.delete((req,res)=>{
  // User.findByIdAndDelete()
})
```

Inside each (req,res) callback function we use mongoose methods on our User model to Create, Read, Update, and Delete individual *user documents* in our *users collection*. The "POST" route is different than the others because mongoDB automatically creates an ID for each document when it is created. We are using route chaining as a shorthand for the "GET", "PUT", and "DELETE" routes, since they all use the `/users/:id` endpoint. The `:id` part of the endpoint is a variable which can be accessed in the "req.params". 

In the commented out code in the routes above, what does *User* represent?

a. A MongoDB document
b. A MongoDB collection
c. A Mongoose Model
d. Data sent in the request body

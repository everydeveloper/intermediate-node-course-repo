## CREATE: User.create 

Let's start using this model to create some users. Go to your server.js file and add this line after all the libraries are imported.

Insert the following code in the post route so it looks like this:

```javascript
// CREATE
app.post('/users',(req,res)=>{
  User.create(
    {
      name:req.body.newData.name,
      email:req.body.newData.email,
      password:req.body.newData.password
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
When you want to make a new *document* in MongoDB, you can simply call the "create" method on your mongoose model. The first argument is an object containing the values for the new document (stored in req.body). The next argument is a callback function, which handles the response (res) from the database.

## Testing

Ok let's test our code before we push it to GitHub. Start up Postman and set up a post request to: http://localhost:8000/users

Under the Headers tab, add this key/value pair:

Content-Type : application/json

Next, go to the body tab and select raw JSON, then paste this in the text under it:

```json
{
  "newData":{
    "name":"Jim",
    "email":"jim@email.com",
    "password":"secretPassword"
  }
}
```

Send the post request, and see if you get a successful response. If our route worked, you should get JSON data back with the new user under "data". Notice that there is an "_id" key automatically created. 

*Leave a comment with the value of the _id key to continue*  
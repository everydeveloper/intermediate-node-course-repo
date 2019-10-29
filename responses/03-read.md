## READ: User.findById

Great, your user has an id of {{ userID }}. This is what we will use in place of :id, as we make the other requests. find the "READ" route in our server file, and replace it with this code:

```javascript
// READ
.get((req,res)=>{
  User.findById(req.params.id,(err,data)=>{
    if (err){
      res.json({
        success: false,
        message: err
      })
    } else if (!data){
      res.json({
        success: false,
        message: "Not Found"
      })
    } else {
      res.json({
        success: true,
        data: data
      })
    }
  })
})
```

## Testing 
Let's find the document for the user we just created. Make a "get" request in postman to this url: `http://localhost:8000/users/{{ userID }}`. This should return the document with the user's data.

Once you have this working, *push your code to GitHub* to continue.
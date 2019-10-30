## UPDATE: User.findByIdAndUpdate

If you want to update a document in mongoDB, you can do it with the User.findByIdAndUpdate method. This takes three arguments (id, newData, callback). The id is still coming from "req.params", but newData is an object sent through the "req.body". Also, by default the update method will return the unmodified document. We can add an "options" argument before the callback (`{new:true}`) to make it return the modified document.

Replace the "UPDATE" route with this code:

```javascript
// UPDATE
.put((req,res)=>{
  User.findByIdAndUpdate(
    req.params.id,
    {
      name:req.body.newData.name,
      email:req.body.newData.email,
      password:req.body.newData.password
    },
    {
      new:true
    },
    (err,data)=>{
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
    }
  )
})
```
Test this out by making a "PUT" request in Postman at the endpoint for our user. Update the password field by putting this json data in the request body:

```json
{
  "newData":{
    "name":"Jim",
    "email":"jim@email.com",
    "password":"newPassword"
  }
}
```

If this worked, you should see the newly modified document as a response.

*Push your code* to GitHub for the next step.

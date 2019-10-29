## Delete Data: findByIdAndDelete

To delete a document, you can use the User.findByIdAndDelete method, which takes an id and callback as arguments.

Replace the "delete" route with this:

```javascript
.delete((req,res)=>{
  User.findByIdAndDelete(
    req.params.id,
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

To test this out, make a "delete" request in Postman to this url: `http://localhost:8000/users/{{ userID }}`

You can test to make sure this worked by making a "get" request to the same url. It should say that the data could not be found. 
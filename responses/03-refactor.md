At this point, your server.js file should look something like this:

```javascript
app.post('/users',(req,res)=>{
  User.create(
    {
      name:req.body.newData.name,
      email:req.body.newData.email,
      password:req.body.newData.password
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

app.route('/users/:id')
.get((req,res)=>{
  User.findById(
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
    })
})
.put((req,res)=>{
  User.findByIdAndUpdate(
    req.params.id,
    { 
      name:req.body.newData.name,
      email:req.body.newData.email,
      password:req.body.newData.password
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
    })
})
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
    })
})
```

This code works, but it is pretty repetitive. In general, it is a good practice to refactor code like this so it is easier to maintain. 

## Create function for response

We are handling the response in the same way each time. We should define a function to shorten this and make it easier to maintain. Paste this in your server file above your routes:

```javascript
function sendResponse(res,err,data){
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
```

Now, let's call the "sendResponse" function in our mongoose callback functions:

```javascript
app.post('/users',(req,res)=>{
  User.create(
    {
      name:req.body.newData.name,
      email:req.body.newData.email,
      password:req.body.newData.password
    },
    (err,data)=>{sendResponse(res,err,data)}
  )
})

app.route('/users/:id')
.get((req,res)=>{
  User.findById(
    req.params.id,
    (err,data)=>{sendResponse(res,err,data)})
})
.put((req,res)=>{
  User.findByIdAndUpdate(
    req.params.id,
    { 
      name:req.body.newData.name,
      email:req.body.newData.email,
      password:req.body.newData.password
    },
    (err,data)=>{sendResponse(res,err,data)})
})
.delete((req,res)=>{
  User.findByIdAndDelete(
    req.params.id,
    (err,data)=>{sendResponse(res,err,data)})
})
```

You can always replace the generic sendResponse function with a custom callback, if you need more flexibility.

## Using spread syntax (...)

We can shorten these routes further by using the [JavaScript spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax), which copies each key/value pair in our newData object.

So, rather than this:

```javascript
{
  name:req.body.newData.name,
  email:req.body.newData.email,
  password:req.body.newData.password
}
```

we can write this:`{...req.body.newData}`.

Our routes should look like this now:

```javascript
app.post('/users',(req,res)=>{
  User.create(
    {...req.body.newData},
    (err,data)=>{sendResponse(res,err,data)}
  )
})

app.route('/users/:id')
.get((req,res)=>{
  User.findById(
    req.params.id,
    (err,data)=>{sendResponse(res,err,data)})
})
.put((req,res)=>{
  User.findByIdAndUpdate(
    req.params.id,
    {...req.body.newData},
    (err,data)=>{sendResponse(res,err,data)})
})
.delete((req,res)=>{
  User.findByIdAndDelete(
    req.params.id,
    (err,data)=>{sendResponse(res,err,data)})
})
```

## Create route set-up function

The code above is much easier to maintain. But what if we want to add new models using this same pattern? The only thing that would change is the route name, and the model name

```javascript
function setUpRoutes(route,Model){
  app.post(route,(req,res)=>{
    Model.create(
      {...req.body.newData},
      (err,data)=>{sendResponse(res,err,data)}
    )
  })

  app.route(route+'/:id')
  .get((req,res)=>{
    Model.findById(
      req.params.id,
      (err,data)=>{sendResponse(res,err,data)})
  })
  .put((req,res)=>{
    Model.findByIdAndUpdate(
      req.params.id,
      {...req.body.newData},
      (err,data)=>{sendResponse(res,err,data)})
  })
  .delete((req,res)=>{
    Model.findByIdAndDelete(
      req.params.id,
      (err,data)=>{sendResponse(res,err,data)})
  })
}

setUpRoutes('/users',User);
``` 

Test this in Postman to make sure you refactored correctly. When you are finished, *commit these changes and push to GitHub*.
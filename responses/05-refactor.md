Alright, let's go back to our server.js file and import those new models. 

```javascript
const Topic=require('./models/Topic');
const Response=require('./models/Response');
```

Now, we could just copy and paste our routes, and replace the endpoints for each model. That would look something like this:

```javascript
app.route('/users')
.post((req,res)=>{
  User.create(
    {...req.body.user},
    (err,user)=>{sendResponse(res,err,user)})
})
.get((req,res)=>{
  User.findById(
    req.body.id,
    (err,user)=>{sendResponse(res,err,user)})
})
.put((req,res)=>{
  User.findByIdAndUpdate(
    req.body.id,
    {...req.body.user},
    (err,user)=>{sendResponse(res,err,user)})
})
.delete((req,res)=>{
  User.findByIdAndDelete(
    req.body.id,
    (err,user)=>{sendResponse(res,err,user)})
})

app.route('/topics')
.post((req,res)=>{
  Topic.create(
    {...req.body.topic},
    (err,topic)=>{sendResponse(res,err,topic)})
})
.get((req,res)=>{
  Topic.findById(
    req.body.id,
    (err,topic)=>{sendResponse(res,err,topic)})
})
.put((req,res)=>{
  Topic.findByIdAndUpdate(
    req.body.id,
    {...req.body.topic},
    (err,topic)=>{sendResponse(res,err,topic)})
})
.delete((req,res)=>{
  Topic.findByIdAndDelete(
    req.body.id,
    (err,topic)=>{sendResponse(res,err,topic)})
})

app.route('/responses')
.post((req,res)=>{
  Response.create(
    {...req.body.response},
    (err,response)=>{sendResponse(res,err,response)})
})
.get((req,res)=>{
  Response.findById(
    req.body.id,
    (err,response)=>{sendResponse(res,err,response)})
})
.put((req,res)=>{
  Response.findByIdAndUpdate(
    req.body.id,
    {...req.body.response},
    (err,response)=>{sendResponse(res,err,response)})
})
.delete((req,res)=>{
  Response.findByIdAndDelete(
    req.body.id,
    (err,response)=>{sendResponse(res,err,response)})
})

```
However, this is the advanced Node.js tutorial! It might be easy to copy and paste once, but maintaining three things is much more tedious than only one thing. Let's make these chained routes into a single function, that we can just call for each model.

```javascript
function setUpRoutes(route,Model){
  app.route(route)
  .post((req,res)=>{
    Model.create(
      {...req.body.newData},
      (err,data)=>{sendResponse(res,err,data)})
  })
  .get((req,res)=>{
    Model.findById(
      req.body.id,
      (err,data)=>{sendResponse(res,err,data)})
  })
  .put((req,res)=>{
    Model.findByIdAndUpdate(
      req.body.id,
      {...req.body.updateData},
      (err,data)=>{sendResponse(res,err,data)})
  })
  .delete((req,res)=>{
    Model.findByIdAndDelete(
      req.body.id,
      (err,data)=>{sendResponse(res,err,data)})
  })
}

setUpRoutes('/users',User);
setUpRoutes('/topics',Topic);
setUpRoutes('/responses',Response);
``` 
Test some of these routes out in Postman, then commit these changes!

Here are a couple of things to remember while testing:
1. The key for our new data object should now be "newData", while an update object should include an "updateData" key and an "id." key.
2. After you create a response, you should update the topic's "responses" array with the new response id.

*When you are finished, commit these changes and push to GitHub.*

```console
git add .
git commit -m"create function to set up model routes"
git push origin master
```


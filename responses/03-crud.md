Ok, lets add a route to find a user by their id. Insert this code in the "get" route:

```javascript
.get((req,res)=>{
	User.findById(req.body.id,(err,data)=>{
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

This time we used the User.findById method, which will search for the unique id given to it by mongoDB. The callback specifies what to do after the method has finished running. 

Try testing this out by posting a new user, copying the value of their "_id", then making a "get" request with this json data in the request body:

```json
{
	"id":"UserIDGoesHere"
}
```

If you want to update a document in mongoDB, you can do it with the User.findByIdAndUpdate method. This takes three arguments (id, updateData, callback).

To delete a document, you can use the User.findByIdAndDelete method, which takes an id and callback as arguments.

All together our routes should look something like this:

```javascript
app.route('/users')
.post((req,res)=>{
	User.create(
		{
			name:req.body.user.name,
			email:req.body.user.email,
			password:req.body.user.password
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
.get((req,res)=>{
	User.findById(
		req.body.id,
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
.put((req,res)=>{
	User.findByIdAndUpdate(
		req.body.id,
		{
			name:req.body.user.name,
			email:req.body.user.email,
			password:req.body.user.password
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
.delete((req,res)=>{
	User.findByIdAndDelete(
		req.body.id,
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

Try testing these routes out in Postman, and *leave a comment  for the next steps.*
Being able to create, read, update, and delete data is a pretty common requirement of most dynamic websites. However, this is pretty repetitive code. We are handling the response in the same way each time. We should define a function to shorten this and make it easier to maintain.

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

Now, let's call this function in our routes:

```javascript
app.route('/users')
.post((req,res)=>{
	User.create(
		{
			name:req.body.user.name,
			email:req.body.user.email,
			password:req.body.user.password
		},
		(err,data)=>{sendResponse(res,err,data)})
})
.get((req,res)=>{
	User.findById(
		req.body.id,
		(err,data)=>{sendResponse(res,err,data)})
})
.put((req,res)=>{
	User.findByIdAndUpdate(
		req.body.id,
		{	
			name:req.body.user.name,
			email:req.body.user.email,
			password:req.body.user.password
		},
		(err,data)=>{sendResponse(res,err,data)})
})
.delete((req,res)=>{
	User.findByIdAndDelete(
		req.body.id,
		(err,data)=>{sendResponse(res,err,data)})
})
```

If we want the response to be handled in the same way each time, it way easier to maintain like this. However, you can always replace the generic sendResponse function with a custom callback, if you need more flexability.

We can shorten these routes further by using the JS object spread syntax, which copies each key/value pair in our req.user object.

So, rather than this:

```javascript
{
	name:req.body.data.name,
	email:req.body.data.email,
	password:req.body.data.password
}
```

we can write this:`{...req.body.data}`.

Our routes should look like this now:

```javascript
app.route('/users')
.post((req,res)=>{
	User.create(
		{...req.body.data},
		(err,data)=>{sendResponse(res,err,data)})
})
.get((req,res)=>{
	User.findById(
		req.body.id,
		(err,data)=>{sendResponse(res,err,data)})
})
.put((req,res)=>{
	User.findByIdAndUpdate(
		req.body.id,
		{...req.body.data},
		(err,data)=>{sendResponse(res,err,data)})
})
.delete((req,res)=>{
	User.findByIdAndDelete(
		req.body.id,
		(err,data)=>{sendResponse(res,err,data)})
})
```

Test this in Postman to make sure you refactored correctly. When you are finished, commit these changes and push to GitHub.

```console
git add .
git commit -m"add and refactor user routes"
git push origin master
```
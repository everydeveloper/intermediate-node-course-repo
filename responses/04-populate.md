One of the nice things about MongoDB is that you can reference the IDs of documents in other collections, and easily retrieve the data associated with them.

Create a new file in your "models" folder called "Topic.js" and paste this code inside it.

```javascript
const mongoose = require('mongoose');

const TopicSchema = new mongoose.Schema({
	title: { type: String, required: true },
	description: { type: String, required: true },
	author: { type: mongoose.Schema.Types.ObjectId, ref:"User", required: true  },
	responses: [{ type: mongoose.Schema.Types.ObjectId, ref:"Response"}]
});

TopicSchema.pre('find',function(next){
	this.populate('author','name')
	this.populate('responses')
	next()
})

module.exports= mongoose.model('Topic',TopicSchema)
```

When we create an instance of a topic, we can store the author's "_id" property (assigned by mongoDB) and then "populate" the author's info (so it is always up to date). We added a "pre" hook to the model that, in this case, will populate the author's name, and an array of nested responses. When you call next(), it will proceed with returning the query. 

We haven't made a Response model yet, but notice that it is enclosed in square brackets. This means that an array of ID's will be stored here (and can be populated all at once).

Let's make that Response model, by creating a file called "Response.js" in the "models" folder.

```javascript
const mongoose = require('mongoose');

const ResponseSchema = new mongoose.Schema({
	comment: { type: String, required: true },
	author: { type: mongoose.Schema.Types.ObjectId, ref:"User" },
	topic: { type: mongoose.Schema.Types.ObjectId, ref:"Topic" }
});

ResponseSchema.pre('find',function(next){
	this.populate('author','name')
	next()
})

module.exports= mongoose.model('Response',ResponseSchema)
```

When you are adding these two models, save these changes to continue.

```console
git add .
git commit -m"add Topic and Response schema with populate"
git push origin master
```
You got it! Mongoose models come with a lot of useful methods (such as create) that make it easy to query for user documents in our user collection.

Ok let's test our code before we push it to GitHub. Start up Postman and set up a post request to: http://localhost:8000/users

Under the Headers tab, add this key/value pair:

Content-Type : application/json

Next, go to the body tab and select raw JSON, then paste this in the text under it:

```json
{
  "user":{
    "name":"Jim",
    "email":"jim@email.com",
    "password":"secretPassword"
  }
}
```

Send the post request, and see if you get a successful response. Notice that there is an "_id" key automatically created. This will be important later. Try posting the same data again. You should get an error with the code: 11000, with a duplicate email key. 

To understand why this happened, remember that we said each email should be unique in the model. 

```javascript
const UserSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  hash: { type: String, required: true }
});
```

This is a good place for a commit. It everything worked in Postman, save your work to GitHub to continue:

```console
git add .
git commit -m"add user model and post route"
git push origin master
```
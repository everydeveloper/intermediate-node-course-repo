Let's start by making a User model for mongodb using the mongoose library. This will be the template used to describe what each individual *document* will look like in our *collection*.

Find the "models" directory in the root of your project and open "User.js", then add this code to it:

```js
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }
});

module.exports= mongoose.model('User',UserSchema)
``` 

Looks like a JS object doesn't it? That is one of the cool things about MongoDB, it is easy to transfer data from the frontend to the backend. Think of this as a factory, or mold, that can create new User documents in a User collection. 

Looking at the model above, which key (name, email, or password) needs to have unique values?

*Leave a comment with your answer to continue*
The last thing we want to go over is encrypting your user's passwords with a library called "bcrypt". We can do this automatically by creating a lifecycle hook in our User model:

```javascript
const mongoose = require('mongoose');
const bcrypt = require('bcrypt');

const UserSchema = new mongoose.Schema({
	name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }
});

UserSchema.pre("save", function(next) {
    if(!this.isModified("password")) {
        return next();
    }
    this.password = bcrypt.hashSync(this.password, 10);
    next();
});

UserSchema.methods.comparePassword = function(inputPassword, callback) {
    return callback(null, bcrypt.compareSync(inputPassword, this.password));
};

module.exports= mongoose.model('User',UserSchema)
```

The keyword "this" here refers to an instance of the User model (aka, a single user document).

Now each time a User document is going to be saved, it does this:
1. Checks if the password has not been modified.
2. If it has been modified (or is new) it will encrypt it (make it look like a bunch of gobbledygook).
3. If the compare password method is called (when logging in) it will decrypt the stored password, and check if it matched what was entered.

Let's finish by adding a login route to our server.js file:

```javascript
app.post('/login',async (req,res)=>{
	try {
    var user = await User.findOne({ email: req.body.email }).exec();
    if(!user) {
      return res.json({ 
      	success:false,
      	message: "User not found" 
      });
    }
    user.comparePassword(req.body.password, (error, match) => {
      if(!match) {
        return res.json({ 
        	success:false,
        	message: "password does not match" 
        });
      }
    });
    res.json({ 
    	success: true,
    	message: "The username and password combination is correct!" 
    });
	} catch (error) {
	    res.json({
	    	success:false,
	    	message:error
	    });
	}
})
```

Test this out in Postman by creating a new user (making note of their email and password). Notice how it returns a hashed version of their password? 

Now test our login route by making a "post" request to "http://localhost:8000/login".

```json
{
	"email":"emailGoesHere",
	"password":"passwordGoesHere"
}
```

If that works, commit these changes to finish this course and get some ideas for next steps.

```console
git add .
git commit -m"create login route and encrypt user passwords"
git push origin master
```


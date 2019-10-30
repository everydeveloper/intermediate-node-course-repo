Good Job! 👍 You are finished! But, there is still much more you can do with Node.js, Express.js, and MongoDB. If you want to continue working on this, here are some next steps to improve security:

1. Encrypt your user passwords with a library like "[bcrypt](https://www.npmjs.com/package/bcrypt)" before saving them.

2. Add a nested collection (activities, pets, blog posts, etc... ) to your User model using the "[populate](https://mongoosejs.com/docs/populate.html)" method. 

3. Use a library like [JSON web token](https://www.npmjs.com/package/jsonwebtoken) to authenticate your users in a login route.

4. Use middleware for your [mongoose model](https://mongoosejs.com/docs/middleware.html) or [express routes](https://expressjs.com/en/guide/using-middleware.html) to check if there is a valid token that matches the user's id before saving data.
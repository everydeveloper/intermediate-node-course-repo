*Great* let's get this project started!

First, by signing up for this class, a starter repository was copied to your GitHub account. Start by cloning this project and installing dependencies:

```console
git clone {{ repoUrl }}
cd intermediate-node-course
npm install
```

You will also need to install the free community edition of [MongoDB](https://www.mongodb.com/download-center/community) for your OS. After installing, you will need to add the path do the MongoDB bin to your environment variables. Create a `/data/db` directory in your root directory. This is where the local documents will be saved.

You will need to close and reopen your console before the new environment variables are registered. Test if it is installed with this command: `mongod --version`. If you see a version printed, then start up the database server by entering: `mongod`.

We are going to be testing our API using Postman. You can install it for free [here](https://www.getpostman.com/downloads/)

There are some express routes already setup in the server.js file. Also, we are using the "nodemon" package in this so that our server restarts automatically. Open a new console and start the server by running this command:`npm run start`. You should see the message from our app.listen method and some statements about nodemon watching for changes. 

Here's a handy checklist of what you'll need to get started on this project:

- [ ] MongoDB installed and configured
- [ ] Node.js and Git installed and configured
- [ ] Project cloned and dependencies installed
- [ ] Postman installed
- [ ] A console running the local mongoDB server (with the "mongod" command)
- [ ] A console with "nodemon" watching your server.js file.

Once you've completed the list, close this issue for the next steps.

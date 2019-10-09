Now we can use these CRUD (Create, Read, Update, Delete) routes for as many collections as we want! 🤩 However, when we make something more abstract, we lose flexability. For instance, our User model should encrypt the password before it is stored for security reasons. 

Rather than using custom routes, we can create a special lifecycle hook to encrypt passwords!

[Click here]({{ repoUrl }}/issues/6 ) to learn how to secure use passwords.
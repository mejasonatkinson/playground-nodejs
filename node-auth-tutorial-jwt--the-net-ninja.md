# [Node Auth Tutorial (JWT)](https://www.youtube.com/playlist?list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp)

## [Node Auth Tutorial (JWT) #1 - Intro & Setup](https://www.youtube.com/watch?v=SnoAwLP1a-0&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=1)

You Should Know 

- Node.js, Express & MongoDB (mongoose)
- JavaScript & Async Code (promises, callbacks, async & await)

JWT

JSON Web Tokens are ONE way to implement authentication

https://github.com/iamshaunjp/node-express-jwt-auth/tree/lesson-1

EJS
Express
Mongoose

npm install

nodemon app

database connection

## [Node Auth Tutorial (JWT) #2 - Auth Routes & Controllers](https://www.youtube.com/watch?v=muhJTRQ7WMk&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=2)

- Using an MVC (model, view & controller) approach
 
## [Node Auth Tutorial (JWT) #3 - Testing Routes & Handling POST Requests](https://www.youtube.com/watch?v=uiKwHx2K1Fo&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=3)

https://www.postman.com/

## [Node Auth Tutorial (JWT) #4 - User Model](https://www.youtube.com/watch?v=mnJxyc0DGM8&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=4)

```
const userSchema = new mongoose.Schema({
 eamil: {
  type: String,
  required: true,
  unqiue: true,
  lowercase: true
 },
 password: {
  type: String,
  required: true,
  minLength: 6
 }
});

const User = mongoose.model('user', userSchema);

module.exports = User;
```

```
const User = require('../');

module.exports.signup_post = async(req, res) => {
 const { email, password } = req.body;
 try {
  const user = await User.create({email, password});
  res.status(201).json(user);
 }
 catch (err) {
  console.loh(err);
  res.status(400).send('error');
 }
}
```

Test in postman

NEVER STORE PLAIN PASSWORDS INSIDE OF THE DATABASE!!

## [Node Auth Tutorial (JWT) #5 - Mongoose Validation](https://www.youtube.com/watch?v=nukNITdis9g&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=5)

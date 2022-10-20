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

Custom error messages

`npm install validator`

```
const { isEmail } = require('validator');

const userSchema = new mongoose.Schema({
 eamil: {
  type: String,
  required: [true, "Please enter an email"],
  unqiue: true,
  lowercase: true
  validate: [isEmail, 'Pleae enter a valid email']
 },
 password: {
  type: String,
  required: [true, "Please enter an password"],
  minlength: [6, "Minium password length is 6 characters"],
 }
});

const User = mongoose.model('user', userSchema);

module.exports = User;
```

```
// hadle errors
const handleErrors = (err) => {
 console.log(err.message, err.code);
 let errors = {email: '', password: ''};
 
 // duplicate error code
 
 if (err.code == 11000) {
  errors.email = 'that email is already registered';
  return errors;
 }
 
 // validation errors
 if(err.message.includes('user validation failed')){
  console.log(err);
  console.log(Object.values(err.errors));
  Object.values(err.errors).forEach(error => {
   console.log(error.properties);
  });
  Object.values(err.errors).forEach(({properties}) => {
   console.log(properties);
   errors[properties.path] = properties.message;
  })
 }
 return errors;
}

catch (err) {
 const errors = handleErrors(err);
 res.status(400).json( errors );
}

```

## [Node Auth Tutorial (JWT) #6 - Mongoose Hooks](https://www.youtube.com/watch?v=teDkX-_Zkbw&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=7)

Hash a users password, so that the users password can not be exposed if the database is hacked.

```
// fire a function after doc saved to db

userSchema.post('save', function (doc, next) {
 console.log('new user created and saved', doc);
 next();
})
```

```
// fire a function before doc saved to db

userSchema.pre('save', function (next) {
 console.log('user about to be created & saved', this);
 next();
})
```

https://mongoosejs.com/docs/middleware.html


## [Node Auth Tutorial (JWT) #7 - Hashing Passwords](https://www.youtube.com/watch?v=DmrjFKTLOYo&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=8)

```
 npm install bcrypt
```

password1234 -> Hashing Algorithm -> A697y8yujkjfh

salt + password1234 -> Hashing Algorithm -> A697y8yujkjfh

```
const bcrypt = require('bcrypt')

// fire a function before doc saved to db
userSchema.pre('save', async function (next) {
 const salt = await bcrypt.genSalt();
 this.password = await bcrypt.hash(this.password, salt);
 next();
})
```

## [Node Auth Tutorial (JWT) #8 - Auth Views](https://www.youtube.com/watch?v=8RiDRdHPcxA&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=9)

## [Node Auth Tutorial (JWT) #9 - ](https://www.youtube.com/watch?v=mevc_dl1i1I&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=10)

## [Node Auth Tutorial (JWT) #10 - ](https://www.youtube.com/watch?v=LZq0G8WUaII&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=11)

## [Node Auth Tutorial (JWT) #11 - ](https://www.youtube.com/watch?v=S-ZIfNuT5H8&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=12)

## [Node Auth Tutorial (JWT) #12 - ](https://www.youtube.com/watch?v=eWGwQ1__73E&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=13)

## [Node Auth Tutorial (JWT) #13 - ](https://www.youtube.com/watch?v=VliJT26LPFA&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=14)

## [Node Auth Tutorial (JWT) #14 - ](https://www.youtube.com/watch?v=f-2jDPgh_Ng&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=15)

## [Node Auth Tutorial (JWT) #15 - ](https://www.youtube.com/watch?v=9N7uqbuODqs&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=16)

## [Node Auth Tutorial (JWT) #16 - ](https://www.youtube.com/watch?v=jQn74jB5dg0&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=17)

## [Node Auth Tutorial (JWT) #17 - ](https://www.youtube.com/watch?v=JqF2BJBQI9Y&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=18)

## [Node Auth Tutorial (JWT) #18 - ](https://www.youtube.com/watch?v=mqubRYtnPcs&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=19)












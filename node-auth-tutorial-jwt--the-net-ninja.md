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

Frontend instead of postman

signup.ejs

```
<%- include('partials/header'); -%>

<form>
 <h2>Sign up</h1>
 
 <label for="email">Email</label>
 <input type="text" name="email" required />
 <div class="email error"></div>
 
  <label for="password">Password</label>
 <input type="password" name="password" required />
 <div class="password error"></div>
 
 <button>Sigm up</button>
 
</form>

<script>
 const form = document.querySelector('form');
 form.addEventListener('submit', (event) => {
  event.preventDefault();
  const email = form.email.value;
  const password = form.password.value;
  
  console.log(email, password);
 })
</script>

<%- include('partials/footer'); -%>
```

login.ejs

```
<%- include('partials/header'); -%>

<form>
 <h2>Log in</h1>
 
 <label for="email">Email</label>
 <input type="text" name="email" required />
 <div class="email error"></div>
 
  <label for="password">Password</label>
 <input type="password" name="password" required />
 <div class="password error"></div>
 
 <button>Sigm up</button>
 
</form>

<script>
 const form = document.querySelector('form');
 form.addEventListener('submit', (event) => {
  event.preventDefault();
  const email = form.email.value;
  const password = form.password.value;
  
  console.log(email, password);
 })
</script>

<%- include('partials/footer'); -%>
```

## [Node Auth Tutorial (JWT) #9 - Cookies Primer](https://www.youtube.com/watch?v=mevc_dl1i1I&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=10)

Cookies

Store data in a user's browser
name=shaun, age=30,

Create a cookie, on a server response.
Every request sends a cookie to the server. 
Which holds a JWT, to authenticate the user.

There are possible sercuirty issues with this and other methods.

cross site, request forgery

state changing end points...

[Research CSRF](https://owasp.org/www-community/attacks/csrf)

app.js

```
// cookies
app.get('/set-cookies', (req, res) => {
 res.setHeader('Set-Cookie', 'nameUser=true');
 res.send('you got the cookies!');
});
```

got to localhost:3000/set-cookies
inspect > Applications > Cookies > You should see it there.

`document.cookie`

alternative:

npm install cookie-parser

```
const cookieParser = require('cookie-paser');

// middleware
app.use(cookieParser());

// cookies
app.get('/set-cookies', (req, res) => {
 // res.setHeader('Set-Cookie', 'nameUser=true');
 
 res.cookie('newUser', false);
 
 res.cookie('isEmployee', true, { maxAge: 1000 * 60 * 60 * 24, httpOnly: true }); 
 // 1 day in mil seconds
 
 // res.cookie('isEmployee', true, { maxAge: 1000 * 60 * 60 * 24, secure:true }); 
 // only send when you have a secure connection (https)
 
 // res.cookie('isEmployee', true, { maxAge: 1000 * 60 * 60 * 24, httpOnly:true }); 
 // cookie can only be accessed by http and not in the console by using document.cookie
 
 res.send('you got the cookies!');
});

app.get('/read-cookies', (req, res) => {

 const cookies = req.cookies;
 console.log(cookies);
 console.log(cookies.newUser);
 res.json(cookies);

});

```

Should always use https, for production.

## [Node Auth Tutorial (JWT) #10 - JSON Web Tokens (theory)](https://www.youtube.com/watch?v=LZq0G8WUaII&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=11)

Log in form (browser) > email + password > server

IF correct (checked creds in database)

server > JSON Web Token (JWT) cookie > browser

The token can then be sent back to the server on each request

browser > JSON Web Token (JWT) cookie > server

[Research CSRF](https://owasp.org/www-community/attacks/csrf)

https://jwt.io/

JWT Signing

Headers
For additional infomation (meta)

Payload
For identity 

Signature
For security 

Secret
A secret secure string

They are all hashed together to create the JWT Signing

## [Node Auth Tutorial (JWT) #11 - New User Signup (part 1)](https://www.youtube.com/watch?v=S-ZIfNuT5H8&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=12)

1. hash pw and store in db [x]
2. instantly log the user in [ ]
3. create a jwt for them [ ]

app.js

```
const cookieParser = require('cookie-paser');

// middleware
app.use(cookieParser());
```

signup.ejs

```
<%- include('partials/header'); -%>

<form>
 <h2>Sign up</h1>
 
 <label for="email">Email</label>
 <input type="text" name="email" required />
 <div class="email error"></div>
 
  <label for="password">Password</label>
 <input type="password" name="password" required />
 <div class="password error"></div>
 
 <button>Sigm up</button>
 
</form>

<script>
 const form = document.querySelector('form');
 form.addEventListener('submit', async (event) => {
  event.preventDefault();
  const email = form.email.value;
  const password = form.password.value;
  
  // console.log(email, password);
  
  
  try {
   const res = await fetch('/signup', {
    method: 'POST', 
    body: JSON.stringify({ email: email, password: password}), 
    // can be shortened to {email, password}
    headers: {'Content-Type': 'application/json'}
   });
  } 
  catch (err) {
   console.loh(err);
  }
  
 })
</script>

<%- include('partials/footer'); -%>
```

```
npm install jsonwebtoken
```

authControllers.js

```
const jwt = require('jsonwebtoken');
const maxAge = 3 * 24 * 60 * 60; // time in seconds // 3 days
const createToken = (id) => {
 return jwt.sign({ id }, 'net ninja secret', {
  expiresIn: maxAge 
 });
}


module.exports.signup_post = async(req, res) => {
 const { email, password } = req.body;
 try {
  const user = await User.create({email, password});
  
  const token = createToken(user._id);
  
  res.cookie('jwt', token, { httpOnly: true, maxAge: maxAge * 1000 });
  
  res.status(201).json({ user: user._id });
 }
 catch (err) {
  console.log(err);
  res.status(400).send('error');
 }
}
```

## [Node Auth Tutorial (JWT) #12 - New User Signup (part 2)](https://www.youtube.com/watch?v=eWGwQ1__73E&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=13)


signup.ejs

```
<%- include('partials/header'); -%>

<form>
 <h2>Sign up</h1>
 
 <label for="email">Email</label>
 <input type="text" name="email" required />
 <div class="email error"></div>
 
  <label for="password">Password</label>
 <input type="password" name="password" required />
 <div class="password error"></div>
 
 <button>Sigm up</button>
 
</form>

<script>
 const form = document.querySelector('form');
 form.addEventListener('submit', async (event) => {
  event.preventDefault();
  const email = form.email.value;
  const password = form.password.value;
  
  // console.log(email, password);
  
  const emailError = document.querySelector('.email.error');
  const passwordError = document.querySelector('.password.error');
  
  emailError.textContent = '';
  passwordError.textContent = '';
  
  try {
   const res = await fetch('/signup', {
    method: 'POST', 
    body: JSON.stringify({ email: email, password: password}), 
    // can be shortened to {email, password}
    headers: {'Content-Type': 'application/json'}
   });
   
   const data = await res.json();
   console.log(data);
   if (data.errors) {
    emailError.textContent = data.errors.email;
    passwordError.textContent = data.errors.password;
   }
   if (data.user) {
    location.assign('/');
   }
  } 
  catch (err) {
   console.loh(err);
  }
  
 })
</script>

<%- include('partials/footer'); -%>
```

## [Node Auth Tutorial (JWT) #13 - Logging Users in (part 1)](https://www.youtube.com/watch?v=VliJT26LPFA&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=14)

Mostly copied from New User Signup (part 1)

signup.ejs > copy, script > login.ejs

change fetch to /login

User.js

```
// static method to login user
userSchema.statics.login = async function(email, password) {
 const user = await this.findOne({email: email});
 if (user) {
  const auth = await bcrypt.compare(password, user.password);
  if (auth) {
   return user
  }
   throw Error('incorect password')
 }
 throw Error('incorect email')
}
```

authController.js

```
module.exports.login_post = async (req, res) => {
 const { email, password } = req.body;
 
 try {
  const user = await user.login(email, password);
  res.status(200).json({ user: user._id });
 }
 catch (err) {
  const errors = handleErrors(err);
  res.status(400).json({})
 }
}
```

## [Node Auth Tutorial (JWT) #14 - Logging Users in (part 2)](https://www.youtube.com/watch?v=f-2jDPgh_Ng&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=15)

authController.js

```


// hadle errors
const handleErrors = (err) => {
 console.log(err.message, err.code);
 let errors = {email: '', password: ''};
 
 // incorrect email
 if (err.message === 'incorrect email') {
  errors.email = 'that email is not registered';
 }
 

 // incorrect password
 if (err.message === 'incorrect password') {
  errors.email = 'that password incorrect';
 }
 
 
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


```

## [Node Auth Tutorial (JWT) #15 - Protecting Routes](https://www.youtube.com/watch?v=9N7uqbuODqs&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=16)





## [Node Auth Tutorial (JWT) #16 - Logging Users Out](https://www.youtube.com/watch?v=jQn74jB5dg0&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=17)

## [Node Auth Tutorial (JWT) #17 - Checking the Current User](https://www.youtube.com/watch?v=JqF2BJBQI9Y&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=18)

## [Node Auth Tutorial (JWT) #18 - Confitional Rendering](https://www.youtube.com/watch?v=mqubRYtnPcs&list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp&index=19)












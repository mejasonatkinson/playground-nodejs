# [REST API Tutorials (Node, Express & Mongo)](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8)

## [REST API Tutorial #1 - What is a REST API?](https://www.youtube.com/watch?v=BRdcRFvuqsE&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=1)

Checklist
- Basic to good understanding of JavaScript
- An appreciation / basic grasp of Node.js and MongoDB

What is a REST API?

API:

- Application
- Programming
- Interface

- TV (Application) 
- Human (Programming)
- Remote (Interface)

- Youtube (Application) 
- programing (Programming)
- Endpoint url (Interface)

Popular API's: YouTube, GoogleMaps, Twitter

REST:
- REpresentaitional 
- State
- Transfer

Architectual style of the web
A standard / set of guidelines by which we can structure & create API's
REST API's have identifiable properties

They use resource based url's

They use http methods
- GET
- POST
- PUT
- DELETE

They use http status codes
- 200
- 404
- 500

What will we learn
- http methods
- Create an API using Node.js, Express & MongoDB
- Test our API using Postman
- Create a simple front-end to interact with our API

https://github.com/iamshaunjp/rest-api-playlist

## [REST API Tutorial (Node, Express & Mongo) #2 -Setting up Node.js](https://www.youtube.com/watch?v=A5fiWcVcADw&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=2)

Installing

Node
Mongo

Mongo DB not working? As expected.. I think things have changed... since the tutorial was made?

Create package.json file

npm init -y 
npm install

## [REST API Tutorial (Node, Express & Mongo) #3 - HTTP Methods](https://www.youtube.com/watch?v=Fizxr21bjWU&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=3)

HTTP Methods
A way of telling the server what type of request is being made.
GET (read)
POST (create)
PUT (update)
DELETE

(CRUD)

API Routes

url/api/name (list)

url/api/name/id (list item)

## [REST API Tutorial (Node, Express & Mongo) #4 - Creating an Express App](https://www.youtube.com/watch?v=7uXKyRFTlWA&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=4)

Don't need express to create a API.

npm install express --save

index.js

const express = require('express');

const app = express();

app.listen(process.en.port || 4000, function(){
	console.log('now listening for requests');
});

node index

## [REST API Tutorial (Node, Express & Mongo) #5 - Handling Requests](https://www.youtube.com/watch?v=Bc2QE-kHbu0&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=5)

app.get("/", function(req, res){
	console.log('GET request);
	res.send({ name: 'Yoshi' });
});

node index

localhost:4000

## [REST API Tutorial (Node, Express & Mongo) #6 - Creating Routes](https://www.youtube.com/watch?v=BNikS1X5NVk&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=6)

node index

npm install nodemon --save-dev

nodemon index

routes/api.js

const express = require('express');
const router = express.Router();

// get a list of ninjas from the db
router.get('/ninjas', function(req, res){
	res.send({type:'GET'});
});

// add a new ninja to the db
router.post('/ninjas', function(req, res){
	res.send({type:'POST'});
});

// update a ninja in the db
router.put('/ninjas/:id', function(req, res){
	res.send({type:'PUT'});
});

// delete a ninja in the db
router.delete('/ninjas/:id', function(req, res){
	res.send({type:'DELETE'});
});


module.exports = router;

index.js

const express = require('express');
const routes = require('./routes/api');

const app = express();

// initialize routes
app.use('/api', routes);

app.listen(process.env.port || 4000, function(){
console.log('now listening for requests');
});

localhost:4000/api/ninjas

Browsers on there own can only handle get requests




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

## [REST API Tutorial (Node, Express & Mongo) #6.5 - Postman](https://www.youtube.com/watch?v=3Nvx0mNXPc4&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=7)

GET

localhost:4000/api/ninjas

POST

localhost:4000/api/ninjas

PUT

localhost:4000/api/ninjas/yoshi

DELETE

localhost:4000/api/ninjas/yoshi


make sure node or nodemon is running.

## [REST API Tutorial (Node, Express & Mongo) #7 - Handling POST Requests (& middleware)](https://www.youtube.com/watch?v=bWiW7tLtlJM&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=8)

POST request

POST

localhost:4000/api/ninjas

Body

raw

JSON (application/json)

{
"name": "ryu",
"rank": "black belt"
}


Middleware

fired between request and response

app.use(middleware);

npm install body-parser --save

index.js

const bodyParser = require('body-parser');

app.use(bodyParser.json());

routes/api.js

// add a new ninja to the db
router.post('/ninjas', function(req, res){
	console.log(req.body);
	res.send({
		type:'POST',
		name: req.body.name,
		rank: req.body.rank
	});
});

nodemon index


## [REST API Tutorial (Node, Express & Mongo) #8 - Models & Schemas](https://www.youtube.com/watch?v=aoB0IkQ_1jE&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=9)


Models, 
are collections within MongoDB

Users
Ninjas

Schemas
is the structure of the data in the collections

Mongoose

adds a layer of methods to easily save, edit, retreive and delete data from mongodb

npm install mongoose --save

models/ninjas.js

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// create ninja Schema & model
const NinjaSchema = new Schema({
	name: {
	type: String,
	required: [true, 'Name field is required'],
	},
	rank: {
	type: String,
	}
	available: {
	type: Boolean,
	default: false
	}
	// add in geo location

});

const Ninja = mongoos.model('ninja', NinjaSchema);

module.exports = Ninja;

## [REST API Tutorial (Node, Express & Mongo) #9 - Saving Data to MongoDB](https://www.youtube.com/watch?v=cOt8LfcA9wY&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=10)

run mongoDB

index.js

const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/ninjago');
mongoose.Promise = global.Promise;

app.js

const Ninja = require('../models/ninja');

router.post('/ninjas', function(req, res){
	// var ninja = new Ninja(req.body);
	// ninja.save();

	Ninja.create(re.body).then(function(ninja){
		res.send(ninja);
	});
});


Postman

POST

localhost:4000/api/ninjas

Body

raw

JSON (application/json)

{
"name": "ryu",
"rank": "black belt"
"available:": true
}

Send

Will return: "_id":

Robomongo (3T is halting development work on Robo 3T and we are setting the code repository to read-only)




Postman

POST

localhost:4000/api/ninjas

Body

raw

JSON (application/json)

{
"name": "yoshi",
"rank": "brown belt"
}

Send




Postman

POST

localhost:4000/api/ninjas

Body

raw

JSON (application/json)

{
"rank": "brown belt"
"available:": true
}

Send

Loading... Error?


## [REST API Tutorial (Node, Express & Mongo) #10 - Error Handling](https://www.youtube.com/watch?v=w1V2SdzdQBs&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=11)

Middleware

Request

Body Parser

Route Handlers

Response


app.js


router.post('/ninjas', function(req, res, next){
	Ninja.create(re.body).then(function(ninja){
		res.send(ninja);
	}).catch(next);
});


index.js

app.use(function(err, req, res, next){
	// console.log(err);
	res.status.(422).send({error: err.message});
});


## [REST API Tutorial (Node, Express & Mongo) #11 - Handling DELETE Requests](https://www.youtube.com/watch?v=NEFfbK323Ok&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=12)


api.js

router.delete('/ninja/:id', function(req, res, next) {

// console.log(req.params.id);

Ninja.findByIdAndRemove({_id: req.params.id}).then(function(ninja){
res.send(ninja);
})

// res.send({type: 'DELETE'});

});

## [REST API Tutorial (Node, Express & Mongo) #12 - PUT Requests](https://www.youtube.com/watch?v=sEkRmVfc8XE&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=13)

api.js

router.put('/ninja/:id', function(req, res, next) {

Ninja.findByIdAndUpdate({_id: req.params.id}, req.body).then(function(){
	Ninja.findOne({_id: req.params.id}).then(function(ninja) {
		res.send(ninja);
	})
})

// res.send({type: 'PUT'});

});


## [REST API Tutorial (Node, Express & Mongo) #13 - GeoJSON](https://www.youtube.com/watch?v=MvY8vcrojYw&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=14)

Mongo GeoJSON


ninja.js


  // "geometry": {
    // "type": "Point",
    // "coordinates": [125.6, 10.1]
  // },


const GeoSchema = new Schema({
type: {
	type: String,
	default: "Point"
},
coordinates: {
	type: [Numbers],
	index: "2dsphere"
}
});


const NinjaSchema = new Schema({
name: {
type: String,
required: [true, 'Name field is required']
},
rank: {
 type: String
},
geometry: GeoSchema
})


api.js

router.get('/ninjas', function(req, res, next) {
res.send({type: 'GET'});
});


https://geojson.org/





## [REST API Tutorial (Node, Express & Mongo) #14 - GET Requests](https://www.youtube.com/watch?v=k8mi38BI55g&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=15)

Post content...




api.js

router.get('/ninjas', function(req, res, next) {
res.send({type: 'GET'});
});

URL Params

?lng50.45&lat=42.35






api.js

router.get('/ninjas', function(req, res, next) {


Ninja.geoNear(
	{type: 'Points', coordinates: [parseFloat(req.query.lng), parseFloat(re.query.lat)]},
	{maxDistance: 100000, spherical: true}
).then(function(ninjas){
res.send(ninjas);
});

});


Postman add params

lng -80
lat 25




## [REST API Tutorial (Node, Express & Mongo) #15 - Creating a Front-end](https://www.youtube.com/watch?v=fGQFeV32nwE&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=16)


index.js

app.use(express.static('public'));

public/index.html

react out of date...

public/styles.css

## [REST API Tutorial (Node, Express & Mongo) #16 - Creating a React Component](https://www.youtube.com/watch?v=f7zXuZRsCTk&list=PL4cUxeGkcC9jBcybHMTIia56aV21o2cZ8&index=17)

Speed runing react...


<!-- Create React Component -->

<script type="text/babel">
var Ninjas = React.createClass({

getInitialState: function(){
return({
ninjas: []
});
}
render: function(){
var ninjas = this.state.ninjas;
ninjas = ninjas.map(function(ninja, index){
return(
<li key={index}>
	<span className={ninja.obj.available}></span>
	<span className="name">{ninja.obj.name}</span>
	<span className="rank">{ninja.obj.rank}</span>
	<span className="dist">{Math.floor(ninja.dis / 1000)} km</span>
</li>
)
});
return(
<div id="ninja-container">
<form id="search" onSubmit={this.handleSubmit}>
<label>latitude</label>
<input type="text" ref="lat" placeholder="latitude" required />
<label>longitude</label>
<input type="text" ref="lng" placeholder="longitude" required/ >
<input type"submit" value="FIND Ninjas" />
</form>
<ul>{ninjas}</ul>
</div>
);
	handleSubmit: function(e){
	e.preventDefault();
	var lng = this.refs.lng.value;
	var lat = this.refs.lat.value;
		fetch('/api/ninjas?lng=' + lng + "&lat=" + lat).then(function(data){
			return data.json();
		}).then(json => {
			this.setState({
				ninjas: json
			});
		})
	}
});

reactDOM.render(<Ninjas />, document.getElementById('ninjas'));

</script>




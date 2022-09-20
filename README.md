# Playground for Node JS

A place to learn more about Node JS, and try things.

10/09/22 -

## Resources

- [Node.js Crash Course Tutorial](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU)

Node.js Crash Course Tutorial #1 - Introduction & Setup
https://www.youtube.com/watch?v=zb3Qk8SG5Ms&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=1

This is an updated nodejs playlist

Front-end (browser)

Back-end (back-end)
Node allows, JS to work on the backend.

-> JavaScript
-> C++
-> Assembly Language
-> Machine code

Machine code can not understand JavaScript on its own.

BUT browsers understand javascript
AND some browsers use an engine to help run javascript called the V8 Engine, which is written in C++

Node.js is written in C++ and is used to run V8 Engine, AND adds more features to JavaScript including:

- Read & write files on a computer
- Connect to a database
- Act as a server for content

-> NodeJS(JavaScript)
-> C++
-> Assembly Language
-> Machine code

Node.js, you can use instead of python, php etc...

Need to know:

- JavaScript (functions, async code, promises etc)
- HTML & CSS

Installing node

command promt
node -v

nodejs.org, download and install if you don't have it installed.

node

going to usee visual studio code...

ctrl + c, ctrl + c, 

cd {file path}

mkdir {name}

cd {name}

code .

new file


test.js

const name = 'mario';
console.log(name);

terminal

node test

https://github.com/iamshaunjp/node-crash-course


Node.js Crash Course Tutorial #2 - Node.js Basics

https://www.youtube.com/watch?v=OIBIXYLJjsI&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=2


Node serve, to handle, requests

const great = (name) => {
	console.log('hello, ${name}');
}

great('mario');

The Global Object

In a browser you have the window object

In node you have the global object

console.log(global);

global.setTimeout(() => {
console.log('in the timeout');
}, 3000)

const int = setTimeout(() => {
console.log('in the timeout');
}, 3000);

setInterval();

ctrl + c

clearInterval(int);

console.log(__dirname); // absolute path
console.log(__filename); // absolute path + file name

Modules & Require

import/export files.

multiple files

modules

const xyz = require('./people');

console.log(xyz)

console.log(xyz.people, xyz.ages);

OR

const { people, ages } = require('./people');

console.log(people, ages);


const os = require('os');

console.log(os);



people

const people = ['jason']
const ages = [31]

module.exports = 'hello'

module.exports = {
	people: people,
	ages: ages,
};


the file system

const fs = require('fs');

// read files

fs.readFile('./file.txt', (err, data) => {
if(err) {
console.log(err);
}
console.log(data.toString());

})


// write files

fs.writeFile('./file.txt', 'hello, world', () => {
	console.log('complete');
})


// directories


if(!fs.existsSync('./assets')) {

fs.mkdir('./assets', (err) => {
if(err) {
	console.log(err);
}
	console.log('complete');
})

} else {

fs.rmdir('./assets', (err) => {
if(err) {
	console.log(err);
}
	console.log('complete');
})

}

// delete  files

if(fs.existsSync('./assets/deleteme.txt')) {

fs.unlick('./assets/deleteme.txt', (err) => {
if(err) {
	console.log(err);
}
	console.log('complete');

})

}

Streams & Buffers

what if there is alot of data

Streams

Start using data, before it has finished loading.

sending, buffers.

read stream

write stream

stream.js

const fs = require('fs');

const readStream = fs.createReadStream('./doc/blog.txt', {encoding: 'utf8'});

const writeStream = fs.createWriteStream('./doc/new.txt');

readStream.on('data', (chunk) => {

// event listener
console.log('------------------');
console.log(chunk);
console.log(chunk.toString()); // or encoding
console.log('------------------');

writeStream('\nNEW CHUNK\n');
writeStream.write(chunk);

})

// piping
readStream.pipe(writeStream);

Node.js Crash Course Tutorial #3 - Clients & Servers
https://www.youtube.com/watch?v=-HPZ1leCV8k&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=3

IP Addresses & Domains

Domains mask IP Addresses

GET Request, to get a resource

via HTTP, Hyper-Text Transfer Protocol

Create a server

with other langs such as PHP, this is done with apache.


new folder

server.js

const http = require('http');

const server = http.createServer((request, response) => {
	console.log('request made');	
});

server.listen(3000, 'localhost', () => {
	console.log('listening for requests on port 3000');
})



Localhost & Port Numbers

127.0.0.1 Loop back to own computer

port, gate, door. into and out off your computer.

url: localhost:3000

termainal: node server


Node.js Crash Course Tutorial #4 - Requests & Responses
https://www.youtube.com/watch?v=DQD00NAUPNk&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=4


const http = require('http');
const fs = require('fs');

const server = http.createServer((request, response) => {

console.log(request);

// used for routing
console.log(request.url);
console.log(request.method);

console.log(response);

// response headers

// set header content type
// response.setHeader('Content-Type', 'text/plain');
response.setHeader('Content-Type', 'text/html');

// response.write('hello world');
// response.write('<h1>hello world<h1>');

// response.end();


let path = './views';

switch(request.url) {
	case '/':
		path += 'index.html';
		response.statusCode = 200;
		break;
	case '/about':
		path += 'about.html';
		response.statusCode = 200;
		break;
	case '/about-me':
		response.statusCode = 301;
		response.setHeader('Location', '/about');
		response.end();
		break;
	default:
		path += '404.html';
		response.statusCode = 404;
		break;
}

// send html file
fs.readFile(path, (err, data) => {
	if(err) {
		console.log(err);
		response.end();
	} else {

		response.write(data);
		response.end();
		// OR
		// response.end(data);
		// does the same thing.
		
	}
})


});


server.listen(3000, 'localhost', () => {
	console.log('listening');
});


noder server

IF you make a change to the server file, you will need to cancel out off and restart the server

views folder

index.html file

...


Status Codes

200 - OK
301 - Resource moved
404 - Not found
500 - Internal server error


Redirects


https://www.youtube.com/watch?v=bdHE2wHT-gQ&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=5
Node.js Crash Course Tutorial #5 - NPM

node core

other node packages can be downloaded by npm

npm is installed with node

lodash

nodemon - Live, refreshable server

npm install -g nodemon 

-g global

nodemon server

package.json

local packages

npm init

npm i --save lodash // old versions of node/npm

npm i lodash

npm install lodash

will see under dependencies

const _ = require('lodash');

const num = _.random(0, 20);
console.log(num);

dependencies

const greet = _.once(() => {
	console.log('hello');
});


DONT upload node_modules - because its HUGE!!

npm install
npm i

https://www.youtube.com/watch?v=Lr9WUkeYSA8&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=6
Node.js Crash Course Tutorial #6 - Express Apps


Saves you time

https://www.npmjs.com/package/express

npm install express

app.js

const express = require('express');

const app = express ();

app.listen(3000);

app.get('/', (request, response) => {
	// response.send('<h1>Hello World</h1>');
	response.sendFile('./views/index.html', { root: __dirname });
	// file // location
})

app.get('/about', (request, response) => {
	// response.send('<h1>About Hello World</h1>');
	response.sendFile('./views/about.html', { root: __dirname });
	// file // location
})


app.get('/about-us', (request, response) => {
	response.redirect('/about');
})


// 404 / middleware
// must be at the bottom of the application
// AS this runs regardless of page
app.use((request, response) => {
	response.status(404).sendFile('./views/404.html', { root: __dirname });
})



https://www.youtube.com/watch?v=yXEesONd_54&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=7
Node.js Crash Course Tutorial #7 - View Engines

Static, or dynamic data.

Different view engines

- express handlebars
- pug
- ejs ***


npm install ejs

app.js

const express = require('express');

const app = express ();

// register view engine
app.set('view engine', 'ejs');

// will look in a views folder by defauly but can be changes
app.set('views', 'myviews');

// files end with ejs extention index.ejs


app.get('/', (request, response) => {
	const blogs = [
	{title: 'title', snippet: 'snippet'}
	]
	response.render('index', {
		title: 'home',
		blogs: blogs
	});
})

app.get('/about', (request, response) => {
	response.render('about', {
		title: 'about'
	});
})

app.get('/blogs/create', (request, response) => {
	response.render('create', {
		title: 'create'
	});
})

app.use((request, response) => {
	response.status(404).render('404', {
		title: '404'
	});
})

// passing data to views

ejs tags

<% const name = 'mario'; %>
<p><%= name %></p> escapes specail charactors. 

<p><%= title %></p> // pass it from the app.js


<% if(blogs.length > 0) { %>

<% blogs.forEach(blog => {  %>

<h3><%= blog.title %></h3>
<p><%= blog.snippet %></p>

<% }) %>

<% } esle { %>

 <p>No blogs to display</p>

<% } %>

Partials

header.ejs

index.ejs

<%- include('./partials/header.ejs') %> // to use html

Adding css


https://www.youtube.com/watch?v=_GJKAs7A0_4&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=8
Node.js Crash Course Tutorial #8 - Middleware


What is Middleware?

code which runs on the server between getting a request and sending a response.

.use
.get

examples

log details,
authentication
parse data
return 404 pages

custom middleware

app.use((request, response, next) => {
	console.log("middleware #2");
	console.log(request.hostname);
	console.log(request.path);
	console.log(request.method);
	next();
});

app.use((request, response, next) => {
	console.log("middleware #1");
	next();
});


3rd-party Middleware

https://www.npmjs.com/package/morgan

npm install morgan

const morgan = require('morgan');

app.use(morgan('dev'));

https://www.npmjs.com/package/helmet

// middleware & static files
app.use(express.static('public')); // don't need to add public to the url of the link


Node.js Crash Course Tutorial #9 - MongoDB
https://www.youtube.com/watch?v=bxsemcrY4gQ&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=9

Database

SQL

tables, rows, columns

NoSQL

collections, documents

mongoDB is a NoSQL database

collections are sort off like tables.
documents are sort off like records. stored similar to JSON..


MongoDB Atlas

Local or cloud based

build cluster

collections

add my own data

database access

add new database user


connect to application,


app.js

const dbURI = '';

Mongoose

ODM library - Object Document Mapping library

Schema & Models

defines the structure of a type of data / document

npm install mongoose

const mongoose - require('mongoose');

mongoos.connect(dbURI, {userNewUrlParser: true, userUnifiedTopology: true }).then((result,) => {
console.log('');
}).catch((err) => {
console.log('');
})

models/blog.js

const mongoose - require('mongoose');
const Schema = mongoos.Schema;

const blogSchema = new Schema({
title: {
type: String
required: true
},
snippet: {
type: String
required: true
},
body: {
type: String
required: true
}, {timestamps: true});

const Blog = mongoose.model('Blog', blogSchema);

module.exports = Blog;


getting and saving data

app.js

const Blog = require('./models/blog');

app.get('/add-blog', (req, res) => {
const blog = new Blog({
title: '',
snippet: '',
body: ''
})

blog.save().then((result) => {
res.send(result) // displayed on page
}).catch((err) => {
console.log(err);
})
})

app.get('/all-blogs', (req, res) => {
	Blog.find().then((result) => {
	res.send(result) // displayed on page
}).catch((err) => {
console.log(err);
})
})

	Blog.findById()

	Blog.find().sort()

outputting

app.get('/blogs', (req, res) => {

Blog.find().then((result) => {


res.render('index', { title: 'All Blogs', blogs: result})


}).catch((err) => {
console.log(err);
})

})





<!-- 

- [Node JS Tutorial for Beginners](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gcy9lrvMJ75z9maRw4byYp)

- [Node.js Tutorial for Beginners: Learn Node in 1 Hour](https://www.youtube.com/watch?v=TlB_eWDSMt4)

-->


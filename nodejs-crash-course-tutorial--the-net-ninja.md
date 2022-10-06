# [Node.js Crash Course Tutorial; The Net Ninja](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU)

## [Node.js Crash Course Tutorial #1 - Introduction & Setup](https://www.youtube.com/watch?v=zb3Qk8SG5Ms&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=1)

This is an updated nodejs playlist

Front-end (browser)

Back-end (server)

Node allows, JS to work on the back-end.

- JavaScript
- C++
- Assembly Language
- Machine code

Machine code can not understand JavaScript on its own BUT browsers understand javascript AND some browsers use an engine to help run javascript called the V8 Engine, which is written in C++

Node.js is written in C++ and is used to run V8 Engine, AND adds more features to JavaScript including:

- Read & write files on a computer
- Ability to connect to a database
- Act as a server for content

Node.js, can be used instead of python or php...

What you need to know first:

- JavaScript (functions, async code, promises etc)
- HTML & CSS

[Code for the lessons can be found here](https://github.com/iamshaunjp/node-crash-course)

## [Node.js Crash Course Tutorial #2 - Node.js Basics](https://www.youtube.com/watch?v=OIBIXYLJjsI&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=2)

**The Global Object**

In a browser you have the window object

In node you have the global object

`console.log(global);` will show you all the things you have access to using the global object.

File paths; node, also gives us access to 2 types of file paths

`console.log(__dirname);` which is a absolute path

`console.log(__filename);` which is a absolute path + file name

**Modules & Require**

Modules, is away of describing when you use multiple files to seperate concerns, then use export and import commands to use them together.
<!-- Not sure if I like this description? -->

You can import a file using the require function, for example:

`const xyz = require('./xyz');`

or you can access certain things within the file:

`const { x, y, x } = require('./xyz');`


<!--

**The file system**

`const fs = require('fs');`

Allows you to read files

`fs.readFile('./file.txt', (err, data) => { if(err) { console.log(err); } else { console.log(data.toString()); } } );`

Allows you to write files

`fs.writeFile('./file.txt', 'hello, world', () => { console.log('complete'); } );`

Allows you to create directories

`if( !fs.existsSync('./assets') ) { fs.mkdir('./assets', (err) => { if(err) { console.log(err); } else { console.log('complete'); } } ); } else { fs.rmdir('./assets', (err) => { if(err) { console.log(err); } else { console.log('complete'); } } ); }`

<!-- How to do multiple line code blocks in markdown -->

```
Multiline();
Code();
Block();
```

Allows you to delete files

`if( fs.existsSync('./assets/deleteme.txt') ) { fs.unlick('./assets/deleteme.txt', (err) => { if(err) { console.log(err); } else { console.log('complete'); } } ) }`

**Streams & Buffers**

What do you do if there is alot of data?

Streams allows you to start using data, before it has finished downloading by sending buffers.

You can create Read or Write streams.

## [Node.js Crash Course Tutorial #3 - Clients & Servers](https://www.youtube.com/watch?v=-HPZ1leCV8k&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=3)

**IP Addresses & Domains**

Domains mask IP Addresses

**GET Requests** are used to get a resource via HTTP(Hyper-Text Transfer Protocol)

With other languages such as PHP, this is done with apache?

**How to create a server?**

`server.js`

`const http = require('http');`

`const server = http.createServer( (request, response) => { } );`

`server.listen( 3000, 'localhost', () => { } );`

**Localhost & Port Numbers**

The IP, **127.0.0.1** will always Loop back to own computer.

**PORTS** are gates or doors into and out off your computer.

**URL:** localhost:3000

**Termainal command:** `node server`

## [Node.js Crash Course Tutorial #4 - Requests & Responses](https://www.youtube.com/watch?v=DQD00NAUPNk&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=4)

**Status Codes**

- **200** - OK
- **301** - Resource moved
- **404** - Not found
- **500** - Internal server error

## [Node.js Crash Course Tutorial #5 - NPM](https://www.youtube.com/watch?v=bdHE2wHT-gQ&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=5)

Node.js is the core, but other node packages can be downloaded by the npm (node package manager)

npm is installed with node

**nodemon** is a Live, refreshable server; node package

`npm install -g nodemon` allows you to install it globally.

To use it locally run the command `npm init` to create a package.json file.

The run `npm i --save lodash` (for old versions of node/npm) or `npm i lodash` (for newer versions of node/npm)

You will see lodash under dependencies in the package.json

## [Node.js Crash Course Tutorial #6 - Express Apps](https://www.youtube.com/watch?v=Lr9WUkeYSA8&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=6)

https://www.npmjs.com/package/express

`npm i express`

`const express = require('express');`

## [Node.js Crash Course Tutorial #7 - View Engines](https://www.youtube.com/watch?v=yXEesONd_54&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=7)

**Static, or dynamic data**

**View Engines** Similar to how php works..

`npm i ejs`

````
const express = require('express');
const app = express ();
app.set('view engine', 'ejs');
app.set('views', 'myviews');
````

Youn can then pass data to views with ejs tags.

````
<% const name = 'mario'; %>
<p><%= name %></p>
<p><%= title %></p>
````

`=` is needed to escape specail charactors

````
<% if(blogs.length > 0) { %>
	<% blogs.forEach(blog => {  %>
		<h3><%= blog.title %></h3>
		<p><%= blog.snippet %></p>
	<% }) %>
<% } esle { %>
	<p>No blogs to display</p>
<% } %>
````

**Partials**

`header.ejs`

`index.ejs`

`<%- include('./partials/header.ejs') %>`


## [Node.js Crash Course Tutorial #8 - Middleware](https://www.youtube.com/watch?v=_GJKAs7A0_4&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=8)

What is Middleware?

Middleware is code which runs on the server between getting a request and sending a response.

Examples of Middleware include; data/detail logging, authentication, parsing data and returning a 404 pages.

You can Build Custom Middleware or you can use 3rd-part Middleware

**Example of Custom Middleware**
    
````    
app.use((request, response, next) => {
	console.log("middleware");
	console.log(request.hostname);
	console.log(request.path);
	console.log(request.method);
	next();
});
````

**Example of 3rd-party Middleware**

https://www.npmjs.com/package/morgan

`npm i morgan`

````
const morgan = require('morgan');
app.use(morgan('dev'));
```

-OR-

https://www.npmjs.com/package/helmet

`app.use(express.static('public'));`


## [Node.js Crash Course Tutorial #9 - MongoDB](https://www.youtube.com/watch?v=bxsemcrY4gQ&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=9)

<!--

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

-->

## [Node.js Crash Course Tutorial #10 - Get, Post & Delete Requests](https://www.youtube.com/watch?v=VVGgacjzc2Y&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=10)

<!--

Request Types

GET requests to get a resource

route parameters

localhost:3000/blogs/:id

something which could change.



app.get('/blog/:id', (req, res) => {

const id = req.params.id;
console.log(id);
Blog.findById(id)
.then((result) => {

res.render('details', {blog: result, title: 'blog details' });

}).catch((err) => {
console.log(err);
})



})






POST requests to create new data

<form action="/blogs" method="POST">
<input type="text" name="title"> // needs name

app.js

app.use(express.urlencoded({ extended: true }));


ap.post('./blogs', (req, res) => {

console.log(req.body);
const blog = new Blog(req.body);

blog.save().then((result) => {
res.redirect('/blogs');
}).catch((err) => {
console.log(err);
})

})

DELETE requests to delete data

<a class="delete" data-doc="<%= blog._id %>">delete</a>

<script>


const trashcan = document.querySelect('a.delete');
trashcan.addEventListern('click', (e) => {
const endpoint = `/blogs/${trashcan.dataset.doc}`;

fetch(endpoit, {
method: 'DELETE'
}).then((response) => {

}).catch((err) => {

console.log(err);
})

})


</script>

app.js

app.delete('/blogs/:id', (req, res) => {

const id = req.params.id;



Blog.findByIdAnd Delete(Id).then((result) => {
res.json({ redirect: '/blogs' })
}).catch((err) => {
console.log(err);
})

})


PUT requests to update data


LOST???

-->

## [Node.js Crash Course Tutorial #11 - Express Router & MVC]( https://www.youtube.com/watch?v=zW_tZR0Ir3Q&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=11)

<!--

Split routes,

routes/blogroutes.js

const express = require('express');

const router = express.router();

router.get('/blogs', (req, res) => {

})


module.exports = router;

app.js

const blogRoutes - require('./routes/blogroutes.js');


app.use(blogRoutes);


MVC Basics

Model, View, Controllers

structuring our code & files


keeps code more modular, reusable & easier to read

controllers.
the middle between model, view

controller functions

// blog_index, blog_details, blog_create_get, blog_create_post, blog_delete

LOST?

-->

## [Node.js Crash Course Tutorial #12 - Wrap up](https://www.youtube.com/watch?v=nYAyhRAV87A&list=PL4cUxeGkcC9jsz4LDYc6kv3ymONOKxwBU&index=12)

This was a beginner course, to help progress to more advanced subjects such as: **[Node.js Auth Tutorial (JWT)](https://www.youtube.com/playlist?list=PL4cUxeGkcC9iqqESP8335DA5cRFp8loyp)**

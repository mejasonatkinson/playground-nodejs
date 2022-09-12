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



<!-- 

- [Node JS Tutorial for Beginners](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gcy9lrvMJ75z9maRw4byYp)

- [Node.js Tutorial for Beginners: Learn Node in 1 Hour](https://www.youtube.com/watch?v=TlB_eWDSMt4)

-->


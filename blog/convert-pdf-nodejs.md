# Convert documents to and from PDF with NodeJs

Many progressive web apps nowadays are built using serverless architecture where complex computations and machine resources are hosted by a third-party service, 
eliminating the need for server software and hardware management by the developer. 
ConvertAPI is a cloud based, platform independent market leader when it comes to processing documents on demand.
It allows you to convert images, MS office documents, ebooks, emails, web pages to PDF as well as merge, encrypt, compress and apply multiple advanced operations to the
final PDF document. In this example we will see how simple it is to integrate it to our NodeJs project.

## The workflow

Let's say we want to generate a PDF document that has a static branded first page, then a dynamic body, that can be anything from .docx, .xlsx, .pptx, images, 
text to even web pages that we'll convert to PDF and merge it with our pre-made title page. Then we will compress and encrypt the generated document with a password 
for secure sharing with the intended audience.

## Let's begin

First, let's set up a simple [NodeJs webserver](https://nodejs.org/en/docs/guides/getting-started-guide/) where we will put our conversion logic. 
Create a directory for our project and add a file called convertapi-nodejs.js:

```javascript
//Load HTTP module
const http = require("http");
const hostname = '127.0.0.1';
const port = 3000;

//Create HTTP server and listen on port 3000 for requests
const server = http.createServer((req, res) => {
  //Set the response HTTP header with HTTP status and Content type
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('ConvertAPI in action!');
});

//listen for request on port 3000, and as a callback function have the port listened on logged
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

Then, let's install a [ConvertAPI NodeJS library](https://github.com/ConvertAPI/convertapi-node) using npm:

`npm install convertapi --save`

Then, lets create a folder inside our project's root directory called "files", and put our source files there. 
You can also convert your files by passing a file URL if the file is hosted on a server, for more information about file upload options please refer to [our docs](https://www.convertapi.com/doc/upload).
In our example we will place two files into the "Files" folder and convert from there. 
Let's add our styled first page called "first-page.pdf" and a sample docx file for demonstration purposes called "sample.docx". So our "Files" folder looks something like this:





Now let's apply our first conversion [DOCX -> PDF](https://www.convertapi.com/docx-to-pdf). Simply put this code snippet at the end of our file:

```javascript
var convertapi = require('convertapi')('your-secret-here');
convertapi.convert('pdf', {
	File: './files/sample.docx'
}, 'docx').then(function(result) {
	result.saveFiles('./files');
});
```

Replace 'your-secret-here' string with [your secret key](https://help.convertapi.com/en/article/how-to-create-a-free-account-2wr644/) and it will run the conversion immediately once we run the `node convertapi-node.js` command from CMD.

Secondly, let's merge our predefined styled PDF intro page with the converted DOCX file into a single PDF using the [PDF -> MERGE](https://www.convertapi.com/pdf-to-merge) conversion:


# Convert documents to and from PDF with NodeJs

Many progressive web apps nowadays are built using serverless architecture where complex computations and machine resources are hosted by a third-party service, 
eliminating the need for server software and hardware management by the developer. 
ConvertAPI is a cloud based, platform independent market leader when it comes to processing documents on demand.
It allows you to convert images, MS office documents, ebooks, emails, web pages to PDF as well as merge, encrypt, compress and apply multiple advanced operations to the
final PDF document. In this example we will see how simple it is to integrate it to our NodeJs project.

## The workflow

Let's say we want to generate a PDF document that has a static branded cover page, then a dynamic body, that can be anything from .docx, .xlsx, .pptx, images, 
text to even web pages that we'll convert to PDF and merge it with our pre-made title page. Later on we will be able to compress, rotate, encrypt, archive the generated document as needed.

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

Now let's create a folder inside our project's root directory called "files", and put our source files there. 
You can also convert your files by passing a file URL if the file is hosted on a server, for more information about file upload options please refer to [our docs](https://www.convertapi.com/doc/upload).
In our example we will place two files into the "Files" folder and convert from there. 
Let's add our styled cover page called "first-page.pdf" and a sample docx file for demonstration purposes called "sample.docx". So our "Files" folder looks something like this:


----------------add folder structure image here------------------


Now let's apply our first conversion [DOCX -> PDF](https://www.convertapi.com/docx-to-pdf). Simply put this code snippet inside the `http.createServer((req, res)` function so it is run when we visit the page:

```javascript
var convertapi = require('convertapi')('your-secret-here');
convertapi.convert('pdf', {
	File: './files/sample.docx'
}, 'docx').then(function(result) {
	result.saveFiles('./files/document-body.pdf');
});
```

Replace 'your-secret-here' string with [your secret key](https://help.convertapi.com/en/article/how-to-create-a-free-account-2wr644/) and it will run the conversion immediately once we run the `node convertapi-node.js` command from CMD and visit http://127.0.0.1:3000/.

Secondly, let's merge our predefined styled PDF intro page with the converted DOCX file into a single PDF using the [PDF -> MERGE](https://www.convertapi.com/pdf-to-merge) conversion. Our extended method will look like this:

```javascript
var convertapi = require('convertapi')('your-secret-here');
convertapi.convert('pdf', {
	File: './files/sample.docx',
}).then(function(result) {
	return result.file.save('./files/document-body.pdf');
}).then(function(file) {
	console.log("File saved: " + file);
	convertapi.convert('merge', {
		Files: ['./files/first-page.pdf', file]
	}, 'pdf').then(function(mergedResult) {
		return mergedResult.file.save('./files/result.pdf');
	}).then(function(file) {
		console.log("Merged file: " + file);
	});
}).catch(function(e) {
	console.error(e.toString());
});
```

That's it, we have converted a DOCX file to PDF and then merged it with our cover page programatically using NodeJs. You can apply further conversions like [PDF Compress](https://www.convertapi.com/pdf-to-compress), [PDF Encrypt](https://www.convertapi.com/pdf-to-encrypt), [archive PDF to PDFa](https://www.convertapi.com/pdf-to-pdfa), [generate a thumbnail preview](https://www.convertapi.com/pdf-to-thumbnail) and so on in the same manner. To get the most performance benefits you can chain multiple conversions using [conversion workflows](https://www.convertapi.com/doc/workflows). You can find a complete list of conversion parameters under [conversions section](https://www.convertapi.com/conversions). Simply select your conversion and you will see an interactive demo with all available parameters for the conversion. Don't forget to grab the auto-generated code snippet at the bottom!


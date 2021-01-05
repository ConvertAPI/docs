Many progressive web apps nowadays are built using a serverless architecture where complex computations and machine resources are hosted by a third-party service, 
eliminating the need for server software and hardware management by the developer. 
ConvertAPI is a cloud-based, platform-independent service that handles document processing on demand.
It allows you to convert [images](https://www.convertapi.com/image-api), [MS office documents](https://www.convertapi.com/ms-office-api), [ebooks](https://www.convertapi.com/ebooks-api), [emails](https://www.convertapi.com/email-api), [web pages](https://www.convertapi.com/web-api) to PDF as well as [merge](https://www.convertapi.com/pdf-to-merge), [encrypt](https://www.convertapi.com/pdf-to-encrypt), [compress](https://www.convertapi.com/pdf-to-compress), and apply multiple advanced operations to the
final PDF document. In this example, we will see how simple it is to integrate it to our NodeJs project.

## The workflow

In this quick demo we want to generate a PDF document that has a static cover page and a dynamic body, that can be anything from .docx, .xlsx, .pptx, images, 
text to even web pages that we'll convert to PDF and merge it with our pre-made title page. Later on, we will be able to compress, rotate, encrypt, archive the generated document as needed.

## Let's begin

First, let's create a directory for our project and add a file called convertapi-nodejs.js. For this project to work on your environment you will need [NodeJs](https://nodejs.org/en/download/) installed. Then, let's add a [ConvertAPI NodeJS library](https://github.com/ConvertAPI/convertapi-node) using npm:

`npm install convertapi --save`

Now let's create a folder inside our project's root directory called "files", and put our source files there. 
You can also convert files by passing a file URL if the file is hosted on a server, for more information about file upload options please refer to [our docs](https://www.convertapi.com/doc/upload).
In our example, we will place two files into the "Files" folder and convert from there. 
Let's add our styled cover page called "first-page.pdf" and a sample DOCX file that will appear as our PDF's content called "sample.docx". So our "Files" folder looks something like this:


![Folder structure](https://user-images.githubusercontent.com/62603039/103544276-818e7000-4ea8-11eb-9c49-83c4fb03e326.png)

We will apply our first [DOCX -> PDF](https://www.convertapi.com/docx-to-pdf) conversion (you don't need to have MS Office installed on your machine to make this conversion). Simply put this code snippet inside the convertapi-nodejs.js file:

```javascript
var convertapi = require('convertapi')('your-secret-here');
convertapi.convert('pdf', {
	File: './files/sample.docx'
}, 'docx').then(function(result) {
	result.saveFiles('./files/document-body.pdf');
});
```

Replace 'your-secret-here' string with [your secret key](https://help.convertapi.com/en/article/how-to-create-a-free-account-2wr644/) and it will run the conversion immediately once we run the `node convertapi-node.js` command from CMD.

Secondly, let's merge our styled cover page with the converted DOCX file into a single PDF using the [PDF -> MERGE](https://www.convertapi.com/pdf-to-merge) conversion. Our extended method will look like this:

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

That's it, we have converted a DOCX file to PDF and then merged it with our cover page programmatically using NodeJs. You can apply further conversions like [PDF Compress](https://www.convertapi.com/pdf-to-compress), [PDF Encrypt](https://www.convertapi.com/pdf-to-encrypt), [archive PDF to PDF/A](https://www.convertapi.com/pdf-to-pdfa), [generate a thumbnail preview](https://www.convertapi.com/pdf-to-thumbnail) and so on in the same manner. To get the most performance benefits you can chain multiple conversions using [conversion workflows](https://www.convertapi.com/doc/workflows). You can find a complete list of conversion parameters under [conversions section](https://www.convertapi.com/conversions). Simply select your conversion and you will see an interactive demo with all available parameters for the conversion. Don't forget to grab the auto-generated code snippet at the bottom!

![NodeJS code snippet](https://user-images.githubusercontent.com/62603039/103544270-7b988f00-4ea8-11eb-8b29-eb907af8053d.png)


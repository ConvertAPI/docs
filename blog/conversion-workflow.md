---
title: Build a custom conversion workflow and improve performance with Conversion Chaining
author_name: Kostas
short_description: ConvertAPI provides a flexible solution for building custom conversion flows. You can process your files by applying multiple conversions and other file manipulations using conversion chaining. This best-practice driven REST API approach improves performance and gives you full control over file processing at any stage of the flow. 
meta_description: Conversion workflow is a powerful feature improving the performance and flexibility of our REST API conversion service.
tags: feature,blog post
date_created: 2020-05-20
---
<!--tags: blog post,new,feature,bug,improvements,api,integration-->

One of our core conversion service features is conversion workflow. 
We've seen so many services implementing it in wrong, anti-pattern ways that make the code slow and hardly reusable so we decided to describe it in detail.

We solved this issue by what we call the REST API Conversion Workflows. 
It simply means applying multiple conversions to a file uploaded to our server. You can process the file over and over again by calling appropriate conversion methods via REST API. 
There is no need to download a partial result and reupload it. The diagram below describes the process of the real-world example we will discuss in a moment.

![Conversion workflow scheme](https://user-images.githubusercontent.com/62603039/82549001-e9d05180-9b64-11ea-8dfa-3e2a9e59869c.png)

## Why use conversion workflows?

Conversion workflows not only improve the performance but also provide the flexibility to manage your file conversions step by step. This way, you gain the ability to handle any exceptions that might occur along the way. 
This particular REST API pattern allows you to continue the communication from where it failed without the need to rerun the whole process again. Now let's dive deep into a real-world demo!

## Real-world example

For our demo, we will use a pretty common JPG to PDF conversion example. This conversion produces multiple PDF files as 
each JPG is converted into PDF. Let's say you want to merge the PDFs into a single file and download it. 
You can achieve that by uploading a bunch of source files and specifying further conversions.

We'll use Node.js for this particular example, although all of our libraries support this feature. For other programming languages libraries, please refer to [our libraries](https://www.convertapi.com/doc/libraries). 

```javascript
let convertapi = require('convertapi')(process.env.CONVERT_API_SECRET)
let jpgPaths = ['first.jpg', 'second.jpg', 'third.jpg']
let pdfs = jpgPaths.map(j => convertapi.convert('pdf', { File: `./images/${j}` }))
Promise.all(pdfs).then(p => convertapi.convert('merge', { Files: p }))
  .then(
    r => {
          r.file.save('merged.pdf')
          console.log('The images has been merged to merge.pdf file.')
          }
        )
```

Run this [code snippet](https://repl.it/@ConvertAPI/JPG-greater-PDF-greater-MERGE) on Repl.it

Another common example is to convert multiple DOCX documents into PDFs, merge them into a single PDF, and finally encrypt the merged result with a "testpassword" password.

```javascript
let convertapi = require('convertapi')(process.env.CONVERT_API_SECRET)
let docPaths = ['document1.docx', 'document2.docx']
let pdfs = docPaths.map(j => convertapi.convert('pdf', { File: `./documents/${j}` }))
Promise.all(pdfs)
  .then(p => convertapi.convert('merge', { Files: p }))
  .then(p => convertapi.convert('encrypt', { File: p, PdfUserPasswordNew : 'testpassword' }))
  .then(
    r => {
          r.file.save('encrypt.pdf')
          console.log('The documents has been merged, encrypted and saved to encrypt.pdf file.')
          }
        )
```

Run this [code snippet](https://repl.it/@ConvertAPI/Chaining-DOCX-to-PDF-then-MERGE-finally-ENCRYPT) on Repl.it

The pure REST API workflow documentation can be found in [our documentation](https://www.convertapi.com/doc/workflows) section.

Please note that the ```StoreFile=true``` parameter must be set when calling the conversion endpoint directly (not using any library) to store the file on our server for multiprocessing.

## Conclusion

To put it in a nutshell, conversion changing is the best practice for processing documents with the performance and flexibility perks. 
It is available in all of our libraries. Use this approach to write a clean, reusable, and performance-oriented code! 

Read more about conversion workflows in our [documentation](https://www.convertapi.com/doc/workflows). 

Happy coding!
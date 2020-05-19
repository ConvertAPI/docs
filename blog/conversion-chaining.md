One of our core conversion service features is conversion chaining. 
We've seen so many services implementing it in wrong, anti-pattern ways that make the code slow and hardly reusable so we decided to describe it in detail.

We solved this issue by what we call a REST API Conversion Chaining. 
It simply means applying multiple conversions to a file uploaded to our server. You can process the file over and over again by calling appropriate conversion methods via REST API. 
There is no need to download a partial result and reupload it. The diagram below describes the process of the real-world example we will discuss in a moment.

![Data flow diagram](https://user-images.githubusercontent.com/62603039/82210296-74bc0c80-9917-11ea-9164-eb951413eea0.png)

## Why use conversion chaining?

Conversion chaining not only improves the performance but also provides the flexibility to manage your file conversions step by step. This way, you gain the ability to handle any exceptions that migh occure along the way. 
This particular REST API pattern allows you to continue the communication from where it failed without the need to rerun the whole process again. Now let's dive deep into a real-world demo!

## Real-world example

For our demo we will use a pretty common PDF to JPG conversion example. This conversion produces multiple files as 
each PDF page is split into a separate JPEG image. Let's say you want to ZIP the images into a single archive and download it. 
You can achieve that by uploading a source file and specifying further conversions.

We'll use Node.js for this particular example, although all of our libraries support this feature. 
For other programming languages, please refer to [our docs](https://www.convertapi.com/doc/chaining).

Please note that the ```StoreFile=true``` parameter must be set when calling the conversion endpoint to store the file on our server for multiprocessing.

```javascript
let convertapi = require('convertapi')(process.env.CONVERT_API_SECRET)
let jpgPaths = ['first.jpg', 'second.jpg', 'third.jpg']
let pdfs = jpgPaths.map(j => convertapi.convert('pdf', { File: `./images/${j}` }))
Promise.all(pdfs).then(p => convertapi.convert('merge', { Files: p }))
  .then(r => r.file.save('merged.pdf'))
```

Run this [code snippet](https://repl.it/@ConvertAPI/JPG-greater-PDF-greater-MERGE) on Repl.it

## Conclusion

To put it in a nutshell, conversion changing is the best practice for processing documents with the performance and flexibility perks. 
It is available in all of our libraries. Use this approach to write a clean, reusable and performance-oriented code! 

Read more about conversion chaining in our [documentation](https://www.convertapi.com/doc/chaining). 

Happy coding!

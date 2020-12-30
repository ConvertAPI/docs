# How to convert HTML + CSS to PDF using PHP?

HTML to PDF conversion might seem like a regular task, but it can be difficult to implement and maintain making your project much more complex. 
Thus, many nowadays solutions come from a 3rd party rigid and robust service providers.
We are going to use a simple API call to take care of the conversion.

Let's begin by installing a [ConvertAPI PHP Client](https://github.com/ConvertAPI/convertapi-php):

`composer require convertapi/convertapi-php`

_Note: if you don't want to use Composer, please follow the [manual installation guide](https://github.com/ConvertAPI/convertapi-php#manual-installation)._

Once you have the library installed, simply run this code snippet:

```
ConvertApi::setApiSecret('your-secret-here');
$result = ConvertApi::convert('pdf', [
        'File' => '/path/to/my_file.html',
    ], 'html'
);
$result->saveFiles('/path/to/result/dir');
```

That's it, just replace [your secret](https://help.convertapi.com/en/article/how-to-create-a-free-account-2wr644/) and path to your file and it should work straight away. 

However, if you want a more advanced conversion with control over whether to run javascript on the web page, 
remove cookie warning popups, ads, etc please refer to the [complete guide including an interactive demo](https://www.convertapi.com/html-to-pdf). 
You will also find an auto-generated snippet at the bottom of the page!

Quick tip: if you want to convert a web page by passing a **web page URL** instead of an HTML file, please refer to the [WEB to PDF guide](https://www.convertapi.com/web-to-pdf).

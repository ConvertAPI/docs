---
title: Convert Apple iWork documents to PDF and Images programatically
author_name: Jonas
short_description: ConvertAPI provides a flexible solution for converting Apple iWork suite files (key, numbers, pages) to image or common MS Office file formats with any programming language of your choice. 
meta_description: ConvertAPI provides a solution for converting Apple iWork suite files (key, numbers, pages) to image or common MS Office file formats programatically.
tags: new,api
date_created: 2019-01-04
---
<!--tags: blog post,new,feature,bug,improvements,api,integration-->

Apple iWork suite is a set of applications meant to work with documents, spreadsheets, and presentations.
It is built specifically to use on macOS and iOS operating systems, which makes it difficult to automate and maintain.
The more flexible, cross-platform option is the MS Office suite, as there are many tools and services supporting formats like .docx, .xlsx, .pptx, etc.

For this purpose we present you our new [iWork API](https://www.convertapi.com/apple-iwork-api), that provides fast and secure conversions to either images, PDFs, or MS Office file formats:

| Convert from  | Convert to                     |
| :-- | :-- |
| key           | [jpg](https://www.convertapi.com/key-to-jpg), [pdf](https://www.convertapi.com/key-to-pdf), [png](https://www.convertapi.com/key-to-png), [ppt](https://www.convertapi.com/key-to-ppt), [pptx](https://www.convertapi.com/key-to-pptx), [tiff](https://www.convertapi.com/key-to-tiff) |
| numbers       | [csv](https://www.convertapi.com/numbers-to-csv), [pdf](https://www.convertapi.com/numbers-to-pdf), [xls](https://www.convertapi.com/numbers-to-xls), [xlsx](https://www.convertapi.com/numbers-to-xlsx) |
| pages         | [doc](https://www.convertapi.com/pages-to-doc), [docx](https://www.convertapi.com/pages-to-docx), [pdf](https://www.convertapi.com/pages-to-pdf), [rtf](https://www.convertapi.com/pages-to-rtf), [txt](https://www.convertapi.com/pages-to-txt) |

Using our [iWork API](https://www.convertapi.com/apple-iwork-api) you are now able to convert iWork suite files programmatically using any OS and any programming language of your choice. Let's see some examples of the most popular programming languages.

## iWorks to PDF conversion examples

You can download these example files (source and destination) and check the conversion quality:
- [example .pages file](/samples/iworks/example.pages) -> [converted PDF](/samples/iworks/example-pages.pdf) 
- [example .numbers file](/samples/iworks/example.numbers) -> [converted PDF](/samples/iworks/example-numbers.pdf) 
- [example .key file](/samples/iworks/example.key) -> [converted PDF](/samples/iworks/example-key.pdf) 

![image](https://user-images.githubusercontent.com/62603039/108726207-d311bd80-752f-11eb-9d97-01c85e27901e.png)


## Convert iWork Pages to MS Office Word using PHP

In this example, we will show a quick code demo for converting the iWork Pages file to a .docx file format using [ConvertAPI PHP Client](https://github.com/ConvertAPI/convertapi-php).
Find a complete list of pages to .docx conversion properties under the developer mode of our [PAGES to DOCX API](https://www.convertapi.com/pages-to-docx) live demo tool:

```php
ConvertApi::setApiSecret('<YOUR SECRET HERE>');
$result = ConvertApi::convert('docx', [
        'File' => '/path/to/my_file.pages',
    ], 'pages'
);
$result->saveFiles('/path/to/result/dir');
```

## Convert iWork Key to MS Office PowerPoint using C#

In the following example, we will show a quick code demo for converting the iWork Pages file to a .docx file format using [ConvertAPI C# Client](https://github.com/ConvertAPI/convertapi-dotnet).
Find a complete list of key to .pptx conversion properties under the developer mode of our [KEY to PPTX API](https://www.convertapi.com/key-to-pptx) live demo tool:

```csharp
var convertApi = new ConvertApi("<YOUR SECRET HERE>");
var convert = await convertApi.ConvertAsync("key", "pptx",
    new ConvertApiFileParam("File", @"C:\path\to\my_file.key")
);
await convert.SaveFilesAsync(@"C:\converted-files\");
```

## Convert iWork Numbers to MS Office Excel using NodeJS

In the last example, we will show a quick code demo for converting the iWork Numbers file to a .xlsx file format using [ConvertAPI Node.js Client](https://github.com/ConvertAPI/convertapi-node).
Find a complete list of numbers to .xlsx conversion properties under the developer mode of our [NUMBERS to XLSX API](https://www.convertapi.com/numbers-to-xlsx) live demo tool:

```javascript
var convertapi = require('convertapi')('<YOUR SECRET HERE>');
convertapi.convert('xlsx', {
    File: '/path/to/my_file.numbers'
}, 'numbers').then(function(result) {
    result.saveFiles('/path/to/dir');
});
```

## Conclusion

Each conversion provides a bunch of useful conversion options. 
You can find the complete list of conversions and their parameters as well as auto-generated code snippets using our interactive [Live Demo](https://www.convertapi.com/apple-iwork-api) tool.
Simply pick a [library](https://www.convertapi.com/doc/libraries) for your programming language, copy the [auto-generated code snippet](https://www.convertapi.com/key-to-jpg), and you are good to go!
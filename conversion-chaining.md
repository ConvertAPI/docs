Converted files that are stored on convertapi.com server can be accessible for further conversion operations. This method allows conversion chaining, without increased network load. Example: conversion PDF to JPG produces as many files as there are pages in PDF file. If these files are stored on the server and links to the files are passed to ZIP converter, result will be one ZIP file with JPG files of each PDF page. The `StoreFile=true` parameter must be set when calling conversion endpoint.

The example below converts PDF to JPG and store result files on server for chaining.

### Convert PDF to JPG - chain #1
```
[POST]
https://v2.convertapi.com/convert/pdf/to/jpg?Secret=XXX
{
    "Parameters": [
        {
            "Name": "File",
            "FileValue": {
                "Name": "my_file.pdf",
                "Data": "--Base64 encoded file content--"
            }
        },
        {
            "Name": "StoreFile",
            "Value": true
        }
    ]
}
```
```
[response]
{
    "ConversionCost": 4,
    "Files": [
        {
            "FileName": "test.jpg",
            "FileSize": 526012,
            "Url": "https://v2.convertapi.com/d/d57646acef91155eb7a57376e9cf8d55/test.jpg"
        },
        {
            "FileName": "test-2.jpg",
            "FileSize": 500216,
            "Url": "https://v2.convertapi.com/d/dfaca13bc861c529d00d22cfacf71c63/test-2.jpg"
        },
        {
            "FileName": "test-3.jpg",
            "FileSize": 516911,
            "Url": "https://v2.convertapi.com/d/4c78541c67d66045dfe5378dc8852ae5/test-3.jpg"
        }
    ]
}
```
Now we can get all result files from above response and send them to ZIP using example below.
### ZIP all JPG files - chain #2
```
[POST] 
https://v2.convertapi.com/convert/jpg/to/zip?Secret=XXX
{
    "Parameters": [
        {
            "Name": "Files",
            "FileValues": [
                {
                    "Url": "https://v2.convertapi.com/d/d57646acef91155eb7a57376e9cf8d55/test.jpg"
                },
                {
                    "Url": "https://v2.convertapi.com/d/dfaca13bc861c529d00d22cfacf71c63/test-2.jpg"
                },
                {
                    "Url": "https://v2.convertapi.com/d/4c78541c67d66045dfe5378dc8852ae5/test-3.jpg"
                }
            ]
        },
        {
            "Name": "StoreFile",
            "Value": true
        }
    ]
}
```
```
[response]
{
    "ConversionCost": 1,
    "Files": [
        {
            "FileName": "test.zip",
            "FileSize": 1543732,
            "Url": "https://v2.convertapi.com/d/2f742a059ab5ae601f41f4503bb2a7f5/test.zip"
        }
    ]
}
```

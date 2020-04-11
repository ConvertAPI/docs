Every conversion request call must be authenticated with `secret` or `token` and submited as `query parameter`. More detailed authentication methods are covered in [Authentication](https://www.convertapi.com/doc/auth) section. All supported [file format](https://www.convertapi.com/doc/supported-formats) conversions are provided here.

### Conversion using just URL

When files or web pages are accessible from the Internet it is enough to open a link to convert them. 

#### Conversion web url to PDF example
```
[GET/POST]
https://v2.convertapi.com/convert/web/to/pdf?download=inline&secret=XXX&url=http%3A%2F%2Fexample.com
```
```
[response]
PDF file contents displayed in a browser
```
URL passed as a query parameter must be [percentage encoded](https://en.wikipedia.org/wiki/Percent-encoding) (e.g. http://example.com should be encoded as http%3A%2F%2Fexample.com).

#### DOCX conversion to PDF example
```
[GET/POST]
https://v2.convertapi.com/convert/docx/to/pdf?download=inline&secret=XXX&file=http%3A%2F%2www.baltsoft.com/files/doc-demo.docx
```
```
[response]
PDF file contents displayed in a browser
```
Learn more about GET method request conversions in [Virtual File Server](https://www.convertapi.com/doc/virtual-file-server) section.

### Conversion using JSON format
#### DOC conversion to PDF using JSON
```
[POST] 
https://v2.convertapi.com/convert/doc/to/pdf?Secret=XXX
{
    "Parameters": [
        {
            "Name": "File",
            "FileValue": {
                "Name": "my_file.doc",
                "Data": "--Base64 encoded file content--"
            }
        }
    ]
}
```
```
[response]
{
    "ConversionTime": 2,
    "Files": [
        {
            "FileName": "my_file.pdf",
            "FileSize": 523672,
            "FileData": "--Base64 encoded file content--"
        }
    ]
}
```

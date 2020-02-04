Query information about converters, their supported formats and account data.

It is possible to get an information about all supported conversions and formats with parameter descriptions in JSON or XML formats.

### List all information
```
[GET]
https://v2.convertapi.com/info
```
### List information about conversion from DOC to PDF
```
[GET]
https://v2.convertapi.com/info/doc/to/pdf
```
### List information about conversion from any format to PDF
```
[GET]
https://v2.convertapi.com/info/*/to/pdf
```
### List information about conversion from PDF to any format
```
[GET]
https://v2.convertapi.com/info/pdf/to/*
```
###List information about converter ExcelToJpg
```
[GET]
https://v2.convertapi.com/info/converter/ExcelToJpg
```
### Checks if conversion is supported
```
[GET]
https://v2.convertapi.com/info/canconvert/doc/to/pdf
````
Response:
Returns HTTP status 200 - supported, 404 - not supported

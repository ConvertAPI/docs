In this documentation section are covered all content types and schemes that are supported by ConvertAPI.

## Request
### application/json
File data must be encoded with Base64 encoding, provided as URL or uploaded File ID.

#### DOC to PDF example
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
#### Merge PDF scheme example (multiple source files)
```
[POST]
https://v2.convertapi.com/convert/pdf/to/merge?Secret=XXX
{
    "Parameters": [
        {
            "Name": "StoreFile",
            "Value": "true"
        },
        {
            "Name": "PdfVersion",
            "Value": "1.7"
        },
        {
            "Name": "Files",
            "FileValues": [
                {
                    "Name": "file.pdf",
                    "Data": "--Base64 encoded file content--"
                },
                {
                    "Url": "http://example.com/myfile.docx"
                },
                {
                    "Id": "0ba132ddd698aaeafcf19ec0015e10e0"
                }
            ]
        }
    ]
}
```
### multipart/form-data
Each request parameter must be in separate part. If there is an array type parameter, index must be appended to parameter name e.g. Files[0], Files[1], Files[2] etc.
#### DOC to PDF example
```
[POST] 
https://v2.convertapi.com/convert/doc/to/pdf?secret=XXXX HTTP/1.1
Content-Type: multipart/form-data; boundary=----7MA4YWxkTrZu0gW

------7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="StoreFile"

true
------7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="File"; filename="my_file.doc"
Content-Type: 

--FILE DATA--
------7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="DocumentTitle"

Test title
------7MA4YWxkTrZu0gW--
```
#### application/octet-stream
Most bandwidth efficient way to convert file is to pass file content as a request body. Also this content type could be used for stream processing. Request header must contain field `Content-Disposition: attachment; filename="my_file.doc"` with the file name and correct file extension. Conversion parameters can be set throw URL query.

### Query parameters
Using query parameters it is possible to convert file which is accessible by URL or uploaded File ID.

DOCX to PDF example
```
[GET/POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&File=http://example.com/myfile.docx&StoreFile=true
```
If there is an array type parameter, index must be appended to parameter name e.g. Files[0], Files[1], Files[2] etc.

## Response

Response headers and body contains this information:

* `ConversionTime` - time in seconds that took to convert file. In this amount of seconds your balance will be decreased after conversion.
* `FileName` - name of converted file.
* `FileSize` - converted file size in bytes.
* `FileData` - converted file content.
* `FileUrl` - link to converted file if `StoreFile` parameter is set to `true`.

### application/json
Single file result example
[response]
```
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
### application/xml
XML scheme is analogous to JSON.
```
<Conversion xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
<ConversionTime>2</ConversionTime>
<Files>
    <File>
        <FileName>my_file.pdf</FileName>
        <FileSize>522579</FileSize>
        <FileData>--Base64 encoded file content--</FileData>
        <Url i:nil="true" />
    </File>
</Files>
</Conversion>
```
### multipart/mixed
Each part contains converted file data or URL to the file.

Single file result example
```
[response]
--43cf1475-ab15-4c6b-b5ee-e2cbcedfe92f
ConversionTime: 3
Content-Type: application/octet-stream
Content-Disposition: attachment; filename="my_file.pdf"; size=8475

--FILE CONTENT--
                
--43cf1475-ab15-4c6b-b5ee-e2cbcedfe92f--
```
### application/octet-stream
Response body is result file content. File name can be found in `content-disposition` header field. Can be used with converters that produce only one file result.

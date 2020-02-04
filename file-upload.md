When source file must be converted multiple times, conversion performance can be increased by uploading file once and converting it multiple times without uploading it once again. Uploaded file will be stored in convertapi.com server for maximum period of 3 hours and will be accessible by secret URL with UUID. In conversion request file can be referred by the File ID, which will be given after file upload. Another benefit of uploaded file is that conversion request can be formed just by URL query (no need for multipart formatter).

### File upload request

File upload response content type is controlled by "Accept" header field value. Default "Accept" header field value is "application/json". If request header has "Accept: text/plain" field, response body will contain plain File ID string. This response format is useful when there are no JSON or XML parsers.

#### application/octet-stream (preferred format)

Raw file data upload is most **simple and efficient** upload type. Must be provided content-disposition header field with the file name or **filename** query parameter.
```
[POST]
https://v2.convertapi.com/upload 
Content-Disposition: inline; filename="my_file.doc"

--FILE DATA--
```
```
[response]
{
    "FileId": "25811safe8e61dd3f51ef00ee5f58b92",
    "FileName": "my_file.doc",
    "FileExt": "doc"
}
```
#### multipart/form-data
There can be one and only part with file data.
```
[POST]
https://v2.convertapi.com/upload 
Content-Disposition: inline; filename="my_file.doc"

Content-Type: multipart/form-data; boundary=----7MA4YWxkTrZu0gW

------7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="FileData"; filename="my_file.doc"
Content-Type:

--FILE DATA--
------7MA4YWxkTrZu0gW--
```
```
[response]
{
    "FileId": "25811safe8e61dd3f51ef00ee5f58b92",
    "FileName": "my_file.doc",
    "FileExt": "doc"
}
```
### Upload from remote server
If file is accessible by the URL, it can be uploaded directly from it's location.
```
[POST]
https://v2.convertapi.com/upload?url=http%3A%2F%2Fexample.com%2Ffile.doc&FileName=my_file.doc
```
```
[response]
{
    "FileId": "25811safe8e61dd3f51ef00ee5f58b92",
    "FileName": "my_file.doc",
    "FileExt": "doc"
}
```
Additionally can be provided "HeaderName" and "HeaderValue" parameters, needed for integration with third party systems like Google Drive.
### HTTP response codes
* **200** Upload completed successfully.
* **500** Unable to download remote file.

### Actions with the uploaded file

#### Conversion
```
[GET/POST]
https://v2.convertapi.com/convert/doc/to/pdf?Secret=XXX&File=25811safe8e61dd3f51ef00ee5f58b92
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
#### Delete uploaded file
If file is no longer required it can be deleted.
```
[DELETE]
https://v2.convertapi.com/d/25811safe8e61dd3f51ef00ee5f58b92
```

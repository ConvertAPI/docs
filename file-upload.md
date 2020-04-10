When source files must be converted multiple times, conversion performance can be increased by uploading files once and converting it multiple times without uploading it again. The uploaded file will be stored in convertapi.com server for maximum period of 3 hours and will be accessible by secret URL with UUID. In conversion request file can be referred by the File ID, which will be returned after a successful file upload. Another benefit of the uploaded file is that conversion requests can be formed just by the URL query (no need for the multipart formatter).

### File upload request

The file upload response content type is controlled by the "Accept" header field value. Default "Accept" header field value is "application/json". If the request header has the "Accept: text/plain" value, the response body will contain plain File ID string. This response format is useful when there are no JSON or XML parsers.

#### application/octet-stream (preferred format)

Raw file data upload is the most **simple and efficient** upload type. The Content-disposition header field must be provided with the file name or **filename** query parameter.
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
There can be one and only one part with file data.
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
If the file is accessible by the URL, it can be uploaded directly from its location by passing the URL instead of the file itself.
```
[POST]
https://v2.convertapi.com/upload?url=http%3A%2F%2Fexample.com%2Ffile.doc&FileName=my_file.doc
```
In addition to this, any "HeaderName" and "HeaderValue" parameters can be provided, needed to authenticate to a third-party system (for example trying to upload a private file from Google Drive). These header fields will be added when making a request to a third-party system.

```
[response]
{
    "FileId": "25811safe8e61dd3f51ef00ee5f58b92",
    "FileName": "my_file.doc",
    "FileExt": "doc"
}
```

#### HTTP response codes
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
If the file is no longer required it can be deleted. Otherwise, it will be automatically deleted after 3 hours.
```
[DELETE]
https://v2.convertapi.com/d/25811safe8e61dd3f51ef00ee5f58b92
```

When source file must be converted multiple times, conversion performance can be increased by uploading file once and converting it multiple times without uploading it once again. Uploaded file will be stored in convertapi.com server for maximum period of 3 hours and will be accessible by secret URL with UUID. In conversion request file can be referred by the File ID, which will be given after file upload. Another benefit of uploaded file is that conversion request can be formed just by URL query (no need for multipart formatter).

### File upload request

File upload response content type is controlled by "Accept" header field value. Default "Accept" header field value is "application/json". If request header has "Accept: text/plain" field, response body will contain plain File ID string. This response format is useful when there are no JSON or XML parsers.

**application/octet-stream (preferred format)**

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

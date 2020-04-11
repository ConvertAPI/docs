ConvertAPI can be used as a virtual file server for all your files or web pages that need to be converted. The file is being converted on-demand whenever user clicks on the link. The result can be displayed in a web browser or downloaded.

### Parameter "download"

The download parameter is mandatory and must be set in order to get the file as a request result.

* **download=inline** - conversion result will be displayed in a browser
* **download=attachment** - conversion result will be downloaded

Parameter **download** controls response "content-type" and "content-dispositon" header values:

| Value of "download" parameter      | content-type          | 	content-dispositon |
|:------------- |:-------------|:-----|
|not set     | default| not set|
|attachment     | application/octet-stream| attachment|
|inline     | application/octet-stream| inline|

### Link examples
```
<a href="https://v2.convertapi.com/convert/web/to/pdf?token=XXX&download=inline&url=http%3A%2F%2Fexample.com%2F" rel="nofollow">View page as PDF</a>
<a href="https://v2.convertapi.com/convert/web/to/pdf?token=XXX&download=attachment&url=http%3A%2F%2Fexample.com%2F" rel="nofollow">Save page as PDF</a>
<a href="https://v2.convertapi.com/convert/docx/to/pdf?token=XXX&file=http%3A%2F%2Fexample.com%2Fmy_file.docx" rel="nofollow">Conversion response in XML format</a>
```
URL passed as a query parameter must be percentage encoded (e.g. http://example.com should be encoded as http%3A%2F%2Fexample.com).

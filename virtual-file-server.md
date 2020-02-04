ConvertAPI can be used as a virtual file server for all your files or web pages that needs to be converted. File is getting converted on demand, when a user clicks on the link. Result can be displayed in a web browser or downloaded.

### Parameter "download"

Download parameter is mandatory and must be set in order to get file as request result.

* **download=inline** - conversion result will be displayed in a browser
* **download=attachment** - conversion result will be downloaded

Parameter **download** controls response "content-type" and "content-dispositon" header value:

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
URL passed as a query parameter must be [percentage encoded](https://en.wikipedia.org/wiki/Percent-encoding) (from http://example.com to http%3A%2F%2Fexample.com).

Asynchronous file conversions are made by setting the `Async` parameter to `True`. The response of the asynchronous conversion contains `JobId` which could be used to poll the result. The ConvertAPI supports two types of asynchronous results: - `Poll` and `Push` (WebHooks).

## Poll

**Asynchronous conversion request**

```
[POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&Async=true&File=http://example.com/myfile.docx
```

**Response**

```
{"JobId": "d3bd2056-4330-4cf3-9b18-483a2412dd6b"}
```

Now using JobId it is possible to retrieve the finished conversion result or get the conversion status.

**Poll result request**

```
[GET]
https://v2.convertapi.com/job/d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

> Only one request of polling is accepted simultaneously, no concurrent poll requests are allowed. The second poll request will get a 503 status code if the first one is not finished yet. Also, there is a 5 seconds delay for every following request.

### Response HTTP status codes

* `200` Conversion is successful. Response is a conversion result.
* `202` Conversion is in progress.
* `404` `JobId` is invalid or the response is expired.
* `503` No concurrent poll requests are allowed.
* `5XX` Conversion error. Response is an error message.

## Push

The ConvertAPI uses WebHooks to make result pushing. When the conversion is completed the WebHook URL is called with `JobId`. The conversion request should include `WebHook parameter with URL` that should be called.

**Asynchronous conversion request**

```
[POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&Async=true&WebHook=http://www.example.com/WaitingForWebHook&File=http://example.com/myfile.docx
```

**Response**

```
{"JobId": "d3bd2056-4330-4cf3-9b18-483a2412dd6b"}
```

The response includes the `JobId` parameter. Once the conversion is complete the WebHook URL will be called with the corresponding `JobId` using `GET method`:

```
http://www.example.com/WaitingForWebHook?JobId=d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

The actual conversion result could be read using the received `JobId`.

**Poll result request**

```
[GET]
https://v2.convertapi.com/job/d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

> Only one request of polling is accepted simultaneously, no concurrent poll requests are allowed. The second poll request will get a 503 status code if the first one is not finished yet. Also, there is a 5 seconds delay for every following request.

### Response HTTP status codes

* `200` Conversion is successful. Response is a conversion result.
* `202` Conversion in progress.
* `404` `JobId` is invalid or response is expired.
* `503` No concurrent poll requests are allowed..
* `5XX` Conversion error. Response is an error message.

## Semi-Asynchronous

Semi-Asynchronous file conversions are useful when the connection to ConvertAPI is lost during large file conversions. To avoid repetitive conversions, please provide the `JobId` parameter with a self-generated `UUID (RFC 4122)`.

**Semi-Asynchronous conversion request**

```
[POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&JobId=d3bd2056-4330-4cf3-9b18-483a2412dd6b&File=http://example.com/myfile.docx
```

In case of a disrupted connection, treat this conversion as if it was an asynchronous conversion. You can retrieve the conversion results as described in the asynchronous conversion section.

## Delete job

If the job is no longer required it can be deleted using the DELETE request or it would be automatically deleted after a maximum of two hours.

**Delete job request**

```
[DELETE]
https://v2.convertapi.com/job/d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

### Response HTTP status codes
* `200` Deleted successfuly.
* `404` `JobId` is invalid or job is already deleted.
* `5XX` Delete error. Response is an error message.

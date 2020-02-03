Asynchronous file conversions are made by setting parameter `Async` to `True`. The response of the asynchronous conversion contains `JobId` which could be used to poll the result. The ConvertAPI support two types of asynchronous result - `Polling` and `WebHooks`.

## Polling

**Asynchronous conversion request**

```
[POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&Async=true&File=http://example.com/myfile.docx
```

**Response**

```
{"JobId": "d3bd2056-4330-4cf3-9b18-483a2412dd6b"}
```

Now using JobId it is possible to retrieve finished conversion result or get the conversion status.

**Poll result request**

```
[GET]
https://v2.convertapi.com/job/d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

> Only one request of pulling is accepted, no concurrent poll requests are allowed. The second pool request will get 503 status code if first is not finished. Also there is delay of 5 second for the seconds pool request.

### Response HTTP status codes

* `200` Conversion is successful. Response is a conversion result.
* `202` Conversion in progress.
* `404` `JobId` is invalid or response is expired.
* `503` No concurrent poll requests are allowed.
* `5XX` Conversion error. Response is an error message.

## WebHooks

The ConvertAPI support WebHooks, when conversion is done the WebHook URL is called with `JobId`. The conversion request should include `WebHook parameter with URL` which should be called.

**Asynchronous conversion request**

```
[POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&Async=true&WebHook=http://www.example.com/WaitingForWebHook&File=http://example.com/myfile.docx
```

**Response**

```
{"JobId": "d3bd2056-4330-4cf3-9b18-483a2412dd6b"}
```

The response includes `JobId` and when conversion is finished the WebHook URL will be called with the same `JobId` using `GET method`:

```
http://www.example.com/WaitingForWebHook?JobId=d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

Using received `JobId` the actual conversion result could be read.

**Poll result request**

```
[GET]
https://v2.convertapi.com/job/d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

> Only one request of pulling is accepted, no concurrent poll requests are allowed. The second pool request will get 503 status code if first is not finished. Also there is delay of 5 second for the seconds pool request.

### Response HTTP status codes

* `200` Conversion is successful. Response is a conversion result.
* `202` Conversion in progress.
* `404` `JobId` is invalid or response is expired.
* `503` No concurrent poll requests are allowed..
* `5XX` Conversion error. Response is an error message.

## Semi-Asynchronous

Semi-Asynchronous file conversions are useful when connection to ConvertAPI is lost during large file conversion. To avoid repetitive conversion, provide `JobId` parameter with self generated `UUID (RFC 4122)`.

**Semi-Asynchronous conversion request**

```
[POST]
https://v2.convertapi.com/convert/docx/to/pdf?Secret=XXX&JobId=d3bd2056-4330-4cf3-9b18-483a2412dd6b&File=http://example.com/myfile.docx
```

In case of disrupted connection treat this conversion as if it was asynchronous conversion. Retrieve conversion result like described in asynchronous conversion section.

## Delete job

If job is no longer required it can be deleted using DELETE request or it would be automatically deleted after maximum two hours.

**Delete job request**

```
[DELETE]
https://v2.convertapi.com/job/d3bd2056-4330-4cf3-9b18-483a2412dd6b
```

### Response HTTP status codes
* `200` Deleted successful.
* `404` `JobId` is invalid or already deleted.
* `5XX` Delete error. Response is an error message.

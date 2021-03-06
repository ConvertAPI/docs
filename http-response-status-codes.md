This is the list of all HTTP response status codes returned by ConvertAPI. The three-number code describes HTTP Status code and four number code shows additional information about the result in the response body. The example response body of authentication failure:

**Response Header**

```
HTTP status code 401
```

**Response body**

```
{
    "Code": 4013,
    "Message": "User credentials not set, secret or token must be passed."
}
```

### Result
* `200 OK` Conversion completed successfully.

### Malformed request
* `400 Bad Request` Request does not provide all data to execute the conversion.
  * `4000` Parameter validation error.
  * `4001` No content disposition provided.
  * `4002` Bad JSON format.
  * `4005` File encoded in Base64 not found.

### Authentication
* `401 Unauthorized` Authentication failure. 
  * `4010` Invalid user credentials - bad secret.
  * `4011` Invalid user credentials - bad token.
  * `4012` Invalid user credentials - bad self generated token.
  * `4013` User credentials not set, secret or token must be passed.
  * `4014` The conversion seconds balance reached zero and no more conversions can be done..
  * `4015` User inactive.

### Conversion failure
* `500 Internal Server Error` Conversion failure.
  * `5000` Conversion timeout.
  * `5001` Conversion failed.
  * `5002` File is damaged.
  * `5003` File is password protected.
  * `5004` No tables to extract in PDF file.
  * `5005` Invalid URL format.
  * `5006` Invalid password.
  * `5007` Unable to download the remote file.
  * `5008` Unable to access the file from local storage.
  * `5009` File id is invalid.
  * `50010` File link is set incorrectly. Url or File Id must be set.

### Throttle failure
* `503 Service Unavailable` Request rejected due to rate limits. Retry is available after a few seconds.

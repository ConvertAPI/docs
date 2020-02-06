This is the list of all HTTP response status codes returned by ConvertAPI. The three-number code describes HTTP Status code and four number code shows additional information about result in the response body. The example response body of authentication failure:

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
* `400 Bad Request` Request do not provide all data to execute conversion.
  * `4000` Parameter validation error.
  * `4001` No content disposition provided.
  * `4002` Bad JSon format.
  * `4005` File encoded in Base64 not found.

### Authentication
* `401 Unauthorized` Authentication failure. 
  * `4010` Invalid user credentials - bad secret.
  * `4011` Invalid user credentials - bad token.
  * `4012` Invalid user credentials - bad self generated token.
  * `4013` User credentials not set, secret or token must be passed.
  * `4014` User inactive.

### Conversion failure
* `500 Internal Server Error` Conversion failure.
  * `5000` Conversion timeout.
  * `5001` Conversion failed.
  * `5002` PDF file is damaged.
  * `5003` File is password protected.
  * `5004` No tables to extract in PDF file.
  * `5005` Invalid URL format.
  * `5006` Invalid password.
  * `5007` Unable to download remote file.
  * `5008` Unable to access file from local storage.
  * `5009` File id is invalid.
  * `50010` File link is set incorrectly. Url or File Id must be set.

### Throttle failure
* `502 Bad Gateway` Request rejected due to rate limits. Retry is possible after several seconds.

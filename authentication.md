In this section, we're going to focus on the basics of two ConvertAPI authentication methods.

To authenticate to v2.convertapi.com there are two options:

* `Secret` - Can be used to authenticate requests from the code that is not accessible for the user (server side software like PHP). Secret can be found in Control Panel.
* `Token` - Can be used to authenticate requests from the code that is accessible for the user (client side software like JavaScript on web browser). Tokens can be requested by API call or generated using Secret.

### Token

#### Request Token

Token request accepts URL query parameters.

* `Secret` - your secret.
* `RequestCount` - restrict how many requests can be made using single token (default is 1).
* `Lifetime` - restrict how many seconds token is valid (default is 1h).
* `Count` - how many tokens will be received by this request (default is 1).

```
[POST] 
https://v2.convertapi.com/token/create?Secret=XXXX&RequestCount=3&Lifetime=10000&Count=2
```
```
[response]
{
    "Tokens": [
        {
            "Id": "4X4RxBGP",
            "ValidUntil": "2017-08-22T16:45:24.6184076Z"
        },
        {
            "Id": "mKRuP5zW",
            "ValidUntil": "2017-08-22T16:45:24.6184076Z"
        }
    ]
}
```
### Generate Token
Token generation algorithm steps:

* Create token string: `tokenUuid|expireTimeStamp|userIp|requestCount`.
  - `tokenUuid` - random 8 bytes alphanumeric string.
  - `expireTimeStamp` - token expiration time in Unix time stamp format.
  - `userIp` - IP address that can use this token (can be blank if token not restricted).
  - `requestCount` - request count that can be made using this token.
* Encrypt token string with AES encryption algorithm using your secret as encryption key, initialization vector (IV) should be "//convertapi.com".
* Encode encrypted string with Base64 algorithm.

### Token usage
```
[POST] 
https://v2.convertapi.com/convert/doc/to/pdf?Token=4X4RxBGP
```

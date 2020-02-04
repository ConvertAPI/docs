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

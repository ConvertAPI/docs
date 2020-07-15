In this section, we're going to focus on the basics of two ConvertAPI authentication methods.

There are two options to authenticate to `v2.convertapi.com`:

* `Secret` - Can be used to authenticate requests from the code that is not accessible for the user (server-side software like PHP). A Secret key can be found in the Control Panel.
* `Token` - Can be used to authenticate requests from the code that is accessible for the user (client-side software like JavaScript on the web browser). Tokens can be requested by the API call or generated using Secret.

### Token

#### Request Token

The token request accepts URL query parameters.

* `Secret` - your secret.
* `RequestCount` - restrict how many requests can be made using a single token (default is 1).
* `Lifetime` - restrict how many seconds token is valid (default is 1h).
* `Count` - specify how many tokens will be received by this request (default is 1).

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
#### Token usage
```
[POST] 
https://v2.convertapi.com/convert/doc/to/pdf?Token=4X4RxBGP
```
#### Delete token
You can leave the token to expire or delete it right away.
```
[DELETE] 
https://v2.convertapi.com/token/4X4RxBGP
```
### Generate Token
Token generation algorithm steps:

* Create token string: `tokenUuid|expireTimeStamp|userIp|requestCount`.
  - `tokenUuid` - random 8 bytes alphanumeric string.
  - `expireTimeStamp` - token expiration time in Unix timestamp format.
  - `userIp` - IP address that can use this token (leave blank if you don’t want to restrict).
  - `requestCount` - request count that can be made using this token.
* Encrypt token string with AES encryption algorithm using your secret as the encryption key, an initialization vector (IV) should be "//convertapi.com".
* Encode an encrypted string using the Base64 algorithm.

#### Token generation code example
```csharp
public static class SelfGeneratedToken
{
    private const int TokenLength = 8;

    private static string GenerateUniqueString(int length)
    {
        var bytes = new byte[100];
        var rng = RandomNumberGenerator.Create();
        rng.GetBytes(bytes);
        return new string(Convert.ToBase64String(bytes).Where(char.IsLetterOrDigit).Take(length).ToArray());
    }

    private static AesCryptoServiceProvider AesCryptoServiceProvider(string secret)
    {
        var aesCsp = new AesCryptoServiceProvider
        {
            BlockSize = 128,
            IV = Encoding.ASCII.GetBytes("//convertapi.com"),
            Key = Encoding.ASCII.GetBytes(secret)
        };
        return aesCsp;
    }

    private static string UrlBase64Encode(byte[] bytes)
    {
        return Convert.ToBase64String(bytes).Replace('+', '-').Replace('/', '_').TrimEnd('=');
    }

    public static string Create(string secret, TimeSpan validityDuration, string userIp, int? requestCount)
    {
        var expireTimeStamp = DateTimeOffset.UtcNow.ToUnixTimeSeconds() + validityDuration.TotalSeconds;
        var tokenUuid = GenerateUniqueString(TokenLength);
        var tokenDataString = $"{tokenUuid}|{expireTimeStamp}|{userIp}|{requestCount}";

        var tokenDataBytes = Encoding.ASCII.GetBytes(tokenDataString);
        var aesCsp = AesCryptoServiceProvider(secret);
        var encryptedTokenData = aesCsp.CreateEncryptor().TransformFinalBlock(tokenDataBytes, 0, tokenDataBytes.Length);
        return UrlBase64Encode(encryptedTokenData);
    }
}
```
Self generated token must be used **together with the ApiKey** parameter. ApiKey can be found in [Control Panel](https://www.convertapi.com/a).
#### Token usage
```
[POST] 
https://v2.convertapi.com/convert/docx/to/pdf?ApiKey=0000000000&Token=E1vYBWy7TAabnFSReCTJGiFUx3xoCJiyIwbPWvuRpcM=
```
### HTTP Response Codes
* `200 Ok` 
  * `2000` Token created successfully.
  * `2001` Token deleted successfully.
  
* `401 Unauthorized` Authentication failure. 
  * `4010` Invalid user credentials - bad secret.
  * `4011` Invalid user credentials - bad token.
  * `4012` Invalid user credentials - bad self generated token.
  * `4013` User credentials not set, secret or token must be passed.
  * `4014` User inactive.

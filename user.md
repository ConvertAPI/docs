The endpoint that returns information about your user account. It is useful to check the account balance status.

### User information request example
```
[GET]
https://v2.convertapi.com/user?Secret=XXXX
```
```
[response]
{
    "Secret": "td234f4k45Go6RLv",
    "ApiKey": 834345618,
    "Active": true,
    "FullName": "Name Lastname",
    "Email": "user@example.com",
    "SecondsLeft": 1463
}
```

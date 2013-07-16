### [&laquo; Home](README.md)

[Bukalapak User API](#bukalapak-user-api)
- [User Info](#user-info)
    - [Resource URL](#resource-url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)

## Bukalapak User API

### User Info
Get information for current user
+ Use `GET` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/users/info.json]()

##### Parameters
None

##### Example Request
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/users/info.json

````

##### Example Response
Success response:
````json
{
  "status":"OK",
  "user":
  {
    "name":"Me Ow",
    "email":"meow@domain.com",
    "phone":"022345678901",
    "avatar":"https://secure.gravatar.com/avatar/c8a0457bfc1b881755588e05a6ce55f0?s=50",
    "bank":
    {
      "name":"Bank Republik Dummy",
      "number":"234567890"
    }
  },
  "message":null
} 
````

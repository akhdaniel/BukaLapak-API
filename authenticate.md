### [&laquo; Home](README.md)

[Authentication for Bukalapak API](#authentication-for-bukalapak-api)
- [Authenticate](#authenticate)
    - [URL](#url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)
- [Register](#register)
    - [URL](#url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)

## Authentication for Bukalapak API

### Authenticate
Return token to enable access for `required authentication's resources`
User Bukalapak `user` and `password` for server authentication.

+ Use `POST` http method.

##### URL
+ [https://api.bukalapak.com/v1/authenticate.json]()

##### Parameters
None

##### POST request data
None

##### Example Request
````sh
curl -u billy:Highs3creT https://api.bukalapak.com/v1/authenticate.json -X POST

````

##### Example Response
Success response:
````json
{
  "status":"OK",
  "user_id": "157324",
  "token": "U8Ch2LigkVhdI3XwYRA",
  "message":null
}
````

Failed response
````json
{
  "status":"ERROR",
  "user_id":"null",
  "message":"Invalid password"
}
````

### Register
Return token after registration to enable access for `required authentication's resources`

+ Use `POST` http method.

##### URL
+ [https://api.bukalapak.com/v1/register.json]()

##### Parameters
None

##### POST request data
+ `user[email]` *(required)*. E-mail address to register.
+ `user[username]` *(required)*. Username to register.
+ `user[name]` *(required)*. New user's name.
+ `user[birthday(3i)]` *(optional)*. Date of birth. Use together with `user[birthday(2i)]` and `user[birthday(1i)]`.
+ `user[birthday(2i)]` *(optional)*. Month of birth. Use together with `user[birthday(3i)]` and `user[birthday(1i)]`
+ `user[birthday(1i)]` *(optional)*. Year of birth. Use together with `user[birthday(3i)]` and `user[birthday(2i)]`
+ `user[password]` *(required)*. Password.
+ `user[password_confirmation]` *(required)*. Password confirmation.
+ `user[phone]` *(optional)*. User's phone number.
+ `user[address_attributes][province]` *(optional)*. User's province. Use together with other `address_attributes` data.
+ `user[address_attributes][city]` *(optional)*. User's city. Use together with other `address_attributes` data.
+ `user[address_attributes][area]` *(optional)*. User's area. Use together with other `address_attributes` data.
+ `user[address_attributes][address]` *(optional)*. User's address. Use together with other `address_attributes` data.
+ `user[address_attributes][post_code]` *(optional)*. User's postal code. Use together with other `address_attributes` data.
+ `user[policy]` *(required)*. Sign that user has accepted the agreements.

##### Example Request
````sh
curl -X POST --data "user[email]=testing@testing12349.com&user[username]=testingtesting9&user[name]=asadasan&user[birthday(3i)]=12&user[birthday(2i)]=12&user[birthday(1i)]=1999&user[password]=testing1234&user[password_confirmation]=testing1234&user[phone]=081238877&user[address_attributes][province]=Banten&user[address_attributes][city]=Tangerang&user[address_attributes][area]=Batuceper&user[address_attributes][address]=jl xxx&user[address_attributes][post_code]=11111]&user[policy]=1" "http://api.local.host:3000/v1/register.json"

````

##### Example Response
Success response:
````json
{
  "status":"OK",
  "user_id": "204270",
  "token": "49Rk5LJvph5PAccAQ2Mq"
  "message":null
}
````

Failed response
````json
{
  "status":"ERROR",
  "user_id":null,
  "token":null,
  "message":"Username sudah digunakan, Email sudah digunakan"
}
````

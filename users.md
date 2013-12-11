### [&laquo; Home](README.md)

[Bukalapak User API](#bukalapak-user-api)
- [User Info](#user-info)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Register](#register)
    - [URL](#url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)
- [User Feedbacks](#user-feedbacks)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Show Bank Accounts](#show-bank-accounts)
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


### Register
Return token after registration to enable access for `required authentication's resources`

+ Use `POST` http method.

##### URL
+ [https://api.bukalapak.com/v1/users.json]()

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
curl -X POST --data "user[email]=testing@testing12349.com&user[username]=testingtesting9&user[name]=asadasan&user[birthday(3i)]=12&user[birthday(2i)]=12&user[birthday(1i)]=1999&user[password]=testing1234&user[password_confirmation]=testing1234&user[phone]=081238877&user[address_attributes][province]=Banten&user[address_attributes][city]=Tangerang&user[address_attributes][area]=Batuceper&user[address_attributes][address]=jl xxx&user[address_attributes][post_code]=11111]&user[policy]=1" "https://api.bukalapak.com/v1/users.json"

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

### User Feedbacks
Get feedback listing for current user
+ Use `GET` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/users/:id/feedbacks.json]()

##### Parameters
+ `page` *(optional)*.
+ `per_page` *(required)*.
+ `seller` *(required)*. Field indicating whether to return feedback as seller, or as buyer. Possible value `0` and anything else. If set to '0', response will return feedbacks as buyer. Other values or empty will return feedback as seller.


##### Example Request
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/users/62817/feedbacks.json?page=1&per_page=10&seller=0

````

##### Example Response
Success response:
````json
{
  "status": "OK",
  "message": null,
  "feedbacks": [
    {
      "id": 22032,
      "transaction_id": 7921,
      "sender_id": 1,
      "sender_name": "Nugroho Herucahyono",
      "user_id": 62817,
      "user_name": "Sayur Kangkung",
      "body": "Pembeli yang baik. Tidak rewel dan responsive",
      "positive": true,
      "created_at":"2012-10-11T17:55:34+07:00",
      "updated_at":"2012-10-11T17:55:34+07:00"
    },
    {
      "id": 22031,
      "transaction_id": 7907,
      "sender_id": 31432,
      "sender_name": "Khairul",
      "user_id": 62817,
      "user_name": "Sayur Kangkung",
      "body": "Recommended buyer. Ga banyak tanya :). Bayar sesuai harga dan cepat tanggap.",
      "positive": true,
      "created_at":"2012-10-11T17:55:34+07:00",
      "updated_at":"2012-10-11T17:55:34+07:00"
    }
  ]
}
````

### Show Bank Accounts
Get bank account listing for the current user.
+ Use `GET` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/users/banks.json]()

##### Parameters
None


##### Example Request
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/users/banks.json

````

##### Example Response
Success response:
````json
{
  "status":"OK",
  "accounts":[
    {
      "id":41829,
      "bank":"Bank Central Asia (BCA)",
      "number":"123 456 789",
      "name":"Me Ow",
      "primary":false
    },
    {
      "id":41831,
      "bank":"Bank Central Asia (BCA)",
      "number":"987 654 321",
      "name":"Me Ow",
      "primary":false
    }
  ],
  "message":null
}
````

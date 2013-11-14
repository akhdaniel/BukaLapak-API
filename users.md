### [&laquo; Home](README.md)

[Bukalapak User API](#bukalapak-user-api)
- [User Info](#user-info)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [User Feedbacks](#user-feedbacks)
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
      "positive": true
    },
    {
      "id": 22031,
      "transaction_id": 7907,
      "sender_id": 31432,
      "sender_name": "Khairul",
      "user_id": 62817,
      "user_name": "Sayur Kangkung",
      "body": "Recommended buyer. Ga banyak tanya :). Bayar sesuai harga dan cepat tanggap.",
      "positive": true
    }
  ]
}
````

##### Example Request for Feedbacks
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/users/15/feedbacks.json?page=2&per_page=5&seller=1

````

URL format: `https://api.bukalapak.com/v1/users/:id/feedbacks.json`
Parameters:
+ `:id` *(required)*. User ID of target user.
+ `page` *(optional)*. Page to be displayed. Default is `1`.
+ `per_page` *(optional)*. Number of displayed feedbacks per page. Default is `10`.
+ `seller` *(optional)*. If `1` display feedbacks as seller. If `0` display feedbacks as buyer. If not defined display feedbacks as seller.

##### Example Response for Feedbacks
Success response:
````json
{
  "status":"OK",
  "feedbacks":
  {
    "body":"Lorem ipsum...",
    "created_at":"2013-10-30T14:36:39+07:00",
    "deleted":false,
    "for_seller":true,
    "id":38503,
    "payment_transaction_id":null,
    "positive":true,
    "redeem":false,
    "retur":false,
    "sender_id":null,
    "sender_name":"Alice",
    "updated_at":"2013-10-30T14:36:39+07:00",
    "url":"some_url",
    "user_id":15
  },
  "message":null
} 
````

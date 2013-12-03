### [&laquo; Home](README.md)

[Bukalapak Messages API](#bukalapak-negotiations-api)
- [Get Inbox](#get-inbox)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Get Conversation](#get-conversation)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Get Message](#get-message)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Create Message](#create-message)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [POST request data](#post-request-data)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Delete Conversation](#delete-conversation)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Delete Message](#delete-message)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)

## Bukalapak Messages API

### Get Inbox
Get current user's inbox

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/messages.json]().

##### Parameters
+ `page` *(optional)*. Default to `1`
+ `per_page` *(optional)*. Default to `10`

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/messages.json?page=1
````

##### Example Response
````json
{
    "status": "OK",
    "unread": 0,
    "inbox": [
        {
            "id": "520e0474e42b5658ab00001c",
            "updated_at": "2013-12-03T08:54:49+07:00",
            "partner_id": "155905",
            "partner_name": "Zakka Fauzan Muhammad",
            "user_id": "62817",
            "user_name": "Sayur Kangkung",
            "last_message": "sip diterima san..."
        },
        {
            "id": "5125950c948f5c1a05000662",
            "updated_at": "2013-12-02T21:50:51+07:00",
            "partner_id": "39435",
            "partner_name": "Cecep",
            "user_id": "62817",
            "user_name": "Sayur Kangkung",
            "last_message": "ok"
        },
        {
            "id": "516ffb155ff21f7b53000178",
            "updated_at": "2013-12-02T11:26:03+07:00",
            "partner_id": "78285",
            "partner_name": "Khairul",
            "user_id": "62817",
            "user_name": "Sayur Kangkung",
            "last_message": "kung"
        },
        {
            "id": "4ffab90e5ff21f447e000004",
            "updated_at": "2013-07-28T17:05:40+07:00",
            "partner_id": "57451",
            "partner_name": "Renjay Shop",
            "user_id": "62817",
            "user_name": "Sayur Kangkung",
            "last_message": "testing..."
        }
    ]
}
````

### Get Conversation
Get current user's selected conversation

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/:id.json]().

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/messages/516d3299425762188f000011.json
````

##### Example Response
````json
{
	"status":"OK",
	"instant_messages":[{"_id":"516e2565177961034c000002","attachment_id":0,"body":"tesssss","body_bb":"tesssss","category":0,"created_at":"2013-04-17T11:30:29+07:00","inbox_id":"516d3299425762188f000011","product_id":null,"read":true,"receiver_id":"110675","receiver_name":"Phillip Leonardo","removed":false,"sender_id":"110677","sender_name":"Testa B","updated_at":"2013-04-17T11:30:29+07:00"}],
	"message":null
}
````

### Get Message
Get current user's selected message

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/im/:id.json]().

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/messages/im/516e2565177961034c000002.json
````

##### Example Response
````json
{
	"status":"OK",
	"instant_message":{"_id":"516e2565177961034c000002","attachment_id":0,"body":"tesssss","body_bb":"tesssss","category":0,"created_at":"2013-04-17T11:30:29+07:00","inbox_id":"516d3299425762188f000011","product_id":null,"read":true,"receiver_id":"110675","receiver_name":"Phillip Leonardo","removed":false,"sender_id":"110677","sender_name":"Testa B","updated_at":"2013-04-17T11:30:29+07:00"},
	"message":null
}
````

### Create Message
Create a new message

+ Use `POST` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/messages.json]().

##### Parameters
None

##### POST request data
+ `instant_message` *(required)*. New message to be sent, which contains:
	+ `receiver_id` *(required)*. Message receiver's user ID
	+ `category` *(required)*. Message category: '0' => normal message, '1' => question, '2' => suggestion, '3' => feature, '4' => transaction, note that for category > 0 must be addressed to admin
	+ `body_bb` *(required)*. Message's content

##### Example Request
```sh
curl -u 110677:JheQQS0OKApu3hGJwkRH -d '{ "instant_message":{"receiver_id":"110675", "category":"0", "body_bb":"tesssss"} }' https://api.bukalapak.com/v1/messages.json -H "Content-Type: application/json" -X POST
```

##### Example Response
Failed example
```json
{
	"status":"ERROR",
	"id":null,
	"message": "Gagal mengirim pesan: harap menggunakan format yang seharusnya"
}
```
```json
{
	"status":"ERROR",
	"id":null,
	"message": "Gagal mengirim pesan"
}
```
```json
{
	"status":"ERROR",
	"id":null,
	"message": "Pengiriman pesan untuk kategori ini hanya dapat ditujukan kepada admin"
}
```
Successfull example
```json
{
	"status":"OK",
	"id":"516d303c425762188f000007",
	"message": null
}
```

### Delete Conversation
Delete existing conversation

+ Use `DELETE` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being destroy.

##### Example Request
```sh
curl -u 110677:JheQQS0OKApu3hGJwkRH https://api.bukalapak.com/v1/messages/516d3299425762188f000011.json -H "Content-Type: application/json" -X DELETE
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"id":"516d3299425762188f000011",
	"message": "Conversation berhasil dihapus"
}
```

### Delete Message
Delete existing message

+ Use `DELETE` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/im/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being destroy.

##### Example Request
```sh
curl -u 110677:JheQQS0OKApu3hGJwkRH https://api.bukalapak.com/v1/messages/516d3299425762188f000015.json -H "Content-Type: application/json" -X DELETE
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"id":"516d3299425762188f000015",
	"message": "Pesan berhasil dihapus"
}
```

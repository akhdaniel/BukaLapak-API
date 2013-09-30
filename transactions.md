### [&laquo; Home](README.md)

[Bukalapak Transactions API](#bukalapak-transactions-api)
- [List Transactions](#list-transactions)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Get Transaction](#get-transaction)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Confirm Shipping for Transaction](#confirm-shipping)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)

## Bukalapak Transactions API

### List Transactions
Get transactions owned by current user.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body.

Server will set `Etag` header to every request to this resource.

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/transactions.json](). No search parameter provided.
+ [https://api.bukalapak.com/v1/transactions.json?page=2&per_page=10](). `page` and `per_page` provided.

##### Parameters
+ `page` *(optional)*. Keywords use to search products.
+ `page` *(optional)*. Page number, default to `0`.
+ `per_page` *(optional)*. Number of transactions `per_page`, default to `10`.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v1/transactions.json?page=2"
```

##### Example Response
```json
{
  "status":"OK",
  "transactions":[{
    "id":7870,
    "state":"remitted",
    "transaction_id":"130429230001",
    "amount":2340000,
    "shipping_fee":9000,
    "total_amount":2349000,
    "product":{
      "name":"Kamara", "url":"https://www.bukalapak.com/p/kamera/kamera-digital/gglw_-kamara"
    },
    "buyer":{
      "id":31432, "name":"Khairul", "username":"kahirul"
    },
    "seller":{
      "id":62817, "name":"Sayur Kangkung", "username":"sayurkangkung"
    },
    "actions":[]
  },
  {
    "id":7858,
    "state":"paid",
    "transaction_id":"130322140001",
    "amount":150000,
    "shipping_fee":9000,
    "total_amount":159000,
    "product":{
      "name":"pre order Haunted Trail Shirt","url":"https://www.bukalapak.com/p/fashion/men/t-shirt-165/gglu_-pre-order-haunted-trail-shirt"
    },
    "buyer":{
      "id":31432,"name":"Khairul","username":"kahirul"
    },
    "seller":{
      "id":62817,"name":"Sayur Kangkung","username":"sayurkangkung"
    },
    "actions":["deliver"]
  }]
  ,"message":null
}
```

### Get Transaction
Get transaction details owned by current user.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body.

Server will set `Etag` header to every request to this resource.

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/transactions/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for transaction being read.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v1/transactions/7870.json"
```

##### Example Response
```json
{
  "status":"OK",
  "transactions":{
    "id":7870,
    "state":"remitted",
    "transaction_id":"130429230001",
    "amount":2340000,
    "shipping_fee":9000,
    "total_amount":2349000,
    "product":{
      "name":"Kamara", "url":"https://www.bukalapak.com/p/kamera/kamera-digital/gglw_-kamara"
    },
    "buyer":{
      "id":31432, "name":"Khairul", "username":"kahirul"
    },
    "seller":{
      "id":62817, "name":"Sayur Kangkung", "username":"sayurkangkung"
    },
    "actions":[]
  }
  ,"message":null
}
```

### Confirm Shipping
Confirm Shipping for Transaction

+ Use `POST` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/transactions/confirm_shipping.json]().

##### Parameters
None

##### POST request data
+ `payment_shipping` *(required)*. Attributes of transaction shipping confirmation in JSON. Attributes constructed by following fields:
  + `transaction_id` *(required)*. Transaction ID
  + `shipping_code` *(required)*. Shipping receipt code
  + `new_courier` *(optional)*. Used if courier used other than JNE, TIKI, or POS

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY -d '{ "payment_shipping": { "transaction_id":"7870", "shipping_code":"1568772840123" } }' https://api.bukalapak.com/v1/transactions/confirm_shipping.json -H "Content-Type: application/json" -X POST
```

##### Example Response
Failed example
```json
{
  "status":"ERROR",
	"id":null,
	"message": "Belum ada konfirmasi pembayaran atau konfirmasi pengiriman barang sudah dilakukan"
}
```
Successfull example
```json
{
	"status":"OK",
	"id":"1315",
	"message": "Konfirmasi pengiriman barang berhasil"
}
```

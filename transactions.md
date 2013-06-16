### [&laquo; Home](README.md)

[Bukalapak Transactions API](#bukalapak-transactions-api)
- [List Products](#list-products)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)

## Bukalapak Transactions API

### List Transactions
Get transactions owned by current user.

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/transactions.json](). No search parameter provided.
+ [https://api.bukalapak.com/v1/transactions.json?page=2&per_page=10](). `page` and `per_page` provided.

##### Parameters
+ `page` *(optional)*. Keywords use to search products.
+ `page` *(optional)*. Page number, default to `0`.
+ `per_page` *(optional)*. Number of transactions `per_page`, default to `10`.

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v1/transactions.json?page=2"
````

##### Example Response
````json
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
````

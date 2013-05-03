# [Bukalapak API](README.md)

[Bukalapak Products API](#bukalapak-products-api)
- [List Products](#list-products)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [My Lapak](#my-lapak)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Create Product](#create-product)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [POST request data](#post-request-data)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Read Product](#read-product)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Delete Product](#delete-product)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)

## Bukalapak Products API

### List Products
Get a number of products. If parameter `q` exist, this will give a number of products matching with keywords `q`

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/products.json](). No search parameter available.
+ [https://api.bukalapak.com/v1/products.json?q=mtb](). Show products match with keywords `mtb`.
+ [https://api.bukalapak.com/v1/products.json?limit=5](). First five products.

##### Parameters
+ `q` *(optional)*. Keywords use to search products.
+ `offset` *(optional)*. Discard first `offset` of products, default to `0`.
+ `limit` *(optional)*. Limit count of products into `limit`, default to `10`.

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products.json?q=mtb&offset=2&limit=1"
````

##### Example Response
````json
{
	"status":"OK",
	"products":[{
		"id":700,
		"category":"Sepeda MTB",
		"name":"MTB miyata carbon",
		"city":"Jakarta Selatan",
		"province":"Jawa Tengah",
		"price":5000000,
		"image":"https://s7.bukalapak.com/system2/images/1/0/6/9/7/thumb/bag-lunch.png?1340957861"
	}],
	"metadata":{
		"offset":"2",
		"limit":"1"
	}
}
````
### My Lapak
Get current user's store (lapak)

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/products/mylapak.json](). No search parameter available.
+ [https://api.bukalapak.com/v1/products/mylapak.json?sold=true](). Show sold products only.
+ [https://api.bukalapak.com/v1/products/mylapak.json?available=true](). Show available products only.

##### Parameters
+ `sold` *(optional)*. Keywords use to get sold only products.
+ `available` *(optional)*. Keywords use to get available only products.

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products/mylapak.json"
````

##### Example Response
````json
{
	"status":"OK",
	"products":[{"active":true,"available":true,"cached_slug":"asdasda","car_model_id":null,"car_type":null,"categories_string":null,"category_id":242,"city":"Bekasi","comments_count":0,"contact_fb":null,"contact_name":null,"contact_phone":null,"created_at":"2013-04-15T10:15:31+07:00","delta":true,"description":"asdasdasd","description_bb":"asdasdasd","id":768014,"images_count":0,"kilometer":null,"minimum_negotiable":1300000,"motor_model_id":null,"name":"asdasda","negotiable":true,"new":false,"pilihan":false,"price":1510000,"primary_imageid":null,"province":"Jawa Barat","rent_or_sell":"Dijual","shippping_method":null,"size":null,"sold_at":null,"stat_changed_at":null,"state":"booked","state_changed_at":{"booked_at":"2013-04-15T17:29:06+07:00"},"stock":0,"transmition":null,"type":null,"updated_at":"2013-04-15T17:29:06+07:00","user_id":110675,"weight":"7000","year":null}]
}
````

### Create Product
Create a new product

+ Use `POST` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/products.json]().

##### Parameters
None

##### POST request data
+ `product` *(required)*. Attributes of new product in JSON. Attributes constructed by following fields:
	+ `category_id` *(required)*. Category of new product. [Check this page for valid categories](categories.md#list-category).
	+ `name` *(required)*. Product name.
	+ `price` *(required)*. Product price.
	+ `weight` *(required)*. Product weight in grams.
	+ `stock` *(required)*. Number new product in stock.
	+ `description_bb` *(required)*. Description for new product. You can use BBCode format.
	+ `new` *(optional)*. Product condition as in *new* or *used*. Possible value are *true* for *new* and *false* for *used* product.
	+ `negotiable` *(optional)*. This field indicate whether new product price is negotiable or not. Possible value are *false* for fixed price and *true* for negotiable price. Default value is *false*.
+ `images` *(required)*. List of images/attachments identifier for new product. Required between 1-5 attachments. Muliple attachments separated by comma. Attachment should be created first and attachment can be used only for one product. More on [attachments](attachments.md#create-attachment)
+ `product_detail_attribute` *(optional)*. Details attributes for product in JSON. [Attributes are vary based on category of product](categories.md#category-attributes). Some of these fields are:
	+ `type` *(optional)*. Tyoe of product. For product categorized as *fullbike* type can be *MTB*, *Roadbike*, etc.
	+ `brand` *(optional)*. For *Fullbike*, brand can be *United*, *Polygon*, etc.
	+ `ukuran` *(optional)*.
	+ `bahan` *(optional)*.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
-d '{ \
	"product": { "category_id":"242", "name":"Polygon Helios 200", "new":"true", "price":"2700000", "negotiable":"true", "weight":"5000", "stock":"2", "description_bb":"Sepeda roadbike polygon series helios 200"}, \
	"images":"10820,10822,10283", \
	"product_detail_attribute":{ "type":"Roadbike", "brand":"Polygon", "bahan":"Cromoly"}}' \
"https://api.bukalapak.com/v1/products.json" -H "Content-Type: application/json" -X POST
```

##### Example Response
Failed example
```json
{
	"status":"ERROR",
	"id":null,
	"message":{
		"images":["Image tidak boleh kosong"]
	}
}
```
Successfull example
```json
{
	"status":"OK",
	"id":"12702",
	"message": null
}
```

### Read Product
Read a product

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/products/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being read.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products/12072.json" -H "Content-Type: application/json" -X GET
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"product":
	{
		"id":12071, "category":"Handphone (HP)", "name":"NOKIA 5200- Black", "city":"Jakarta Selatan", "province":"DKI Jakarta", "price":500000, "image":"https://s5.bukalapak.com/system2/images/5/thumb/nokia.jpg?1264040052"
	},
	"message":null
}
```

### Delete Product
Delete existing product

+ Use `DELETE` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/products/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being destroy.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products/12072.json" -H "Content-Type: application/json" -X DELETE
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"id":"12702",
	"message": null
}
```

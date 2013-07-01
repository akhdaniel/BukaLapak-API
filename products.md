### [&laquo; Home](README.md)

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
- [Update Product](#update-product)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [PUT request data](#put-request-data)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Read Product](#read-product)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Sold Product](#sold-product)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Relist Product](#relist-product)
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
+ [https://api.bukalapak.com/v1/products.json](). No search parameter provided.
+ [https://api.bukalapak.com/v1/products.json?q=mtb](). Show products match with keywords `mtb`.
+ [https://api.bukalapak.com/v1/products.json?page=1&per_page=10](). First ten products.

##### Parameters
+ `q` *(optional)*. Keywords use to search products.
+ `page` *(optional)*. Pagination page, default to `0`.
+ `per_page` *(optional)*. Number results per_page, default to `20`.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products.json?q=mtb&page=2&per_page=40"
```

##### Example Response
```json
{
	"status":"OK",
	"products":[{
		"id":"kxsp",
		"category":"Sepeda MTB",
		"name":"MTB miyata carbon",
		"city":"Jakarta Selatan",
		"province":"Jawa Tengah",
		"price":5000000,
		"image":"https://s7.bukalapak.com/system2/images/1/0/6/9/7/thumb/bag-lunch.png?1340957861"
	}],
	"message":null
}
```

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
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products/mylapak.json"
```

##### Example Response
```json
{
  "status":"OK",
  "products":[
  {
    "id":"llyq",
    "category":"Digital Camera",
    "category_structure":["Kamera","Digital Camera"],
    "name":"Nikon (Test, please ignore)",
    "city":"Jakarta Selatan",
    "province":"DKI Jakarta",
    "price":5500000,
    "images":["https://s1.bukalapak.com/system/images/2/4/5/4/5/6/6/large/81M95oa1m2L._SL1500_.jpg?1369729801"],
    "url":"https://www.bukalapak.com/p/kamera/digital-camera/llyq_-nikon-test-please-ignore",
    "desc":"Test, please ignore",
    "condition":"used",
    "nego":true,
    "seller_name":"Me Oww",
    "payment_ready":true,
    "stock":1,
    "specs":{
      "type":"D-SLR",
      "brand":"Nikon",
      "megapixel":"5.0 - 9.9MP",
      "optical_zoom":"0",
      "screen_size":"",
      "garansi":"1-12 bulan",
      "memory_card_type":"MicroSD",
      "body_color":"hitam",
      "video":"Yes",
      "image_stabilization":""
    }
  },
  {
    ...
  }],
  "message":null
}
```

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
+ `images` *(required)*. List of images identifier for new product. Required between 1-5 images. Muliple images separated by comma. Image should be created first and image can be used only for one product. More on [images](images.md#create-image)
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
	"id":"kxvi",
	"message": null
}
```

### Update Product
Update an existing user's product

+ Use `PUT` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/products/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being read.

##### PUT request data
+ `product` *(required)*. Attributes of existing product in JSON. Attributes constructed by following fields:
	+ `name` *(optional)*. Product name.
	+ `price` *(optional)*. Product price.
	+ `weight` *(optional)*. Product weight in grams.
	+ `stock` *(optional)*. Number existing product in stock.
	+ `description_bb` *(optional)*. Description for existing product. You can use BBCode format.
	+ `new` *(optional)*. Product condition as in *new* or *used*. Possible value are *true* for *new* and *false* for *used* product.
	+ `negotiable` *(optional)*. This field indicate whether existing product price is negotiable or not. Possible value are *false* for fixed price and *true* for negotiable price. Default value is *false*.
+ `images` *(optional)*. List of images identifier for existing product. Required between 1-5 images. Muliple images separated by comma. Image should be created first and image can be used only for one product. More on [images](images.md#create-image)
+ `product_detail_attribute` *(optional)*. Details attributes for product in JSON. [Attributes are vary based on category of product](categories.md#category-attributes). Some of these fields are:
	+ `type` *(optional)*. Tyoe of product. For product categorized as *fullbike* type can be *MTB*, *Roadbike*, etc.
	+ `brand` *(optional)*. For *Fullbike*, brand can be *United*, *Polygon*, etc.
	+ `ukuran` *(optional)*.
	+ `bahan` *(optional)*.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
-d '{ \
	"product": { "price":"2700000", "stock":"2" } }' \
"https://api.bukalapak.com/v1/products/f3vi.json" -H "Content-Type: application/json" -X PUT
```

##### Example Response
```json
{
	"status":"OK",
	"product": {
		"id":"f3vi",
		"category":"Handphone (HP)",
		"name":"Gemini PALING MAHAL (made in mexico)",
		"city":"Jakarta Selatan",
		"province":"DKI Jakarta",
		"price":2700000,
		"image":"https://s0.bukalapak.com/system/images/1/6/7/6/6/8/0/large/IMG00475-20121105-1431.jpg?1352105447",
		"description":"blackberry 8520 original\r\nnot fake / KW / grade ori\r\njudge by pic\r\nmade in mexico\r\nmemory card and battery not included\r\nberrindo\r\nbought it 2009 september\r\nbox, charger, etc included",
		"specs":{
			"brand":"Blackberry",
			"operating_system":"Blackberry",
			"features":["Wifi","Bluetooth","Memory Card Slots","MP3","Message","e-mail","Video Player","QWERT Keyboard",""],
			"bentuk":"Klasik (Bar)",
			"display_size":"",
			"camera":"Camera",
			"garansi":"Tidak bergaransi",
			"network":"GSM",
			"body_color":"hitam"
		}
	},
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
"https://api.bukalapak.com/v1/products/kxvi.json" -H "Content-Type: application/json" -X GET
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"product":
	{
		"id":kxvi, "category":"Handphone (HP)", "name":"NOKIA 5200- Black", "city":"Jakarta Selatan", "province":"DKI Jakarta", "price":500000, "image":"https://s5.bukalapak.com/system2/images/5/thumb/nokia.jpg?1264040052"
	},
	"message":null
}
```

### Sold Product
Set Product to Sold

+ Use `PUT` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/products/:id/sold.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being read.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products/kxvi/sold.json" -H "Content-Type: application/json" -X PUT
```

##### Example Response
```json
{
	"status":"OK",
	"id": "kxvi",
	"message": "Product has been set to sold"
}
```

### Relist Product
Set Product to Available

+ Use `PUT` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/products/:id/relist.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being read.

##### Example Request
```sh
curl -u 67287:lXymG93y83m6RHzZV5FY \
"https://api.bukalapak.com/v1/products/kxvi/relist.json" -H "Content-Type: application/json" -X PUT
```

##### Example Response
```json
{
	"status":"OK",
	"id": "kxvi",
	"message": "Product has been set to available"
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
"https://api.bukalapak.com/v1/products/kxvi.json" -H "Content-Type: application/json" -X DELETE
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"id":"kxvi",
	"message": null
}
```

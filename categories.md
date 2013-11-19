### [&laquo; Home](README.md)

[Bukalapak Product Category API](#bukalapak-product-category-api)
- [List Category](#list-category)
    - [Resource URL](#resource-url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)
- [Category Attributes](#category-attributes)
    - [Resource URL](#resource-url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)
- [Dictionary](#dictionary)

## Bukalapak Product Category API

### List Category
Get all `product's category`

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body.

Server will set `Etag` header to every request to this resource.

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/categories.json]()

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/categories.json

````

##### Example Response
````json
{
  "status": "OK",
  "categories": [
    {
      "id": 64,
      "name": "Sepeda",
      "children": [
        {
          "id": 242,
          "name": "Fullbike",
          "children": [
            {
              "id": 370,
              "name": "MTB"
            },
            {
              "id": 371,
              "name": "Roadbike"
            }
          ]
        },
        {
          "id": 85,
          "name": "Frame",
          "children": [
            {
              "id": 372,
              "name": "MTB"
            },
            {
              "id": 373,
              "name": "Roadbike"
            }
          ]
        }
      ]
    },
    {
      "id": 10,
      "name": "Kamera",
      "children": [
        {
          "id": 186,
          "name": "Kamera Digital"
        },
        {
          "id": 350,
          "name": "Kamera Analog"
        }
      ]
    },
  ]
}
````

### Category Attributes
Get attributes for a category

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body.

Server will set `Etag` header to every request to this resource.

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/categories/:id/attributes.json]()

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/categories/242/attributes.json

````

##### Example Response
````json
{
  "status":"OK",
  "attributes":{
    "type":{
      "fieldName":"type",
      "displayName":"Type",
      "inputType":"select",
      "options":["MTB", "Roadbike", "City", "Others"]
    },
    "brand":{
      "fieldName":"brand",
      "displayName":"Brand",
      "inputType":"select",
      "options":["United", "Polygon", "Giant", "WimCycle", "Generik", "Tidak Tahu"]
    },
    "ukuran":{
      "fieldName":"ukuran",
      "displayName":"Ukuran",
      "inputType":"string",
      "options":[]
    },
    "bahan":{
      "fieldName":"bahan",
      "displayName":"Bahan",
      "inputType":"select",
      "options":["Chromoly", "Carbon", "Steel"]
    }
  },
  "message":null
}
````

### Dictionary
- `inputType` Type of input. *No shit Sherlock*. Possible value are
    - `string`, equivalent to `input` type `text` tag in html
    - `text`, equivalnet to `textarea`
    - `select`, `combo_select`, equivalent to `select`
    - `boolean`, `check_boxes`, equivalent to `input` type `checkbox`
    - `radio_buttons`, equivalent to `input` type `radio`

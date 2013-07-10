### [&laquo; Home](README.md)

[Bukalapak Image API](#bukalapak-image-api)
- [Create Image](#create-image)
    - [Resource URL](#resource-url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)

- [Image Status](#image-status)
    - [Resource URL](#resource-url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)

## Bukalapak Image API

### Create Image
Create Image
+ Use `POST` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/images.json]()

##### Parameters
None

##### POST request data
None

##### Example Request
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/images.json -F file=@product-image.png -X POST

````

##### Example Response
Success response:
````json
{
  "status":"OK",
  "id": "157324",
  "message":null
}
````

Failed response
````json
{
  "status":"ERROR",
  "user_id":"null",
  "message":"Harus berupa file gambar"
}
````

### Image Status
Check image status whether it has been assigned to a product or not.
+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/images/status/:id.json]()

##### Parameters
+ `id` *(required)*. Image identifier.

##### Example Request
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/images/status/181244.json

````

##### Example Response
Response for image without product:
````json
{
  "status":"OK",
  "id":1838301,
  "message":"Orphaned"
}
````

Response for image that has been assigned to product.
````json
{
  "status":"ERROR",
  "user_id":1838301,
  "message":"Assigned"
}
````
# [Bukalapak API](README.md)

[Bukalapak Attachment API](#bukalapak-attachment-api)
- [Create Attachment](#create-attachment)
    - [Resource URL](#resource-url)
    - [Parameters](#parameters)
    - [Example Request](#example-request)
    - [Example Response](#example-response)

## Bukalapak Attachment API

### Create Attachment
Create Attachment
+ Use `POST` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/authenticate.json]()

##### Parameters
None

##### POST request data
None

##### Example Request
````sh
curl -u 15:wcrG8WPPWaq9Ndiesbjn https://api.bukalapak.com/v1/attachments.json -F file=@product-image.png

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

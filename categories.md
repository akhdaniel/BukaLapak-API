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

## Bukalapak Product Category API

### List Category
Get all `product's category`

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/categories.json]()

##### Parameters
None

##### Example Request
````sh
curl https://api.bukalapak.com/v1/categories.json

````

##### Example Response
````json
{
  "status":"OK",
  "categories":{
    "Sepeda":{
      "83":"Sepeda MTB",
      "96":"Helm & Body Protection",
      "Drivetrain":{
        "88":"Crank",
        "259":"Rantai"
      },
      "138":"Part Generic",
      "Outwear":{
        "279":"Gogle",
        "280":"Tas"
      }
    },
    "HP & Elektronik":{
      "Handphone (HP)":{
        "105":"Blackberry",
        "Android":{
          "147":"Samsung",
          "150":"LG",
          "151":"Lain-lain"
        },       
        "154":"Lain-lain"
      },
      "Kamera":{
        "119":"SLR Fullset",
        "199":"Others"
      }      
    },
    "Properti":{
      "74":"Rumah",
      "75":"Apartemen",
      "76":"Ruko",
      "77":"Kamar & Kos",
      "78":"Tanah"
    }
  },
  "message":null
}
````

### Category Attributes
Get attributes for a category

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/categories/:id/attributes.json]()

##### Parameters
None

##### Example Request
````sh
curl https://api.bukalapak.com/v1/categories/242/attributes.json

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

### [&laquo; Home](README.md)

[Notifications API](#notifications-api)
- [Add Android Device](#add-android-device)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Logout Android Device](#logout-android-device)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Remove Android Device](#remove-android-device)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Get Unread Notifications](#get-unread-notifications)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Set Notifications as Read](#set-notifications-as-read)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Set a Notification as Read](#set-a-notifications-as-read)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Android Notifications Data Format](#android-notifications-data-format)
- [Supported Banks](#supported-banks)

## Notifications API

### Add Android Device
Add user's Android device to receive notifications.
+ Use `POST` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/notifications/android.json]()

##### Parameters
+ `reg_id` *(required)*. Registration ID of the device.
+ `model` *(optional)*. Device model.
+ `manufacturer` *(optional)*. Device manufacturer.
+ `product_name` *(optional)*. Device product name.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu "https://api.bukalapak.com/v1/notifications/android.json" -X POST --data "reg_id=ASD223SDA&model=GG-P4124H&manufacturer=Nokia&name=Lumpia"

````

#### Example Response
Success response:

````json
{
  "status":"OK",
  "message":"Device added"
}
````

Failed response:
````json
{
  "status":"ERROR",
  "message":"Failed adding device"
}
````

### Logout Android Device
Logout current user from current device.
+ Use `DELETE` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/notifications/logout.json]()

##### Parameters
+ `reg_id` *(required)*. Registration ID of the device.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu "https://api.bukalapak.com/v1/notifications/logout.json" -X DELETE --data "reg_id=ASD223SDA"

````

#### Example Response
Success response:
````json
{
  "status":"OK",
  "message":"Device logged out"
}
````

Failed response:
````json
{
  "status":"ERROR",
  "message":"Failed logging out"
}
````


### Remove Android Device
Remove user's Android device from receiver devices list.
+ Use `DELETE` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/notifications/android.json]()

##### Parameters
+ `reg_id` *(required)*. Registration ID of the device.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu "https://api.bukalapak.com/v1/notifications/android.json" -X DELETE --data "reg_id=ASD223SDA"

````

#### Example Response
Success response:
````json
{
  "status":"OK",
  "message":"Device unregistered"
}
````

Failed response:
````json
{
  "status":"ERROR",
  "message":"The requested device doesn't belong to this user"
}
````

### Get Unread Notifications
Get numbers of unread messages and transactions.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/notifications/unreads.json]()

##### Parameters
+ `reg_id` *(required)*. Registration ID of the device.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu "https://api.bukalapak.com/v1/notifications/unreads.json"

````

#### Example Response
````json
{
  "messages":0,
  "transactions_need_action_as_seller":0,
  "transactions_as_buyer":0,
  "unread_notifications":0,
  "transactions_need_action_as_buyer":4
}
````

### Set Notifications as Read
+ Use `PUT` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/notifications.json]()

##### Parameters
+ `reg_id` *(required)*. Registration ID of the device.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu -X PUT "https://api.bukalapak.com/v1/notifications.json" --data ""

````

#### Example Response
````json
{
  "status":"OK",
  "message":null
}
````

### Set a Notification as Read
+ Use `PUT` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/notifications/:notification_transaction_id.json]()

##### Parameters
+ `notification_transaction_id` *(required)*. Notification ID of the transaction.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu -X PUT "http://api.local.host:3000/v1/notifications/52a6e5e284eab03aa200013a.json"

````

#### Example Response
````json
Success response

{
  "status":"OK",
  "unread":0,
  "message":null
}

Failed response

{
  "status":"ERROR",
  "unread":1,
  "message":"The requested notifications doesn't belong to the current user"
}
````


### Android Notifications Data Examples

````json
Transaction Notification

{
  "type"=>"transaction",
  "receiver_id"=>204254,
  "message"=>"Transaksi baru dari Liem Lie Wie",
  "details"=>{
    "id"=>51960,
    "state"=>"paid",
    "transaction_id"=>"131211141960",
    "amount"=>155000,
    "quantity"=>1,
    "shipping_fee"=>8000,
    "total_amount"=>163000,
    "products"=>[1069398],
    "consignee"=>{
      "name"=>"Me Ow",
      "address"=>"Jl Lancar XXI",
      "city"=>"Jakarta Barat",
      "province"=>"DKI Jakarta",
      "post_code"=>"11440"
    },
    "buyer"=>{
      "id"=>15,
      "name"=>"Me Ow",
      "username"=>"meow"
    },
    "seller"=>{
      "id"=>204254,
      "name"=>"Testing Account",
      "username"=>"testingaccount"
    },
    "actions"=>["deliver", "reject"],
    "created_at"=>"2013-12-11T14:59:21+07:00"
  }
}

Offer Notification

{
  "type"=>"nego",
  "receiver_id"=>204254,
  "message"=>"Anda mendapatkan tawaran nego dari Me Ow",
  "details"=>{
    "id"=>51580,
    "product_id"=>1069403
  }
}

Message Notification

{
  "type"=>"message",
  "receiver_id"=>204254,
  "message"=>"Anda mendapatkan pesan dari Me Ow"
  "details"=>{
    "id":"56be34322",
    "inbox_id":"56be34",
    "message"=>"mantab gan"
  }
}
````

### Supported Banks

````
[
  "Bank Central Asia (BCA)",
  "Bank Mandiri",
  "Bank Negara Indonesia (BNI)",
  "Bank Rakyat Indonesia (BRI)",
  "Bank Tabungan Negara (BTN)",
  "Bank Agroniaga",
  "Bank Artha Graha International",
  "Bank Bukopin",
  "Bank Bumi Arta",
  "Bank Capital Indonesia",
  "Bank CIMB Niaga",
  "Bank Danamon Indonesia",
  "Bank Ekonomi Raharja",
  "Bank Ganesha",
  "Bank Hana",
  "Bank ICB Bumiputra",
  "Bank ICBC Indonesia",
  "Bank Index Selindo",
  "Bank Maybank Indonesia",
  "Bank Maspion",
  "Bank Mayapada",
  "Bank Mega",
  "Bank Mestika Dharma",
  "Bank Metro Express",
  "Bank Nusantara Parahayangan",
  "Bank OCBC NISP",
  "Bank of India Indonesia",
  "Panin Bank",
  "Bank Permata",
  "Bank QNB Kesawan",
  "Bank SBI Indonesia",
  "Bank Sinarmas",
  "Bank UOB Indonesia",
  "Anglomas International Bank",
  "Bank Andara",
  "Bank Artos Indonesia",
  "Bank Bisnis Internasional",
  "Centrama Nasional Bank",
  "Bank Dipo International",
  "Bank Fama International",
  "Bank Harda International",
  "Bank Ina Perdana",
  "Bank Jasa Jakarta",
  "Bank Kesejahteraan Ekonomi",
  "Bank Liman International",
  "Bank Mayora",
  "Bank Mitraniaga",
  "Bank Multi Arta Sentosa",
  "Bank Nationalnobu",
  "Prima Master Bank",
  "Bank Pundi Indonesia",
  "Bank Royal Indonesia",
  "Bank Sahabat Purba Danarta",
  "Bank Sinar Harapan Bali",
  "Bank Tabungan Pensiunan Nasional",
  "Bank Victoria International",
  "Bank Yudha Bhakti",
  "Bank Jambi (Jambi)",
  "Bank Kalsel (Banjarmasin)",
  "Bank Kaltim (Samarinda)",
  "Bank Sultra (Kendari)",
  "Bank BPD DIY (Yogyakarta)",
  "Bank Nagari (Padang)",
  "Bank DKI (Jakarta)",
  "Bank Lampung (Bandar Lampung)",
  "Bank Kalteng (Palangka Raya)",
  "Bank BPD Aceh (Banda Aceh)",
  "Bank Sulsel (Makassar)",
  "Bank BJB (Bandung)",
  "Bank Kalbar (Pontianak)",
  "Bank Maluku (Ambon)",
  "Bank Bengkulu (Bengkulu)",
  "Bank Jateng (Semarang)",
  "Bank Jatim (Surabaya)",
  "Bank NTB (Mataram)",
  "Bank NTT (Kupang)",
  "Bank Sulteng (Palu)",
  "Bank Sulut (Manado)",
  "Bank BPD Bali (Denpasar)",
  "Bank Papua (Jayapura)",
  "Bank Riau Kepri (Pekanbaru)",
  "Bank Sumsel Babel (Palembang)",
  "Bank Sumut (Medan)",
  "Bank ANZ Indonesia",
  "Bank Commonwealth",
  "Bank Agris",
  "Bank BNP Paribas Indonesia",
  "Bank Capital Indonesia",
  "Bank Chinatrust Indonesia",
  "Bank DBS Indonesia",
  "Bank International Indonesia (BII)",
  "Bank KEB Indonesia",
  "Bank Mizuho Indonesia",
  "Bank Rabobank International Indonesia",
  "Bank Resona Perdania",
  "Bank Sumitomo Mitsui Indonesia",
  "Bank Windu Kentjana International",
  "Bank Woori Indonesia",
  "Bank of Ameriza",
  "Bangkok Bank",
  "Bank of China",
  "Citibank",
  "Deutsche Bank",
  "HSBC",
  "JPMorgan Chase",
  "Royal Bank of Scotland",
  "Standard Chartered",
  "The Bank of Tokyo Mitsubishi UFJ",
  "Bank BNI Syariah",
  "Bank Muamalat Indonesia",
  "Bank Syariah Mandiri",
  "BCA Syariah",
  "Bank BJB Syariah",
  "Bank BRI Syariah",
  "Bank Mega Syariah",
  "Panin Bank Syariah",
  "Bank Syariah Bukopin",
  "Bank Victoria Syariah",
  "Bank Maybank Syariah Indonesia",
  "Bank BTN Syariah",
  "Bank Danamon Syariah",
  "CIMB Niaga Syariah",
  "BII Syariah",
  "OCBC NISP Syariah",
  "Bank Permata Syariah",
  "Bank BPD Aceh Syariah",
  "Bank DKI Syariah",
  "Bank Kalbar Syariah",
  "Bank Kalsel Syariah",
  "Bank NTB Syariah",
  "Bank Riau Kepri Syariah",
  "Bank Sumsel Babel Syariah",
  "Bank Sumut Syariah",
  "HSBC Amanah",
  "Bank Perkreditan Rakyat (BPR KS)"
]
````
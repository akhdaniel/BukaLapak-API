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

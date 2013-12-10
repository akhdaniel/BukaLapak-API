### [&laquo; Home](README.md)

[Bukalapak Dompet API](#bukalapak-dompet-api)
- [Mutation History](#mutation-history)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Withdrawal History](#withdrawal-history)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Withdrawal Request](#withdrawal-request)
  - [Resource URL](#resource-url)
  - [Parameters](#parameters)
  - [Example Request](#example-request)
  - [Example Response](#example-response)
- [Dictionary](#dictionary)

## Bukalapak Dompet API

### Mutation History
Get current user's mutation history.
+ Use `GET` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/dompet/history/mutations.json]()

##### Parameters
+ `page` *(optional)*. Page number to display. Default value is *1*.
+ `per_page` *(optional)*. Number of record to display per page. Default value is *10*.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu "https://api.bukalapak.com/v1/dompet/history/mutations.json?page=1&per_page=1"

````

##### Example Response
````json
{
  "status":"OK",
  "history":[{"id":346,
              "type":"Deposit::Credit",
              "action":"remit",
              "amount":30000,
              "initial_balance":0,
              "final_balance":30000,
              "transaction_id":51938,
              "created_at":"2013-11-25T15:32:47+07:00",
              "updated_at":"2013-11-25T15:32:47+07:00"}],
  "message":null
}
````

### Withdrawal History
Get current user's withdrawal history.
+ Use `GET` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/dompet/history/withdrawals.json]()

##### Parameters
+ `page` *(optional)*. Page number to display. Default value is *1*.
+ `per_page` *(optional)*. Number of record to display per page. Default value is *10*.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu "https://api.bukalapak.com/v1/dompet/history/withdrawals.json?page=1&per_page=1"

````

##### Example Response
````json
{
  "status":"OK",
  "history":[{"amount":25000,
              "bank_account_id":41812,
              "cancelled_at":null,
              "created_at":"2013-11-22T16:00:39+07:00",
              "deposit_id":1,
              "id":4,
              "processed_at":null,
              "state":"pending",
              "updated_at":"2013-11-22T16:00:39+07:00"}],
  "message":null
}
````

### Withdrawal Request
Make withdrawal request for current user.
+ Use `POST` http method
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/dompet/withdraw.json]()

##### Parameters
+ `deposit_withdrawal[amount]` *(required)*. Amount to withdraw.
+ `deposit_withdrawal[bank_account_id]` *(required)*. Bank account id for current user's target account.
+ `deposit_withdrawal[password]` *(required)*. Current user's password.

##### Example Request
````sh
curl -u 204254:Sy7PRGGr4foUk22uzjMu -X POST "https://api.bukalapak.com/v1/dompet/withdraw.json" --data "deposit_withdrawal[amount]=25000&deposit_withdrawal[bank_account_id]=41812&deposit_withdrawal[password]=testing1234"

````

##### Example Response
````json
success:
{
  "status":"OK",
  "withdrawal_id":4,
  "message":null
}

failed:
{
  "status":"OK",
  "withdrawal_id":4,
  "message":"Pencairan hanya bisa dilakukan satu kali sehari."
}

````

### Dictionary
- `type` Type of muation, possible values are `Deposit::Credit` and `Deposit::Debit`
- `action` Action that trigger mutation. Possible values are  `remit`, `topup`, `payment`, `refund`, `withdrawal`, `restore`. 

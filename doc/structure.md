# API
## API description 
#### Getting Started with the Shop Express API  

The Shop Express API allows developers to integrate with and extend the in-built features of the Retail Express platform. It is a RESTful API based on the OpenAPI specification and is the focus for all development and enhancement moving forwards.

This Shop Express API is a modern, secure, and standards based API designed to eventually replace all of our legacy SOAP XML services:
* Webstore/eCommerce
* Warehouse Management
* Inventory Planning
* Accounting

Authorisation
All developers will require an API Key which can be used to generate an access token that is used to authenticate all subsequent requests. Before making calls to a Retail Express client, you must first request an API Key from the client you wish to integrate with. Each API Key is unique to a given client and only provides access to that clients’ data.

Each access token will expire after 60 minutes at which point a new token must be requested.

To authenticate with the Retail Express API, first make a call to the Authentication Token endpoint, passing your API Key in header parameter x-api-key:

https://ccccc.com/v2/auth/token

Assuming a valid API Key is passed, an access token will be returned along with the date/time when it will expire:

{

    "token_type": "Bearer",
    "access_token": "eyJhbmdWxsX2FjY2VzcyJdfQ.IWPofNEfIu-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "expires_on": "2021-01-31T23:48:23.4672689+00:00"

} 

Requests to other endpoints in the API must include this token (in the Authorization header parameter) and the API Key (again in the x-api-key header parameter):

Authorization: Bearer eyJhbmdWxsX2FjY2VzcyJdfQ.IWPofNEfIu-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
x-api-key: hkldfhTYDnhlkadsfadsdfTYSDFNFDSF

Once a token expires, the same call to the Authentication Token endpoint is required to retrieve a new token. Once a token has expired, or if an invalid token is passed, a 401 Unauthorised response will be returned.

## Rate Limits
The Shop Express API is rate limited to maintain the quality of service and performance of the platform. Currently rate limits are imposed on a client basis so if you integrate with multiple clients there will be a separate rate limit for each client / API Key. However, requests from all developers / API Keys count towards the rate limits so even if your application does not exceed the limits, you may still hit the limit for a given client.

**There are two forms of limits imposed:**

300 requests in any single 1 minute, or on average 5 requests per second
100,000 total requests in a 24 hour period

If you hit the per minute rate limit you will receive a 429 Too Many requests response and will need to retry your request after a short period of time.

If you hit the daily quota, you will again receive a 429 Too Many Requests response but you will not be able to make any further requests until the following day.

The per minute limits are designed to allow short bursts of frequent requests as required - integrations should not constantly make requests at these limits or the daily limit will be rapidly reached.

We expect all developers to design their integrations using industry standard techniques for limiting requests within these rate limits and to utilise caching techniques where possible to reduce the overall number of calls.

These rate limits may change at any time.





| Method|Path| Descripton|
|-------|-----------------|------------|
| **POST**  | api/v1/products |Добавление (обновление) по коду 
| **GET**   | api/v1/products |Получение последних 100 записей товаров


## Структуры данных 

### Products
|    Поле                | Значение|Наименование|
|------------------------|---------|-----------|
|Id|              int64  | Уникальный номер (присваивается системой)
|Code|            string | * Код товара запчати товара (должен быть уникальным)
|ReplaceCode|     string | Код замены 
|Title|           string | Наименование запчасти
|Description|     string | Описание товара  
|BarCode|         string | Код для шритри-кода
|BrandId|         int64  | * Brand Id
|Brand|           string | * Бренд имя
|Qt|              float64| * Количество на складе (остаток)    
|Netto|           string | Цена от поставщика в текстовом виде
|VendorId|        int64  | Код поставщика
|Vendor|          string | Наименование производителя
|ExchangeEur|     float64| Курс в евро
|ExchangeUsd|     float64| Курс в гривнах
|PriceEur|        float64| Цена в евро
|PriceUsd|        float64| Цена в долларах
|Price|           float64| * Цена в гривнах
|PriceIn|         float64| Цена входная
|Markup|          float64| Наценка в процентах 
|PriceEuroMurkup| float64| Наценка в евро
|PriceUahMurkup|  float64| Наценка в грн
|Unit|            string| Единица измерения по умолчанию "шт"  






## CURL
```
curl -XPOS 'https://www.mainsite.com/api/v1/products' 
--header 'token: XXXXXXXXXXXXXXXXXXXXXXXXXXXX' 
--header 'Content-Type: application/json'
--data '  {
             "title"        : "parts name",
             ....
          }
```


## Return 

```
}
    "code": "CODE",
    "message": "Товар был успешно добавлен на склад.",
    "name": "Прокладка",
    "status": "ok"
}
```



## Data JSON
**Example JSON :**
```json
{
   "code"         : "CODE-12334",
   "barcode"      : "1223-2002",
   "replace_code" : "122233-93993",
   "title"        : "Блок клопанов",
   "description"  : "Блок клапанов в комплекте и направляющими",
   "barand_id"    : 1,
   "brand"        : "Toyota",
   "vendor"       : "VAG",
   "vendor_id"    : 12,
   "price"        : 515.55,
   "price_in"     : 55.55,
   "price_eur"    : 12255.55,
   "qt"           : 1,
   "cell"         : "Ячейка 12-Ф",
   "row"          : "Полка 14-Б",
   "note"         : "Описание для поставщика",
   "unit"         : "шт",
   "weight"       : 0.123,
   "stock_qty"    : 12,
   "markup"       : 3,
   "max_qt"       : 12,
   "min_qt"       : 2
}
```




# Response Codes
### 200 OK
The request was successfully processed

### 201 Created
The request was successfully processed and a new resource was created

### 400 Bad Request
The request was not understood, generally due to bad request syntax

### 401 Unauthorised
Invalid, missing, or expired credentials

### 404 Not Found
Requested resource or endpoint could not be found

### 429 Too Many Requests
The rate limits for the client have been exceeded

### 500 Internal Server Error
An internal error occurred in Retail Express. Please contact Support.

### 503 Service Unavailable
The server is currently unavailable. Please contact Support.

### 504 Gateway Timeout
The request timed out. Retail Express waits up to 60 seconds for a response. 



### Order
|    Поле                | Значение            |Наименование|
|------------------------|---------------------|-----------|
|Id|              int64  | Уникальный номер
|Code|            string | Id клиента в системе (складской) 
|Name|            string | Наименование клиента  
|Total|           float64| Общая сумма счета
|CreateAt|        time   | Дата создания счета

### Order_items
|    Поле                | Значение            |Наименование|
|------------------------|---------------------|-----------|
|Id|              int64  | Уникальный номер
|OrderId|         string | Id заказа
|Code|            string | Id товара
|Name|            string | Наименование товара  
|Price|           float64| Цена товара  
|Qty|             int    | Количество
|Total|           float64| Общая сумма счета
|Remark|          string | Примечание


## JSON 

GET api/v1/orders/new 

```json

{ 
  "id"          : 12334,
  "order_id"    : 1234566,
  "number"      : "d-200334",
  "create_at    : "20202-02-01 15:04:32",
  "client_id"   : 125,
  "client_name" : "OOO 'System Technologic'", 
  "toatl"       : 1323.89,
  "type"        : "cash", 
  "payment"     : "ok", 
  "status"      : "new",
  "products"    : [
                    { 
                        "id_product" : 12359,
                        "name"       : "Product name ",
                        "qty"        : 2,
                        "price"      : 123.23,
                        "total_sum"  : 246.46,
                        "remark"     : ""
                     },
                    { 
                        "id_product" : 12459,
                        "name"       : "Product name other",
                        "qty"        : 1,
                        "price"      : 23.23,
                        "total_sum"  : 23.23,
                        "remark"     : ""
                     }
                  ]
  }
```


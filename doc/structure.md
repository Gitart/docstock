# Структуры данных для интеграции

## Структура JSON файла


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
|Description|     string | Примечание
|Markup|          float64| Наценка в процентах 
|PriceEuroMurkup| float64| Наценка в евро
|PriceUahMurkup|  float64| Наценка в грн
|Unit|            float64| Единица измерения по умолчанию "шт"  


**Example JSON :**

| Method|url| Descripton|
|-------|-----------------|------------|
| **POST**  | api/v1/products |Добавление (обновление) по коду 


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


**POST** api/v1/products
```json
[
  {
    "id"                : 12345,
    "code"              : "A-203004044",
    "replace_code"      : "A-203004044",
    "title"             : "Parts for cars",
    "brand_id"          : 1233,
    "brand"             : "BMW",
    "netto"             : "123.89",
    "vendor_id"         : 2354,
    "Vendor_code"       : "C-239003",
    "exchange_eur"      : 32.788,
    "exchange_usd"      : 48.788,
    "price"             : 248.788,
    "description        : "Примечание",
    "markup"            : 20,
    "price_euro_murkup" : 21,
    "price_uah_murkup"  : 24
  },
  {....},
  {....},
  {....}
]
  
```


## Structure

### Структура JSON файла


## Products
|    Поле                | Значение|Наименование|
|------------------------|---------|-----------|
|Id|              int64  | Уникальный номер
|Code|            string | Код товара ID запчати товара
|ReplaceCode|     string | Код замены ID запчати товара
|Title|           string | Наименование Запчасти
|BrandId|         int64  | Brand Id
|Brand|           string | Бренд имя
|Netto|           string | Цена от поставщика в текстовом виде
|VendorId|        int64  | Код поставщика
|VendorCode|      string | Код Запчасти
|ExchangeEur|     float64| Курс в евро
|ExchangeUsd|     float64| Курс в гривнах
|PriceEur|        float64| Цена в евро
|PriceUsd|        float64| Цена в долларах
|PriceUah|        float64| Цена в гривнах
|Description|     string | Примечание
|Markup|          float64| Наценка в процентах 20% по умолчанию
|PriceEuroMurkup| float64|Наценка в евро
|PriceUahMurkup|  float64|Наценка в грн


## Order
|    Поле                | Значение            |Наименование|
|------------------------|---------------------|-----------|
|Id|              int64  | Уникальный номер
|Code|            string | Id клиента в системе (складской) 
|Name|            string | Наименование клиента  
|Total|           float64| Общая сумма счета
|CreateAt|        time   | Дата создания счета

## Order_items
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




















## Structure

// Структура JSON файла
```txt
  Code            string         // Код товара ID запчати товара
  ReplaceCode     string         // Код замены ID запчати товара
  Title           string         // Наименование Запчасти
  BrandId         int64          // Brand Id
  Brand           string         // Бренд имя
  Netto           string         // Цена от поставщика в текстовом виде
  VendorId        int64          // Код поставщика
  VendorCode      string         // Код Запчасти
  ExchangeEur     float64        // Курс в евро
  ExchangeUsd     float64        // Курс в гривнах
  PriceEur        float64        // Цена в евро
  PriceUsd        float64        // Цена в долларах
  PriceUah        float64        // Цена в гривнах
  Description     string         // Примечание
  Markup          float64        // Наценка в процентах 20% по умолчанию
  PriceEuroMurkup float64        // Наценка в евро
  PriceUahMurkup  float64        // Наценка в грн
```

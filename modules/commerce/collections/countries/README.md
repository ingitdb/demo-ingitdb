# 🌍 countries

> ISO 3166-1 alpha-2 country codes with default currency and dialling prefix.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | min_length:2, max_length:2, regex:`^[A-Z]{2}$` | |
| name | string | ✅ | min_length:2, max_length:100 | |
| currency_id | string | ✅ | | [currencies](../../currencies/) |
| phone_prefix | string | ✅ | regex:`^\+\d{1,4}$` | |
| region | string | ❌ | enum: Africa, Americas, Asia, Europe, Oceania | |

### Example Records

| $ID | name | currency_id | phone_prefix | region |
|----|------|:-----------:|:------------:|--------|
| US | United States | USD | +1 | Americas |
| GB | United Kingdom | GBP | +44 | Europe |
| DE | Germany | EUR | +49 | Europe |
| JP | Japan | JPY | +81 | Asia |
| AU | Australia | AUD | +61 | Oceania |

### Referrers of countries

- [customers](../../customers/): country_id
- [addresses](../../addresses/): country_id
- [suppliers](../../suppliers/): country_id
- [tax_rates](../../tax_rates/): country_id

---

## Collection Definition

```yaml
titles:
  en: Countries

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    min_length: 2
    max_length: 2
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^[A-Z]{2}$"
  name:
    type: string
    required: true
    min_length: 2
    max_length: 100
  currency_id:
    type: string
    required: true
    foreign_key: currencies
  phone_prefix:
    type: string
    required: true
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^\\+\\d{1,4}$"
  region:
    type: string
    required: false
    # TODO: enum constraint needs implementation in ColumnDef
    # enum: [Africa, Americas, Asia, Europe, Oceania]

columns_order:
  - "$ID"
  - name
  - currency_id
  - phone_prefix
  - region
```

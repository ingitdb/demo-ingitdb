# 📈 exchange_rates

> Point-in-time exchange rates between currency pairs, used for multi-currency order reporting.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| from_currency_id | string | ✅ | | [currencies](../../currencies/) |
| to_currency_id | string | ✅ | | [currencies](../../currencies/) |
| rate | float | ✅ | min:0 | |
| effective_date | date | ✅ | | |
| source | string | ❌ | max_length:128 | |

### Example Records

| $ID | from_currency_id | to_currency_id | rate | effective_date | source |
|----|:----------------:|:--------------:|-----:|----------------|--------|
| usd-eur-2024-01-01 | USD | EUR | 0.9182 | 2024-01-01 | ECB |
| usd-gbp-2024-01-01 | USD | GBP | 0.7895 | 2024-01-01 | ECB |
| eur-usd-2024-01-01 | EUR | USD | 1.0890 | 2024-01-01 | ECB |
| usd-jpy-2024-01-01 | USD | JPY | 141.45 | 2024-01-01 | ECB |

---

## Collection Definition

```yaml
titles:
  en: Exchange Rates

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  from_currency_id:
    type: string
    required: true
    foreign_key: currencies
  to_currency_id:
    type: string
    required: true
    foreign_key: currencies
  rate:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  effective_date:
    type: date
    required: true
  source:
    type: string
    required: false
    max_length: 128

columns_order:
  - "$ID"
  - from_currency_id
  - to_currency_id
  - rate
  - effective_date
  - source
```

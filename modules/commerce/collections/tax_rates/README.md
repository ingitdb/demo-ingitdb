# 🧾 tax_rates

> Tax rates per country and optional sub-region — applied when computing order tax amounts.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| country_id | string | ✅ | | [countries](../../countries/) |
| region | string | ❌ | max_length:100 | |
| label | string | ✅ | max_length:50 | |
| rate_percent | float | ✅ | min:0, max:100 | |
| effective_date | date | ✅ | | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | country_id | region | label | rate_percent | effective_date | is_active |
|----|:----------:|--------|-------|:------------:|----------------|:---------:|
| us-ca-sales | US | CA | Sales Tax | 8.25 | 2020-01-01 | true |
| us-ny-sales | US | NY | Sales Tax | 8.875 | 2021-03-01 | true |
| de-vat | DE | | VAT | 19.00 | 2021-01-01 | true |
| gb-vat | GB | | VAT | 20.00 | 2011-01-04 | true |
| au-gst | AU | | GST | 10.00 | 2000-07-01 | true |

---

## Collection Definition

```yaml
titles:
  en: Tax Rates

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  country_id:
    type: string
    required: true
    foreign_key: countries
  region:
    type: string
    required: false
    max_length: 100
  label:
    type: string
    required: true
    max_length: 50
  rate_percent:
    type: float
    required: true
    # TODO: min/max value constraints need implementation in ColumnDef
    # min: 0
    # max: 100
  effective_date:
    type: date
    required: true
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - country_id
  - region
  - label
  - rate_percent
  - effective_date
  - is_active
```

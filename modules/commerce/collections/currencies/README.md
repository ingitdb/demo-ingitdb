# 💱 currencies

> ISO 4217 currency definitions — the monetary foundation for all pricing, rates, and orders.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | min_length:3, max_length:3, regex:`^[A-Z]{3}$` | |
| name | string | ✅ | min_length:2, max_length:64 | |
| symbol | string | ✅ | min_length:1, max_length:8 | |
| decimal_places | int | ✅ | min:0, max:4 | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | name | symbol | decimal_places | is_active |
|----|------|--------|:--------------:|:---------:|
| USD | US Dollar | $ | 2 | true |
| EUR | Euro | € | 2 | true |
| GBP | Pound Sterling | £ | 2 | true |
| JPY | Japanese Yen | ¥ | 0 | true |
| AUD | Australian Dollar | A$ | 2 | true |

### Referrers of currencies

- [exchange_rates](../../exchange_rates/): from_currency_id, to_currency_id
- [countries](../../countries/): currency_id
- [customers](../../customers/): preferred_currency_id
- [products](../../products/): currency_id
- [shipping_options](../../shipping_options/): currency_id
- [promotions](../../promotions/): currency_id
- [orders](../../orders/): currency_id
- [order_details](../../orders/): currency_id

---

## Collection Definition

```yaml
titles:
  en: Currencies

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    min_length: 3
    max_length: 3
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^[A-Z]{3}$"
  name:
    type: string
    required: true
    min_length: 2
    max_length: 64
  symbol:
    type: string
    required: true
    min_length: 1
    max_length: 8
  decimal_places:
    type: int
    required: true
    # TODO: min/max value constraints need implementation in ColumnDef
    # min: 0
    # max: 4
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - name
  - symbol
  - decimal_places
  - is_active
```

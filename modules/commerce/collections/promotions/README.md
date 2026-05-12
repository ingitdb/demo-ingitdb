# 🏷️ promotions

> Discount codes and coupon campaigns — applied to orders for percentage or fixed-amount discounts.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| code | string | ✅ | min_length:3, max_length:32, regex:`^[A-Z0-9_\-]+$` | |
| description | string | ❌ | max_length:500 | |
| discount_type | string | ✅ | enum: percent, fixed | |
| discount_value | float | ✅ | min:0 | |
| currency_id | string | ❌ | required when discount_type=`fixed` | [currencies](../../currencies/) |
| min_order_amount | float | ❌ | min:0 | |
| valid_from | date | ✅ | | |
| valid_until | date | ❌ | | |
| max_uses | int | ❌ | min:1 | |
| uses_count | int | ✅ | min:0 | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | code | discount_type | discount_value | currency_id | min_order_amount | valid_from | valid_until | max_uses | uses_count |
|----|------|:-------------:|:--------------:|:-----------:|:----------------:|:----------:|:-----------:|:--------:|:----------:|
| promo-summer24 | SUMMER24 | percent | 10.0 | | 50.00 | 2024-06-01 | 2024-08-31 | 1000 | 342 |
| promo-welcome | WELCOME15 | percent | 15.0 | | | 2023-01-01 | | | 1987 |
| promo-flat20 | FLAT20 | fixed | 20.00 | USD | 100.00 | 2024-01-01 | 2024-12-31 | 500 | 89 |

### Referrers of promotions

- [orders](../../orders/): promotion_id

---

## Collection Definition

```yaml
titles:
  en: Promotions

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  code:
    type: string
    required: true
    min_length: 3
    max_length: 32
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^[A-Z0-9_\\-]+$"
  description:
    type: string
    required: false
    max_length: 500
  discount_type:
    type: string
    required: true
    # TODO: enum constraint needs implementation in ColumnDef
    # enum: [percent, fixed]
  discount_value:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  currency_id:
    type: string
    required: false
    foreign_key: currencies
    # TODO: conditional required (required when discount_type=fixed) needs implementation
  min_order_amount:
    type: float
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  valid_from:
    type: date
    required: true
  valid_until:
    type: date
    required: false
  max_uses:
    type: int
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 1
  uses_count:
    type: int
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - code
  - description
  - discount_type
  - discount_value
  - currency_id
  - min_order_amount
  - valid_from
  - valid_until
  - max_uses
  - uses_count
  - is_active
```

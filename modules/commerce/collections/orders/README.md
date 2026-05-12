# 🛒 orders

> Customer order records — captures the full purchase snapshot at the time of placement.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| customer_id | string | ✅ | | [customers](../../customers/) |
| billing_address_id | string | ✅ | | [addresses](../../addresses/) |
| shipping_address_id | string | ✅ | | [addresses](../../addresses/) |
| shipping_option_id | string | ✅ | | [shipping_options](../../shipping_options/) |
| currency_id | string | ✅ | | [currencies](../../currencies/) |
| promotion_id | string | ❌ | | [promotions](../../promotions/) |
| status | string | ✅ | enum: pending, confirmed, processing, shipped, delivered, cancelled, refunded | |
| subtotal | float | ✅ | min:0 | |
| discount_amount | float | ✅ | min:0 | |
| tax_amount | float | ✅ | min:0 | |
| shipping_amount | float | ✅ | min:0 | |
| total_amount | float | ✅ | min:0 | |
| placed_at | datetime | ✅ | | |
| shipped_at | datetime | ❌ | | |
| delivered_at | datetime | ❌ | | |
| notes | string | ❌ | max_length:1000 | |

### Example Records

| $ID | customer_id | shipping_option_id | currency_id | status | subtotal | discount | tax | shipping | total | placed_at |
|----|------------|:------------------:|:-----------:|:------:|:--------:|:--------:|:---:|:--------:|:-----:|-----------|
| ord-2024-0001 | cust-001 | fedex-standard | USD | delivered | 819.98 | 0.00 | 67.64 | 5.99 | 893.61 | 2024-02-14T10:32:00Z |
| ord-2024-0002 | cust-002 | dhl-economy | EUR | shipped | 1299.00 | 129.90 | 93.53 | 3.99 | 1266.62 | 2024-03-01T16:45:00Z |
| ord-2024-0003 | cust-001 | fedex-express | USD | processing | 19.99 | 0.00 | 1.65 | 14.99 | 36.63 | 2024-03-18T09:10:00Z |

---

## Collection Definition

```yaml
titles:
  en: Orders

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  customer_id:
    type: string
    required: true
    foreign_key: customers
  billing_address_id:
    type: string
    required: true
    foreign_key: addresses
  shipping_address_id:
    type: string
    required: true
    foreign_key: addresses
  shipping_option_id:
    type: string
    required: true
    foreign_key: shipping_options
  currency_id:
    type: string
    required: true
    foreign_key: currencies
  promotion_id:
    type: string
    required: false
    foreign_key: promotions
  status:
    type: string
    required: true
    # TODO: enum constraint needs implementation in ColumnDef
    # enum: [pending, confirmed, processing, shipped, delivered, cancelled, refunded]
  subtotal:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  discount_amount:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  tax_amount:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  shipping_amount:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  total_amount:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  placed_at:
    type: datetime
    required: true
  shipped_at:
    type: datetime
    required: false
  delivered_at:
    type: datetime
    required: false
  notes:
    type: string
    required: false
    max_length: 1000

columns_order:
  - "$ID"
  - customer_id
  - billing_address_id
  - shipping_address_id
  - shipping_option_id
  - currency_id
  - promotion_id
  - status
  - subtotal
  - discount_amount
  - tax_amount
  - shipping_amount
  - total_amount
  - placed_at
  - shipped_at
  - delivered_at
  - notes
```

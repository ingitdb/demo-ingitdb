# 🚀 shipping_options

> Service levels offered by each carrier — defines price, speed tier, and estimated transit days.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| shipper_id | string | ✅ | | [shippers](../../shippers/) |
| name | string | ✅ | min_length:2, max_length:100 | |
| service_level | string | ✅ | enum: economy, standard, express, overnight | |
| base_price | float | ✅ | min:0 | |
| currency_id | string | ✅ | | [currencies](../../currencies/) |
| estimated_days_min | int | ✅ | min:0 | |
| estimated_days_max | int | ✅ | min:0 | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | shipper_id | name | service_level | base_price | currency_id | est. days min | est. days max |
|----|:----------:|------|:-------------:|:----------:|:-----------:|:-------------:|:-------------:|
| fedex-standard | fedex | FedEx Standard | standard | 5.99 | USD | 3 | 5 |
| fedex-express | fedex | FedEx Express | express | 14.99 | USD | 1 | 2 |
| ups-overnight | ups | UPS Overnight | overnight | 29.99 | USD | 1 | 1 |
| dhl-economy | dhl | DHL Economy | economy | 3.99 | USD | 5 | 10 |

### Referrers of shipping_options

- [orders](../../orders/): shipping_option_id

---

## Collection Definition

```yaml
titles:
  en: Shipping Options

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  shipper_id:
    type: string
    required: true
    foreign_key: shippers
  name:
    type: string
    required: true
    min_length: 2
    max_length: 100
  service_level:
    type: string
    required: true
    # TODO: enum constraint needs implementation in ColumnDef
    # enum: [economy, standard, express, overnight]
  base_price:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  currency_id:
    type: string
    required: true
    foreign_key: currencies
  estimated_days_min:
    type: int
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  estimated_days_max:
    type: int
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - shipper_id
  - name
  - service_level
  - base_price
  - currency_id
  - estimated_days_min
  - estimated_days_max
  - is_active
```

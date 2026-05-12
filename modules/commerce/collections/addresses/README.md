# 📍 addresses

> Reusable billing and shipping addresses, each linked to a customer and a country.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| customer_id | string | ✅ | | [customers](../../customers/) |
| label | string | ❌ | max_length:64 | |
| line1 | string | ✅ | min_length:1, max_length:128 | |
| line2 | string | ❌ | max_length:128 | |
| city | string | ✅ | min_length:1, max_length:100 | |
| state | string | ❌ | max_length:100 | |
| postal_code | string | ✅ | min_length:1, max_length:20 | |
| country_id | string | ✅ | | [countries](../../countries/) |
| is_default | bool | ✅ | | |

### Example Records

| $ID | customer_id | label | line1 | city | state | postal_code | country_id | is_default |
|----|-------------|-------|-------|------|-------|:-----------:|:----------:|:----------:|
| addr-001 | cust-001 | Home | 42 Maple Ave | San Francisco | CA | 94102 | US | true |
| addr-002 | cust-001 | Work | 100 Market St Ste 900 | San Francisco | CA | 94105 | US | false |
| addr-003 | cust-002 | Home | Hauptstraße 12 | Berlin | | 10115 | DE | true |
| addr-004 | cust-004 | Home | 15 Baker Street | London | England | W1U 6SB | GB | true |

### Referrers of addresses

- [orders](../../orders/): billing_address_id, shipping_address_id

---

## Collection Definition

```yaml
titles:
  en: Addresses

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
  label:
    type: string
    required: false
    max_length: 64
  line1:
    type: string
    required: true
    min_length: 1
    max_length: 128
  line2:
    type: string
    required: false
    max_length: 128
  city:
    type: string
    required: true
    min_length: 1
    max_length: 100
  state:
    type: string
    required: false
    max_length: 100
  postal_code:
    type: string
    required: true
    min_length: 1
    max_length: 20
  country_id:
    type: string
    required: true
    foreign_key: countries
  is_default:
    type: bool
    required: true

columns_order:
  - "$ID"
  - customer_id
  - label
  - line1
  - line2
  - city
  - state
  - postal_code
  - country_id
  - is_default
```

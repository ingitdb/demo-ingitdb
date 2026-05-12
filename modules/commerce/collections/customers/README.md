# 👤 customers

> Customer accounts — the CRM core record linking contacts, preferences, and order history.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| first_name | string | ✅ | min_length:1, max_length:64 | |
| last_name | string | ✅ | min_length:1, max_length:64 | |
| email | string | ✅ | max_length:254, regex:`^[^@\s]+@[^@\s]+\.[^@\s]+$` | |
| phone | string | ❌ | regex:`^\+\d{7,15}$` | |
| country_id | string | ✅ | | [countries](../../countries/) |
| preferred_currency_id | string | ❌ | | [currencies](../../currencies/) |
| created_at | datetime | ✅ | | |
| is_active | bool | ✅ | | |
| notes | string | ❌ | max_length:1000 | |

### Example Records

| $ID | first_name | last_name | email | phone | country_id | preferred_currency_id | is_active |
|----|-----------|-----------|-------|-------|:----------:|:--------------------:|:---------:|
| cust-001 | Alice | Johnson | alice.johnson@example.com | +14155550101 | US | USD | true |
| cust-002 | Bruno | Müller | bruno.mueller@example.de | +4930555012 | DE | EUR | true |
| cust-003 | Yuki | Tanaka | yuki.tanaka@example.jp | +81312345678 | JP | JPY | true |
| cust-004 | Sarah | Williams | sarah.w@example.co.uk | +447911123456 | GB | GBP | true |

### Referrers of customers

- [addresses](../../addresses/): customer_id
- [orders](../../orders/): customer_id

---

## Collection Definition

```yaml
titles:
  en: Customers

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  first_name:
    type: string
    required: true
    min_length: 1
    max_length: 64
  last_name:
    type: string
    required: true
    min_length: 1
    max_length: 64
  email:
    type: string
    required: true
    max_length: 254
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$"
  phone:
    type: string
    required: false
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^\\+\\d{7,15}$"
  country_id:
    type: string
    required: true
    foreign_key: countries
  preferred_currency_id:
    type: string
    required: false
    foreign_key: currencies
  created_at:
    type: datetime
    required: true
  is_active:
    type: bool
    required: true
  notes:
    type: string
    required: false
    max_length: 1000

columns_order:
  - "$ID"
  - first_name
  - last_name
  - email
  - phone
  - country_id
  - preferred_currency_id
  - created_at
  - is_active
  - notes
```

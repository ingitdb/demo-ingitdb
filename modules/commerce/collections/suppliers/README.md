# 🏭 suppliers

> Vendor and supplier contacts for the products in the catalogue.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| name | string | ✅ | min_length:2, max_length:200 | |
| contact_name | string | ❌ | max_length:100 | |
| email | string | ✅ | max_length:254, regex:`^[^@\s]+@[^@\s]+\.[^@\s]+$` | |
| phone | string | ❌ | regex:`^\+\d{7,15}$` | |
| country_id | string | ✅ | | [countries](../../countries/) |
| website | string | ❌ | max_length:512, regex:`^https?://` | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | name | contact_name | email | country_id | website | is_active |
|----|------|-------------|-------|:----------:|---------|:---------:|
| sup-001 | TechSource Ltd | Jenny Park | supply@techsource.example | US | https://techsource.example | true |
| sup-002 | Computex GmbH | Klaus Werner | orders@computex.example | DE | https://computex.example | true |
| sup-003 | Accessory World | Li Wei | ops@accessoryworld.example | US | https://accessoryworld.example | true |

### Referrers of suppliers

- [products](../../products/): supplier_id

---

## Collection Definition

```yaml
titles:
  en: Suppliers

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  name:
    type: string
    required: true
    min_length: 2
    max_length: 200
  contact_name:
    type: string
    required: false
    max_length: 100
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
  website:
    type: string
    required: false
    max_length: 512
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^https?://"
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - name
  - contact_name
  - email
  - phone
  - country_id
  - website
  - is_active
```

# 🚚 shippers

> Shipping carrier definitions — each shipper may offer multiple service levels.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| name | string | ✅ | min_length:2, max_length:100 | |
| tracking_url_template | string | ❌ | max_length:512 | |
| contact_email | string | ❌ | max_length:254, regex:`^[^@\s]+@[^@\s]+\.[^@\s]+$` | |
| is_active | bool | ✅ | | |

> `tracking_url_template` supports the `{tracking_number}` placeholder — e.g.
> `https://carrier.example/track?n={tracking_number}`.

### Example Records

| $ID | name | tracking_url_template | contact_email | is_active |
|----|------|-----------------------|---------------|:---------:|
| fedex | FedEx | `https://www.fedex.com/apps/fedextrack/?tracknumbers={tracking_number}` | support@fedex.example | true |
| ups | UPS | `https://www.ups.com/track?tracknum={tracking_number}` | support@ups.example | true |
| dhl | DHL | `https://www.dhl.com/en/express/tracking.html?AWB={tracking_number}` | support@dhl.example | true |

### Referrers of shippers

- [shipping_options](../../shipping_options/): shipper_id

---

## Collection Definition

```yaml
titles:
  en: Shippers

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
    max_length: 100
  tracking_url_template:
    type: string
    required: false
    max_length: 512
  contact_email:
    type: string
    required: false
    max_length: 254
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$"
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - name
  - tracking_url_template
  - contact_email
  - is_active
```

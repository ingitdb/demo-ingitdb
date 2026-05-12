# 📦 products

> Product catalogue — each entry has a unique SKU, price, supplier, category, and live stock count.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| sku | string | ✅ | min_length:3, max_length:64, regex:`^[A-Z0-9\-]+$` | |
| name | string | ✅ | min_length:2, max_length:200 | |
| description | string | ❌ | max_length:2000 | |
| category_id | string | ✅ | | [product_categories](../../product_categories/) |
| supplier_id | string | ✅ | | [suppliers](../../suppliers/) |
| image_id | string | ❌ | | [product_images](../../product_images/) |
| unit_price | float | ✅ | min:0.01 | |
| currency_id | string | ✅ | | [currencies](../../currencies/) |
| weight_kg | float | ❌ | min:0 | |
| stock_quantity | int | ✅ | min:0 | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | sku | name | category_id | supplier_id | image_id | unit_price | currency_id | stock_quantity |
|----|-----|------|-------------|-------------|----------|:----------:|:-----------:|:--------------:|
| prod-001 | PHONE-X1-128 | Phone X1 128 GB | smartphones | sup-001 | img-001 | 799.99 | USD | 250 |
| prod-002 | LAPTOP-PRO-15 | Laptop Pro 15" | laptops | sup-002 | img-003 | 1299.00 | USD | 80 |
| prod-003 | CASE-X1-BLK | Phone X1 Black Case | cases | sup-003 | | 19.99 | USD | 500 |

### Referrers of products

- [order_details](../../orders/): product_id

---

## Collection Definition

```yaml
titles:
  en: Products

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  sku:
    type: string
    required: true
    min_length: 3
    max_length: 64
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^[A-Z0-9\\-]+$"
  name:
    type: string
    required: true
    min_length: 2
    max_length: 200
  description:
    type: string
    required: false
    max_length: 2000
  category_id:
    type: string
    required: true
    foreign_key: product_categories
  supplier_id:
    type: string
    required: true
    foreign_key: suppliers
  image_id:
    type: string
    required: false
    foreign_key: product_images
  unit_price:
    type: float
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0.01
  currency_id:
    type: string
    required: true
    foreign_key: currencies
  weight_kg:
    type: float
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  stock_quantity:
    type: int
    required: true
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - sku
  - name
  - description
  - category_id
  - supplier_id
  - image_id
  - unit_price
  - currency_id
  - weight_kg
  - stock_quantity
  - is_active
```

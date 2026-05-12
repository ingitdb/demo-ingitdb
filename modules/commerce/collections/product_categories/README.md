# 🗂️ product_categories

> Hierarchical product taxonomy — categories can nest under a parent category.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| name | string | ✅ | min_length:2, max_length:100 | |
| parent_category_id | string | ❌ | | [product_categories](../../product_categories/) |
| description | string | ❌ | max_length:500 | |
| sort_order | int | ❌ | min:0 | |
| is_active | bool | ✅ | | |

### Example Records

| $ID | name | parent_category_id | sort_order | is_active |
|----|------|--------------------|:----------:|:---------:|
| electronics | Electronics | | 1 | true |
| smartphones | Smartphones | electronics | 1 | true |
| laptops | Laptops | electronics | 2 | true |
| accessories | Accessories | | 2 | true |
| cases | Cases & Covers | accessories | 1 | true |

### Referrers of product_categories

- [product_categories](../../product_categories/): parent_category_id (self-referential)
- [products](../../products/): category_id

---

## Collection Definition

```yaml
titles:
  en: Product Categories

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
  parent_category_id:
    type: string
    required: false
    foreign_key: product_categories
  description:
    type: string
    required: false
    max_length: 500
  sort_order:
    type: int
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0
  is_active:
    type: bool
    required: true

columns_order:
  - "$ID"
  - name
  - parent_category_id
  - description
  - sort_order
  - is_active
```

# 🖼️ product_images

> Shareable product images — a single image record can be referenced by multiple products.

| Column | Type | Required | Constraints | Foreign Key |
|--------|------|:--------:|-------------|-------------|
| $ID | string | ✅ | max_length:64 | |
| url | string | ✅ | max_length:512, regex:`^https?://` | |
| alt_text | string | ✅ | max_length:255 | |
| width_px | int | ❌ | min:1 | |
| height_px | int | ❌ | min:1 | |
| sort_order | int | ❌ | min:0 | |

### Example Records

| $ID | url | alt_text | width_px | height_px |
|----|-----|----------|:--------:|:---------:|
| img-001 | https://cdn.example.com/products/phone-x1-front.jpg | Phone X1 front view | 1200 | 1200 |
| img-002 | https://cdn.example.com/products/phone-x1-back.jpg | Phone X1 rear view | 1200 | 1200 |
| img-003 | https://cdn.example.com/products/laptop-pro-15.jpg | Laptop Pro 15 side view | 1600 | 900 |

### Referrers of product_images

- [products](../../products/): image_id

---

## Collection Definition

```yaml
titles:
  en: Product Images

record_file:
  name: "{key}.yaml"
  type: "map[string]any"
  format: yaml

columns:
  "$ID":
    type: string
    required: true
    max_length: 64
  url:
    type: string
    required: true
    max_length: 512
    # TODO: regex constraint needs implementation in ColumnDef
    # regex: "^https?://"
  alt_text:
    type: string
    required: true
    max_length: 255
  width_px:
    type: int
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 1
  height_px:
    type: int
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 1
  sort_order:
    type: int
    required: false
    # TODO: min value constraint needs implementation in ColumnDef
    # min: 0

columns_order:
  - "$ID"
  - url
  - alt_text
  - width_px
  - height_px
  - sort_order
```

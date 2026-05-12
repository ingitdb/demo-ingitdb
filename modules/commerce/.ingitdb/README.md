# .ingitdb — Database Configuration

This directory contains the inGitDB configuration files for the `demo_commerce_ingitdb` database.

## Files

### `settings.yaml`

Defines the database namespace.

```yaml
default_namespace: demo_commerce_ingitdb
```

### `root-collections.yaml`

Lists all root-level collections and their directory paths.

```yaml
currencies: currencies
exchange_rates: exchange_rates
countries: countries
customers: customers
addresses: addresses
product_categories: product_categories
product_images: product_images
products: products
suppliers: suppliers
shippers: shippers
shipping_options: shipping_options
tax_rates: tax_rates
promotions: promotions
orders: orders
```

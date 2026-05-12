# geo

A small geographic reference database. Exposes one collection:

| Collection | Records | Description |
|------------|---------|-------------|
| `geo.countries` | `countries/$records/{ISO}.json` | Country records with localized names, ISO code, capital, population, area. |

## TODO: deduplicate `countries`

> The [`commerce`](../commerce) module also defines its own `countries` collection (with `currency_id` FK and different columns).
> Long-term these should unify around a single canonical `geo.countries` collection that `commerce` references via foreign key.
> Tracked separately — do not fix in passing.

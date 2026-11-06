# Warehouse tools

Small Python utilities for warehouse order and shipping workflows.

Run the tests with `python3 -m unittest discover -s tests -v`.

## Shipping

`shipping_quote(weight_kg, zone, service="standard")` returns a delivery quote
in dollars. Zones are `local` and `regional`; weights must be positive.

| Service    | Local base | Regional base | Surcharge   |
|------------|-----------|---------------|-------------|
| `standard` | $5.00     | $8.00         | —           |
| `express`  | $5.00     | $8.00         | +$7.00 flat |

The rate formula is `base + 1.50 × weight_kg (+ $7.00 for express)`.

### CLI

```
python -m warehouse.cli <weight_kg> <zone> [--service {standard,express}]
```

Examples:

```bash
# Standard quote — 3 kg, local zone
python -m warehouse.cli 3 local
# → $9.50

# Express quote — 3 kg, local zone
python -m warehouse.cli 3 local --service express
# → $16.50
```

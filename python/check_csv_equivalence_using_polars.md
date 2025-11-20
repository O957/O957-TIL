# Check CSV Equivalence Using Polars

_Today I Learned added on 2025-11-20, learned on 2025-11-20._

I found myself reviewing two PRs made by the same individual and both PRs had a `csv` files containing forecasts. The `csv`s seemed identical, but I wasn't sure, so I wanted a way to check using Python. Given that, at present, I prefer `polars` over `pandas`, I searched `polars` for a method and found that the `equals` (see <https://docs.pola.rs/api/python/stable/reference/dataframe/api/polars.DataFrame.equals.html>) method of the `DataFrame` class satisfied my needs.

Example `csv` file as `example_01.csv`:

```
column_1,column_2
45,98
32,31
17,100
```

Example `csv` file as `example_02.csv`:

```
column_1,column_2
87,98
32,31
17,100
```

First, the non-Python-based, Unix command `diff` (the standard method I've employed for equivalence testing):

```bash
diff example_01.csv example_02.csv

# output:
# 2c2
# < 45,98
# ---
# > 87,98
```

In Python, using `polars`:

```python
import polars as pl


df_01 = pl.read_csv("example_01.csv")
df_02 = pl.read_csv("example_02.csv")

# output: False
df_01.equals(df_02)
```

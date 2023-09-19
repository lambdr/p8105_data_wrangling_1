Data Wrangling I
================

Load necessary packages for this file.

``` r
library(tidyverse)
```

Let’s import the `FAS_litters.csv` csv ysubg a relative path.

``` r
#Load in using read_csv
litters_df =
  read_csv(file = "data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# Clean column names, note "::" accesses a specific function within an unloaded package
litters_df = 
  janitor::clean_names(litters_df)
```

Let’s import the `FAS_litters.csv` csv using an absolute path.

``` r
#Load in using read_csv
litters_df_absolute =
  read_csv(file = "~/Documents/Data Science/data_wrangling_i/data/FAS_litters.csv")

# Clean column names
litters_df_absolute = 
  janitor::clean_names(litters_df_absolute)
```

Don’t use absolute paths. It makes your life more complicated when you
try to move/rename/distribute your work.

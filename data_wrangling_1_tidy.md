Data Wrangling 1: Tidy Data
================
Derek Lamb
2023-09-26

Load all necessary packages.

``` r
library(tidyverse)
library(haven)
```

## PULSE data

``` r
# Load and convert from wide to long format
pulse_df <- read_sas("data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names() |> 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "time",
    values_to = "bdi_score",
    names_prefix = "bdi_score_"
  ) |> 
  
# Recode baseline to 0 months
  mutate(
    time = replace(time, time == "bl", "00m")
  )
  
pulse_df
```

    ## # A tibble: 4,348 × 5
    ##       id   age sex   time  bdi_score
    ##    <dbl> <dbl> <chr> <chr>     <dbl>
    ##  1 10003  48.0 male  00m           7
    ##  2 10003  48.0 male  01m           1
    ##  3 10003  48.0 male  06m           2
    ##  4 10003  48.0 male  12m           0
    ##  5 10015  72.5 male  00m           6
    ##  6 10015  72.5 male  01m          NA
    ##  7 10015  72.5 male  06m          NA
    ##  8 10015  72.5 male  12m          NA
    ##  9 10022  58.5 male  00m          14
    ## 10 10022  58.5 male  01m           3
    ## # ℹ 4,338 more rows

We observe that the BDI is long not wide and so used `pivot_longer` to
make it long.

### Learning Assessment

``` r
litters_df <- read_csv("data/FAS_litters.csv") |> 
  janitor::clean_names() |> 
  pivot_longer(
    gd0_weight:gd18_weight,
    names_to = "gestational_day",
    values_to = "weight"
               ) |> 
  mutate(
    gestational_day = 
      replace(gestational_day, 
              gestational_day == "gd0_weight",0 ),
    gestational_day = 
      replace(gestational_day, 
              gestational_day == "gd18_weight",18 )
    )
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
litters_df
```

    ## # A tibble: 98 × 8
    ##    group litter_number gd_of_birth pups_born_alive pups_dead_birth pups_survive
    ##    <chr> <chr>               <dbl>           <dbl>           <dbl>        <dbl>
    ##  1 Con7  #85                    20               3               4            3
    ##  2 Con7  #85                    20               3               4            3
    ##  3 Con7  #1/2/95/2              19               8               0            7
    ##  4 Con7  #1/2/95/2              19               8               0            7
    ##  5 Con7  #5/5/3/83/3-3          19               6               0            5
    ##  6 Con7  #5/5/3/83/3-3          19               6               0            5
    ##  7 Con7  #5/4/2/95/2            19               5               1            4
    ##  8 Con7  #5/4/2/95/2            19               5               1            4
    ##  9 Con7  #4/2/95/3-3            20               6               0            6
    ## 10 Con7  #4/2/95/3-3            20               6               0            6
    ## # ℹ 88 more rows
    ## # ℹ 2 more variables: gestational_day <chr>, weight <dbl>

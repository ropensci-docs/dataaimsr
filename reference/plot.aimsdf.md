# plot.aimsdf

Plotting options for aimsdf objects

## Usage

``` r
# S3 method for class 'aimsdf'
plot(x, ..., ptype, pars)
```

## Arguments

- x:

  An object of class
  [`aimsdf`](https://docs.ropensci.org/dataaimsr/reference/aimsdf-class.md)
  as returned by
  [`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md).

- ...:

  Not used.

- ptype:

  Type of plot. Can either be "time_series" or "map".

- pars:

  Which parameters to plot? Only relevant if ptype is "time_series"

## Value

An object of class
[`ggplot`](https://ggplot2.tidyverse.org/reference/ggplot.html).

## Details

Currently plots cannot be customised. Summary datasets can only be
represented by maps.

## Examples

``` r
if (FALSE) { # \dontrun{
library(dataaimsr)
wdf <- aims_data("weather", api_key = NULL,
                 filters = list(site = "Yongala",
                                from_date = "2018-01-01",
                                thru_date = "2018-01-02"))
plot(wdf, ptype = "map")
plot(wdf, ptype = "time_series")
# summary-by- datasets can only return maps
sdf <- aims_data("temp_loggers", api_key = NULL,
                 summary = "summary-by-deployment")
plot(sdf, ptype = "map")
} # }
```

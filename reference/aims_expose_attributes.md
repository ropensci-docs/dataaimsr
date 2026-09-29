# Expose available query filters

Expose available query filters which are allowed to be parsed either via
argument `summary` or `filters` in
[`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md)

## Usage

``` r
aims_expose_attributes(target)
```

## Arguments

- target:

  A [`character`](https://rdrr.io/r/base/character.html) vector of
  length 1 specifying the dataset. Only `weather` or `temp_loggers` are
  currently allowed.

## Value

A [`list`](https://rdrr.io/r/base/list.html) of two
[`character`](https://rdrr.io/r/base/character.html) vectors: one
detailing summary modes, another detailing filters.

## Details

Use this function to learn which summary modes and filters are allowed.

We are working on implementing summary visualisation methods for weather
station data. So, for the moment, the options below are only available
for temperature logger data. Three options are available:

- summary-by-seriesExpose summary for all available series; a series is
  a continuing time-series, i.e. a collection of deployments measuring
  the same parameter at the same site. For temperature loggers, series
  is synonymous with sub-site. For weather stations, it is the
  combination of sub-site and parameter.

- summary-by-deploymentExpose summary for all available deployments.

- dailyReturn mean daily aggregated monitoring data .

We offer a list of valid filter names:

- siteFilter by a particular site.

- subsiteFilter by a particular subsite.

- seriesFilter by a particular series.

- series_idA unique identifier for the series - it should be unique
  within a dataset. An alternative to looking up a series by name.

- parameterParameter of interest. Only relevant for weather station data
  because temperature logger is always water temperature.

- min_latMinimum latitude; used to filter by a lat-lon box.

- max_latMaximum latitude; used to filter by a lat-lon box.

- min_lonMinimum longitude; used to filter by a lat-lon box.

- max_lonMaximum longitude; used to filter by a lat-lon box.

- from_dateFilter from time (string of format YYYY-MM-DD).

- thru_dateFilter until time (string of format YYYY-MM-DD).

Some additional options for the actual download, which should be passed
as additional arguments to the function, are:

- sizeSet a page size for large queries (only for the `data` and
  `data-no-key` endpoints).

- cursorUsed for pagination on / data").

- versionRequest the data as recorded at a particular time (a version
  history).

## Author

AIMS Datacentre <adc@aims.gov.au>

## Examples

``` r
if (FALSE) { # \dontrun{
library(dataaimsr)
aims_expose_attributes("weather")
aims_expose_attributes("temp_loggers")
} # }
```

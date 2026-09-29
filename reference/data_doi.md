# AIMS Dataset DOI retriever

Returns DOI for a given dataset

## Usage

``` r
data_doi(target)
```

## Arguments

- target:

  A [`character`](https://rdrr.io/r/base/character.html) vector of
  length 1 specifying the dataset. Only `weather` or `temp_loggers` are
  currently allowed.

## Value

A [`character`](https://rdrr.io/r/base/character.html) vector containing
the dataset DOI string.

## Author

AIMS Datacentre <adc@aims.gov.au>

## Examples

``` r
if (FALSE) { # \dontrun{
library(dataaimsr)
weather_doi <- data_doi("weather")
ssts_doi <- data_doi("temp_loggers")
} # }
```

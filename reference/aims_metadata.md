# Extracts metadata attribute from object of class aimsdf

Extracts metadata attribute from object of class aimsdf

## Usage

``` r
aims_metadata(df_)
```

## Arguments

- df\_:

  A data.frame of class
  [`aimsdf`](https://docs.ropensci.org/dataaimsr/reference/aimsdf-class.md)
  created by function
  [`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md)

## Value

A [`character`](https://rdrr.io/r/base/character.html) vector.

## Details

This function retrieves the metadata attribute from an
[`aimsdf`](https://docs.ropensci.org/dataaimsr/reference/aimsdf-class.md)
object. If the input
[`aimsdf`](https://docs.ropensci.org/dataaimsr/reference/aimsdf-class.md)
object is a summary data.frame (see
?[`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md)),
then output will be an empty string.

## Author

AIMS Datacentre <adc@aims.gov.au>

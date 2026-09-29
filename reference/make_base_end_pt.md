# Expose available query filters

Expose available query filters which are allowed to be parsed either via
argument `summary` or `filters` in
[`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md)

## Usage

``` r
make_base_end_pt(doi, aims_version = NA)
```

## Arguments

- doi:

  A [Digital Object Identifier](https://www.doi.org/) for a chosen [AIMS
  data series](https://open-aims.github.io/data-platform/)

- aims_version:

  A [`character`](https://rdrr.io/r/base/character.html) string defining
  the version of database. Must be "/v1.0" or "-v2.0". If none is
  provided, then "-v2.0" (the most recent) is used.

## Author

AIMS Datacentre <adc@aims.gov.au>

# Retrieve vector of existing filter values

This is a utility function which allows to user to query about the
existing possibilities of a given filter name

## Usage

``` r
aims_filter_values(target, filter_name)
```

## Arguments

- target:

  A [`character`](https://rdrr.io/r/base/character.html) vector of
  length 1 specifying the dataset. Only `weather` or `temp_loggers` are
  currently allowed.

- filter_name:

  A [`character`](https://rdrr.io/r/base/character.html) string
  containing the name of the filter. Must be "site", "subsite",
  "series", or "parameter". See details.

## Value

Either a [`data.frame`](https://rdrr.io/r/base/data.frame.html) if
`filter_name = "series"`, else a
[`character`](https://rdrr.io/r/base/character.html) vector.

## Details

For a full description of each valid filter_name see
?[`aims_expose_attributes`](https://docs.ropensci.org/dataaimsr/reference/aims_expose_attributes.md).
In the temperature logger dataset, "subsite" is equivalent to "series";
moreover, note that there is only one parameter being measured (i.e.
water temperature), so the "parameter" filter contains one single value.

## See also

[`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md),
[`aims_expose_attributes`](https://docs.ropensci.org/dataaimsr/reference/aims_expose_attributes.md)

## Author

AIMS Datacentre <adc@aims.gov.au>

## Examples

``` r
if (FALSE) { # \dontrun{
library(dataaimsr)
aims_filter_values("weather", filter_name = "site")
aims_filter_values("temp_loggers", filter_name = "subsite")
} # }
```

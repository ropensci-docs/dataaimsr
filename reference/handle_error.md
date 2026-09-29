# [`GET`](https://httr.r-lib.org/reference/GET.html) error handler

Displays error status

## Usage

``` r
handle_error(dt_req)
```

## Arguments

- dt_req:

  An URL [`GET`](https://httr.r-lib.org/reference/GET.html) output

## Value

A [`character`](https://rdrr.io/r/base/character.html) vector conveying
the error message.

## Details

This function retrieves the status and content of `dt_req` via the httr
package.

## Author

AIMS Datacentre <adc@aims.gov.au>

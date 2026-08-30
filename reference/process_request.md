# Format [`json_results`](https://docs.ropensci.org/dataaimsr/reference/json_results.md) output

Wrapper function

## Usage

``` r
process_request(dt_req, next_page = FALSE, ...)
```

## Arguments

- dt_req:

  An URL [`GET`](https://httr.r-lib.org/reference/GET.html) output

- next_page:

  Logical. Is this a multi-url request?

- ...:

  Additional arguments to be passed to internal function
  [`update_format`](https://docs.ropensci.org/dataaimsr/reference/update_format.md)

## Value

`aims_data` returns a
[`data.frame`](https://rdrr.io/r/base/data.frame.html) of class
[`aimsdf`](https://docs.ropensci.org/dataaimsr/reference/aimsdf-class.md).

If `summary %in% c("summary-by-series", "summary-by-deployment")`, the
output shows the summary information for the target dataset (i.e.
weather or temperature loggers) (NB: currently, `summary` only works for
the temperature logger database). If `summary` is *not* passed as an
additional argument, then the output contains **raw** monitoring data.
If `summary = "daily"`, then the output contains **mean daily
aggregated** monitoring data. The output also contains five attributes
(empty strings if `summary` is passed as an additional argument):

- `metadata`a [DOI](https://www.doi.org/) link containing the metadata
  record for the data series.

- `citation`the citation information for the particular dataset.

- `parameters`The measured parameters comprised in the output.

- `type`The type of dataset. Either "monitoring" if `summary` is not
  specified, "monitoring (daily aggregation)" if `summary = "daily"`, or
  a "summary-by-" otherwise.

- `target`The input target.

## Details

This function checks for errors in `dt_req` data request and processes
result via
[`json_results`](https://docs.ropensci.org/dataaimsr/reference/json_results.md).

## Author

AIMS Datacentre <adc@aims.gov.au>

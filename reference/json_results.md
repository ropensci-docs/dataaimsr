# [`fromJSON`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html) data request

Wrapper function

## Usage

``` r
json_results(dt_req)
```

## Arguments

- dt_req:

  An URL [`GET`](https://httr.r-lib.org/reference/GET.html) output

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

This function submits a `dt_req` data request via
[`fromJSON`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html).

## Author

AIMS Datacentre <adc@aims.gov.au>

# Further data requests via the AIMS Data Platform API

Similar to
[`page_data`](https://docs.ropensci.org/dataaimsr/reference/page_data.md),
but for cases \#' where there are multiple URLs for data retrieval

## Usage

``` r
next_page_data(url, api_key = NULL, ...)
```

## Arguments

- url:

  A data retrieval URL

- api_key:

  An AIMS Data Platform [API
  Key](https://open-aims.github.io/data-platform/key-request)

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

The AIMS Data Platform R Client provides easy access to data sets for R
applications to the [AIMS Data Platform
API](https://open-aims.github.io/data-platform/). The AIMS Data Platform
requires an API Key for requests, which can be obtained at this
[link](https://open-aims.github.io/data-platform/key-request). It is
preferred that API Keys are not stored in code. We recommend storing the
environment variable `AIMS_DATAPLATFORM_API_KEY` permanently under the
user's `.Renviron` file in order to load the API Key automatically.

There are two types of data currently available through the [AIMS Data
Platform API](https://open-aims.github.io/data-platform/):
[Weather](https://weather.aims.gov.au/#/overview) and [Sea Water
Temperature Loggers](https://tinyurl.com/h93mcojk). They are searched
internally via unique DOI identifiers. Only one data type at a time can
be passed to the argument `target`.

A list of arguments for `filters` can be exposed for both
[Weather](https://weather.aims.gov.au/#/overview) and [Sea Water
Temperature Loggers](https://weather.aims.gov.au/#/overview) using
function
[`aims_expose_attributes`](https://docs.ropensci.org/dataaimsr/reference/aims_expose_attributes.md).

Note that at present the user can inspect the range of dates for the
temperature loggers data only (see usage of argument `summary` in the
examples below). For that, the argument `summary` must be either the
string `"summary-by-series"` or `"summary-by-deployment"`. In those
cases, time filters will be ignored.

Details about available dates for each dataset and time series can be
accessed via Metadata on [AIMS Data Platform
API](https://open-aims.github.io/data-platform/). We raise this caveat
here because these time boundaries are very important; data are
collected at very small time intervals, a window of just a few days can
yield very large datasets. The query will return and error if it reaches
the system's memory capacity.

For that same reason, from version 1.1.0 onwards, we are offering the
possibility of downloading a mean daily aggregated version. For that,
the user must set `summary = "daily"`. In this particular case, query
filter will be taken into account.

## See also

[`aims_filter_values`](https://docs.ropensci.org/dataaimsr/reference/aims_filter_values.md),
[`page_data`](https://docs.ropensci.org/dataaimsr/reference/page_data.md),
[`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md)

## Author

AIMS Datacentre <adc@aims.gov.au>

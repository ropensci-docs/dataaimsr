# Request data via the AIMS Data Platform API

A function that communicates with the the [AIMS Data
Platform](https://open-aims.github.io/data-platform/) via the AIMS Data
Platform API

## Usage

``` r
page_data(
  doi,
  filters = NULL,
  api_key = NULL,
  summary = NA,
  aims_version = NA,
  verbose = FALSE
)
```

## Arguments

- doi:

  A [Digital Object Identifier](https://www.doi.org/) for a chosen [AIMS
  data series](https://open-aims.github.io/data-platform/)

- filters:

  A [`list`](https://rdrr.io/r/base/list.html) containing a set of
  filters for the data query (see Details).

- api_key:

  An AIMS Data Platform [API
  Key](https://open-aims.github.io/data-platform/key-request)

- summary:

  Should summary tables (`"summary-by-series"` or
  `"summary-by-deployment"`) or daily aggregated data ("daily") be
  returned instead of full data (see Details)?

- aims_version:

  A [`character`](https://rdrr.io/r/base/character.html) string defining
  the version of database. Must be "/v1.0" or "-v2.0". If none is
  provided, then "-v2.0" (the most recent) is used.

- verbose:

  Should links be printed to screen? Used for debugging only

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

[`aims_expose_attributes`](https://docs.ropensci.org/dataaimsr/reference/aims_expose_attributes.md),
[`aims_filter_values`](https://docs.ropensci.org/dataaimsr/reference/aims_filter_values.md),
[`aims_data`](https://docs.ropensci.org/dataaimsr/reference/aims_data.md)

## Author

AIMS Datacentre <adc@aims.gov.au>

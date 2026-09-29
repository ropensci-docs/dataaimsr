# AIMS API Key retriever

This function tries to search for an API Key

## Usage

``` r
find_api_key(api_key)
```

## Arguments

- api_key:

  An AIMS Data Platform [API
  Key](https://open-aims.github.io/data-platform/key-request)

## Value

Either a [`character`](https://rdrr.io/r/base/character.html) vector API
Key found in .Renviron or, if missing entirely, an error message.

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

## Author

AIMS Datacentre <adc@aims.gov.au>

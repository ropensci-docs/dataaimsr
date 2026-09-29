# Request data via the AIMS Data Platform API

A function that communicates with the the [AIMS Data
Platform](https://open-aims.github.io/data-platform/) via the AIMS Data
Platform API

## Usage

``` r
aims_data(target, filters = NULL, summary = NA, ...)
```

## Arguments

- target:

  A [`character`](https://rdrr.io/r/base/character.html) vector of
  length 1 specifying the dataset. Only `weather` or `temp_loggers` are
  currently allowed.

- filters:

  A [`list`](https://rdrr.io/r/base/list.html) containing a set of
  filters for the data query (see Details).

- summary:

  Should summary tables (`"summary-by-series"` or
  `"summary-by-deployment"`) or daily aggregated data ("daily") be
  returned instead of full data (see Details)?

- ...:

  Currently unused. Additional arguments to be passed to non-exported
  internal functions.

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

[`aims_citation`](https://docs.ropensci.org/dataaimsr/reference/aims_citation.md),
[`aims_metadata`](https://docs.ropensci.org/dataaimsr/reference/aims_metadata.md),
[`aims_parameters`](https://docs.ropensci.org/dataaimsr/reference/aims_parameters.md)

## Author

AIMS Datacentre <adc@aims.gov.au>

## Examples

``` r
if (FALSE) { # \dontrun{
library(dataaimsr)
# assumes that user already has API key saved to
# .Renviron

# start downloads:
# 1. downloads weather data from
# site Yongala
# within a defined date range
wdf_a <- aims_data("weather", api_key = NULL,
                   filters = list(site = "Yongala",
                                  from_date = "2018-01-01",
                                  thru_date = "2018-01-02"))

# 2. downloads weather data from all sites
# under series_id 64 from Davies Reef
# within a defined date range
wdf_b <- aims_data("weather", api_key = NULL,
                   filters = list(series_id = 64,
                                  from_date = "1991-10-18",
                                  thru_date = "1991-10-19"))
head(wdf_b)
range(wdf_b$time)

# 3. downloads weather data from all sites
# under series_id 64 from Davies Reef
# within defined date AND time range
wdf_c <- aims_data("weather", api_key = NULL,
                   filters = list(series_id = 64,
                                  from_date = "1991-10-18T06:00:00",
                                  thru_date = "1991-10-18T12:00:00"))
head(wdf_c)
range(wdf_c$time)

# 4. downloads all parameters from all sites
# within a defined date range
wdf_d <- aims_data("weather", api_key = NULL,
                   filters = list(from_date = "2003-01-01",
                                  thru_date = "2003-01-02"))
# note that there are multiple sites and series
# so in this case, because we did not specify a specific
# parameter, series within sites could differ by both
# parameter and depth
head(wdf_d)
unique(wdf_d[, c("site", "series_id", "series")])
unique(wdf_d$parameter)
range(wdf_d$time)

# 5. downloads chlorophyll from all sites
# within a defined date range
wdf_e <- aims_data("weather", api_key = NULL,
                   filters = list(parameter = "Chlorophyll",
                                  from_date = "2018-01-01",
                                  thru_date = "2018-01-02"))
# note again that there are multiple sites and series
# however in this case because we did specify a specific
# parameter, series within sites differ by depth only
head(wdf_e)
unique(wdf_e[, c("site", "series_id", "series", "depth")])
unique(wdf_e$parameter)
range(wdf_e$time)

# 6. downloads temperature data
# summarised by series
sdf_a <- aims_data("temp_loggers", api_key = NULL,
                   summary = "summary-by-series")
head(sdf_a)
dim(sdf_a)

# 7. downloads temperature data
# summarised by series
# for all sites that contain data
# within a defined date range
sdf_b <- aims_data("temp_loggers", api_key = NULL,
                   summary = "summary-by-series",
                   filters = list("from_date" = "2018-01-01",
                                  "thru_date" = "2018-12-31"))
head(sdf_b)
dim(sdf_b) # a subset of sdf_a

# 8. downloads temperature data
# summarised by deployment
sdf_c <- aims_data("temp_loggers", api_key = NULL,
                   summary = "summary-by-deployment")
head(sdf_c)
dim(sdf_c)

# 9. downloads temperature data
# within a defined date range, averaged by day
sdf_d <- aims_data("temp_loggers", api_key = NULL, summary = "daily",
                   filters = list(series = "DAVFL1",
                                  from_date = "2018-01-01",
                                  thru_date = "2018-01-10"))
# note again that there are multiple sites and series
# however in this case because we did specify a specific
# parameter, series within sites differ by depth only
head(sdf_d)
unique(sdf_d[, c("site", "series_id", "series", "depth")])
unique(sdf_d$parameter)
range(sdf_d$time)
} # }
```

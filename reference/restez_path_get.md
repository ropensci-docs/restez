# Get restez path

Return filepath to where the restez database is stored.

## Usage

``` r
restez_path_get()
```

## Value

character

## See also

Other setup:
[`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md),
[`restez_path_unset()`](https://docs.ropensci.org/restez/reference/restez_path_unset.md),
[`restez_ready()`](https://docs.ropensci.org/restez/reference/restez_ready.md),
[`restez_status()`](https://docs.ropensci.org/restez/reference/restez_status.md)

## Examples

``` r
library(restez)
# set a restez path with a tempdir
restez_path_set(filepath = tempdir())
#> ... Creating '/tmp/RtmpHnubI1/restez'
#> ... Creating '/tmp/RtmpHnubI1/restez/downloads'
# check what the set path is
(restez_path_get())
#> [1] "/tmp/RtmpHnubI1/restez"
```

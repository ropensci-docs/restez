# Is restez ready?

Returns TRUE if a restez SQL database is available. Use restez_status()
for more information.

## Usage

``` r
restez_ready()
```

## Value

Logical

## See also

Other setup:
[`restez_path_get()`](https://docs.ropensci.org/restez/reference/restez_path_get.md),
[`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md),
[`restez_path_unset()`](https://docs.ropensci.org/restez/reference/restez_path_unset.md),
[`restez_status()`](https://docs.ropensci.org/restez/reference/restez_status.md)

## Examples

``` r
library(restez)
fp <- tempdir()
restez_path_set(filepath = fp)
demo_db_create(n = 5)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
(restez_ready())
#> [1] TRUE
db_delete(everything = TRUE)
(restez_ready())
#> [1] FALSE
```

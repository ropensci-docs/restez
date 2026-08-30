# Delete database

Delete the local SQL database and/or restez folder.

## Usage

``` r
db_delete(everything = FALSE)
```

## Arguments

- everything:

  T/F, delete the whole restez folder as well?

## Details

Any connected database will be automatically disconnected.

## See also

Other database:
[`count_db_ids()`](https://docs.ropensci.org/restez/reference/count_db_ids.md),
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md),
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md),
[`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md),
[`is_in_db()`](https://docs.ropensci.org/restez/reference/is_in_db.md),
[`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)

## Examples

``` r
library(restez)
fp <- tempdir()
restez_path_set(filepath = fp)
#> ... Creating '/tmp/RtmpHnubI1/restez'
#> ... Creating '/tmp/RtmpHnubI1/restez/downloads'
demo_db_create(n = 10)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
db_delete(everything = FALSE)
# Will not run: gb_sequence_get(id = 'demo_1')
# only the SQL database is deleted
db_delete(everything = TRUE)
# Now returns NULL
(restez_path_get())
#> NULL
```

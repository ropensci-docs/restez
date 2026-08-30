# Return the number of ids

Return the number of ids in a user's restez database.

## Usage

``` r
count_db_ids(db = "nucleotide")
```

## Arguments

- db:

  character, database name

## Value

integer

## Details

Requires an open connection. If no connection or db 0 is returned.

## See also

Other database:
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md),
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md),
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md),
[`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md),
[`is_in_db()`](https://docs.ropensci.org/restez/reference/is_in_db.md),
[`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)

## Examples

``` r
library(restez)
restez_path_set(filepath = tempdir())
#> ... Creating '/tmp/RtmpHnubI1/restez'
#> ... Creating '/tmp/RtmpHnubI1/restez/downloads'
demo_db_create(n = 5)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
(count_db_ids())
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> [1] 5

# delete demo after example
db_delete(everything = TRUE)
```

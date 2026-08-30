# Is in db

Determine whether an id(s) is/are present in a database.

## Usage

``` r
is_in_db(id, db = "nucleotide")
```

## Arguments

- id:

  character, sequence accession ID(s)

- db:

  character, database name

## Value

named vector of booleans

## See also

Other database:
[`count_db_ids()`](https://docs.ropensci.org/restez/reference/count_db_ids.md),
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md),
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md),
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md),
[`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md),
[`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)

## Examples

``` r
library(restez)
# set the restez path to a temporary dir
restez_path_set(filepath = tempdir())
#> ... Creating '/tmp/RtmpHnubI1/restez'
#> ... Creating '/tmp/RtmpHnubI1/restez/downloads'
# create demo database
demo_db_create(n = 5)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
# in the demo, IDs are 'demo_1', 'demo_2' ...
ids <- c('thisisnotanid', 'demo_1', 'demo_2')
(is_in_db(id = ids))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> thisisnotanid        demo_1        demo_2 
#>         FALSE          TRUE          TRUE 


# delete demo after example
db_delete(everything = TRUE)
```

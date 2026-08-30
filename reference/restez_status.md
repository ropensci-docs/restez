# Check restez status

Report to console current setup status of restez.

## Usage

``` r
restez_status(gb_check = FALSE)
```

## Arguments

- gb_check:

  Check whether last download was from latest GenBank release? Default
  FALSE.

## Value

Status class

## Details

Set gb_check=TRUE to see if your downloads are up-to-date.

## See also

Other setup:
[`restez_path_get()`](https://docs.ropensci.org/restez/reference/restez_path_get.md),
[`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md),
[`restez_path_unset()`](https://docs.ropensci.org/restez/reference/restez_path_unset.md),
[`restez_ready()`](https://docs.ropensci.org/restez/reference/restez_ready.md)

## Examples

``` r
library(restez)
fp <- tempdir()
restez_path_set(filepath = fp)
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
restez_status()
#> Checking setup status at  ...
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> ────────────────────────────────────────────────────────────────────────────────
#> Restez path ...
#> ... Path '/tmp/RtmpHnubI1/restez'
#> ... Does path exist? 'Yes'
#> ────────────────────────────────────────────────────────────────────────────────
#> Download ...
#> ... Path '/tmp/RtmpHnubI1/restez/downloads'
#> ... Does path exist? 'Yes'
#> ... N. files 0
#> ... Total size 0
#> ... GenBank division selections ''
#> ... GenBank Release '0'
#> ... Last updated ''
#> ────────────────────────────────────────────────────────────────────────────────
#> Database ...
#> ... Path '/tmp/RtmpHnubI1/restez/sql_db'
#> ... Does path exist? 'Yes'
#> ... Total size 780K
#> ... Does the database have data? 'Yes'
#> ... Number of sequences 5
#> ... Min. sequence length '0'
#> ... Max. sequence length 'Inf'
#> ... Last_updated ''
db_delete(everything = TRUE)
# Errors:
# restez_status()
```

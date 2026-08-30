# List database IDs

Return a vector of all IDs in a database.

## Usage

``` r
list_db_ids(db = "nucleotide", n = 100)
```

## Arguments

- db:

  character, database name

- n:

  Maximum number of IDs to return, if NULL returns all

## Value

vector of characters

## Details

Warning: can return very large vectors for large databases.

## See also

Other database:
[`count_db_ids()`](https://docs.ropensci.org/restez/reference/count_db_ids.md),
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md),
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md),
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md),
[`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md),
[`is_in_db()`](https://docs.ropensci.org/restez/reference/is_in_db.md)

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
# Warning: not recommended for real databases
#  with potentially millions of IDs
all_ids <- list_db_ids()
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> Warning: Number of ids returned was limited to [100].
#> Set `n=NULL` to return all ids.


# What shall we do with these IDs?
# ... how about make a mock fasta file
seqs <- gb_sequence_get(id = all_ids)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
defs <- gb_definition_get(id = all_ids)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
# paste together
fasta_seqs <- paste0('>', defs, '\n', seqs)
fasta_file <- paste0(fasta_seqs, collapse = '\n')
cat(fasta_file)
#> >A demonstration sequence | id demo_1
#> AGGCGTCTGC
#> >A demonstration sequence | id demo_2
#> ATCCTTGCAT
#> >A demonstration sequence | id demo_3
#> AAAGCACCGT
#> >A demonstration sequence | id demo_4
#> AAGCATGGAC
#> >A demonstration sequence | id demo_5
#> TTTATGGGTT


# delete after example
db_delete(everything = TRUE)
```

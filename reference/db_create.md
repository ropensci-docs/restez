# Create new NCBI database

Create a new local SQL database from downloaded files. Currently only
GenBank/nucleotide/nuccore database is supported.

## Usage

``` r
db_create(
  db_type = "nucleotide",
  min_length = 0,
  max_length = NULL,
  acc_filter = NULL,
  invert = FALSE,
  alt_restez_path = NULL,
  scan = FALSE
)
```

## Arguments

- db_type:

  character, database type

- min_length:

  Minimum sequence length, default 0.

- max_length:

  Maximum sequence length, default NULL.

- acc_filter:

  Character vector; accessions to include or exclude from the database
  as specified by `invert`.

- invert:

  Logical vector of length 1; if TRUE, accessions in `acc_filter` will
  be excluded from the database; if FALSE, only accessions in
  `acc_filter` will be included in the database. Default FALSE.

- alt_restez_path:

  Alternative restez path if you would like to use the downloads from a
  different restez path.

- scan:

  Logical vector of length 1; should the sequence file be scanned for
  accessions in `acc_filter` prior to processing? Requires zgrep to be
  installed (so does not work on Windows). Only used if `acc_filter` is
  not NULL and `invert` is FALSE. Default FALSE.

## Details

All .seq.gz files are added to the database by default. A user can
specify minimum/maximum sequence lengths or accession numbers to limit
the sequences to be added to the database – smaller databases are faster
to search. The final selection of sequences is the result of applying
all filters (`acc_filter`, `min_length`, `max_length`) in combination.

The `scan` option can decrease the time needed to build a database if
only a small number of sequences should be written to the database
compared to the number of the sequences downloaded from GenBank; i.e.,
if many of the files downloaded from GenBank do not contain any
sequences that should be written to the database. When set to TRUE, if a
file does not contain any of the accessions in `acc_filter`, further
processing of that file will be skipped and none of the sequences it
contains will be added to the database.

Alternatively, a user can use the `alt_restez_path` to add the files
from an alternative restez file path. For example, you may wish to have
a database of all environmental sequences but then an additional smaller
one of just the sequences with lengths below 100 bp. Instead of having
to download all environmental sequences twice, you can generate multiple
restez databases using the same downloaded files from a single restez
path.

This function will not overwrite a pre-existing database. Old databases
must be deleted before a new one can be created. Use
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md)
with everything=FALSE to delete an SQL database.

Connections/disconnections to the database are made automatically.

## See also

Other database:
[`count_db_ids()`](https://docs.ropensci.org/restez/reference/count_db_ids.md),
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md),
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md),
[`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md),
[`is_in_db()`](https://docs.ropensci.org/restez/reference/is_in_db.md),
[`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# Example of general usage
library(restez)
restez_path_set(filepath = 'path/for/downloads/and/database')
db_download()
db_create()

# Example of using `acc_filter`
#
# Download files to temporary directory
temp_dir <- paste0(tempdir(), "/restez", collapse = "")
dir.create(temp_dir)
restez_path_set(filepath = temp_dir)
# Choose GenBank domain 20 ('unannotated'), the smallest
db_download(preselection = 20)
# Only include three accessions in database
db_create(
  acc_filter = c("AF000122", "AF000123", "AF000124")
)
list_db_ids()
db_delete()
unlink(temp_dir)
} # }
```

# Download database

Download .seq.tar files from the latest GenBank release.

## Usage

``` r
db_download(
  db = "nucleotide",
  overwrite = FALSE,
  preselection = NULL,
  max_tries = 1
)
```

## Arguments

- db:

  Database type, only 'nucleotide' currently available.

- overwrite:

  T/F, overwrite pre-existing downloaded files?

- preselection:

  Character vector of length 1; GenBank domains to download. If not
  specified (default), a menu will be provided for selection. To
  specify, provide either a single number or a single character string
  of numbers separated by spaces, e.g. "19 20" for 'Phage' (19) and
  'Unannotated' (20).

- max_tries:

  Numeric vector of length 1; maximum number of times to attempt
  downloading database (default 1).

## Value

T/F, if all files download correctly, TRUE else FALSE.

## Details

In default mode, the user interactively selects the parts (i.e.,
"domains") of GenBank to download (e.g. primates, plants, bacteria ...).
Alternatively, the selected domains can be provided as a character
string to `preselection`.

The `max_tries` argument is useful for large databases that may
otherwise fail due to periodic lapses in internet connectivity. This
value can be set to `Inf` to continuously try until the database
download succeeds (not recommended if you do not have an internet
connection!).

## See also

[`ncbi_acc_get()`](https://docs.ropensci.org/restez/reference/ncbi_acc_get.md)

Other database:
[`count_db_ids()`](https://docs.ropensci.org/restez/reference/count_db_ids.md),
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md),
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md),
[`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md),
[`is_in_db()`](https://docs.ropensci.org/restez/reference/is_in_db.md),
[`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)

## Examples

``` r
if (FALSE) { # \dontrun{
library(restez)
restez_path_set(filepath = 'path/for/downloads')
db_download()
} # }
```

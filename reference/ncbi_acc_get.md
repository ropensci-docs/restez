# Get accession numbers by querying NCBI GenBank

The query string can be formatted using [GenBank advanced query
terms](https://www.ncbi.nlm.nih.gov/nuccore/advanced) to obtain
accession numbers corresponding to a specific set of criteria.

## Usage

``` r
ncbi_acc_get(query, strict = TRUE, drop_ver = TRUE)
```

## Arguments

- query:

  Character vector of length 1; query string to search GenBank.

- strict:

  Logical vector of length 1; should an error be issued if the number of
  unique accessions retrieved does not match the number of hits from
  GenBank? Default TRUE.

- drop_ver:

  Logical vector of length 1; should the version part of the accession
  number (e.g., '.1' in 'AB001538.1') be dropped? Default TRUE.

## Value

Character vector; accession numbers resulting from query.

## Details

Note this queries NCBI GenBank, not the local database generated with
restez.

It can be used either to restrict the accessions used to construct the
local database (`acc_filter` argument of
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md))
or to specify accessions to read from the local database (`id` argument
of
[`gb_fasta_get()`](https://docs.ropensci.org/restez/reference/gb_fasta_get.md)
and other gb\_\*\_get() functions).

## See also

[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md),
[`gb_fasta_get()`](https://docs.ropensci.org/restez/reference/gb_fasta_get.md)

## Examples

``` r
if (FALSE) { # \dontrun{
  # requires an internet connection
  cmin_accs <- ncbi_acc_get("Crepidomanes minutum")
  length(cmin_accs)
  head(cmin_accs)
} # }
```

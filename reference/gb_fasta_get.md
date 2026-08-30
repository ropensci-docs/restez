# Get fasta from GenBank

Get sequence and definition data in FASTA format. Equivalent to
`rettype='fasta'` in
[`rentrez::entrez_fetch()`](https://docs.ropensci.org/rentrez/reference/entrez_fetch.html).

## Usage

``` r
gb_fasta_get(id, width = 70)
```

## Arguments

- id:

  character, sequence accession ID(s)

- width:

  integer, maximum number of characters in a line

## Value

named vector of fasta sequences, if no results found NULL

## See also

[`ncbi_acc_get()`](https://docs.ropensci.org/restez/reference/ncbi_acc_get.md)

Other get:
[`gb_definition_get()`](https://docs.ropensci.org/restez/reference/gb_definition_get.md),
[`gb_organism_get()`](https://docs.ropensci.org/restez/reference/gb_organism_get.md),
[`gb_record_get()`](https://docs.ropensci.org/restez/reference/gb_record_get.md),
[`gb_sequence_get()`](https://docs.ropensci.org/restez/reference/gb_sequence_get.md),
[`gb_version_get()`](https://docs.ropensci.org/restez/reference/gb_version_get.md)

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
(fasta <- gb_fasta_get(id = 'demo_1'))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>                                                           demo_1 
#> ">demo_1.4 A demonstration sequence | id demo_1\nCTTCGTTTAA\n\n" 
(fastas <- gb_fasta_get(id = c('demo_1', 'demo_2')))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>                                                           demo_1 
#> ">demo_1.4 A demonstration sequence | id demo_1\nCTTCGTTTAA\n\n" 
#>                                                           demo_2 
#> ">demo_2.4 A demonstration sequence | id demo_2\nCAGGTAACGA\n\n" 


# delete demo after example
db_delete(everything = TRUE)
```

# Get organism from GenBank

Return the organism name for an accession ID.

## Usage

``` r
gb_organism_get(id)
```

## Arguments

- id:

  character, sequence accession ID(s)

## Value

named vector of definitions, if no results found NULL

## See also

[`ncbi_acc_get()`](https://docs.ropensci.org/restez/reference/ncbi_acc_get.md)

Other get:
[`gb_definition_get()`](https://docs.ropensci.org/restez/reference/gb_definition_get.md),
[`gb_fasta_get()`](https://docs.ropensci.org/restez/reference/gb_fasta_get.md),
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
(org <- gb_organism_get(id = 'demo_1'))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>              demo_1 
#> "Unreal organism 1" 
(orgs <- gb_organism_get(id = c('demo_1', 'demo_2')))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>              demo_1              demo_2 
#> "Unreal organism 1" "Unreal organism 2" 


# delete demo after example
db_delete(everything = TRUE)
```

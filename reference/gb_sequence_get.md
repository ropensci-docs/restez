# Get sequence from GenBank

Return the sequence(s) for a record(s) from the accession ID(s).

## Usage

``` r
gb_sequence_get(id, dnabin = FALSE)
```

## Arguments

- id:

  character, sequence accession ID(s)

- dnabin:

  Logical vector of length 1; should the sequences be returned using the
  bit-level coding scheme of the ape package? Default FALSE.

## Value

named vector of sequences, if no results found NULL

## Details

For more information about the `dnabin` format, see
[`ape::DNAbin()`](https://rdrr.io/pkg/ape/man/DNAbin.html).

## See also

[`ncbi_acc_get()`](https://docs.ropensci.org/restez/reference/ncbi_acc_get.md)

Other get:
[`gb_definition_get()`](https://docs.ropensci.org/restez/reference/gb_definition_get.md),
[`gb_fasta_get()`](https://docs.ropensci.org/restez/reference/gb_fasta_get.md),
[`gb_organism_get()`](https://docs.ropensci.org/restez/reference/gb_organism_get.md),
[`gb_record_get()`](https://docs.ropensci.org/restez/reference/gb_record_get.md),
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
(seq <- gb_sequence_get(id = 'demo_1'))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>       demo_1 
#> "ATAGTTACCC" 
(seqs <- gb_sequence_get(id = c('demo_1', 'demo_2')))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>       demo_1       demo_2 
#> "ATAGTTACCC" "AACATTTAAG" 
(fasta_dnabin <- gb_sequence_get(id = 'demo_1', dnabin = TRUE))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> 1 DNA sequence in binary format stored in a list.
#> 
#> Sequence length: 10 
#> 
#> Label:
#> demo_1
#> 
#> Base composition:
#>   a   c   g   t 
#> 0.3 0.3 0.1 0.3 
#> (Total: 10 bases)

# delete demo after example
db_delete(everything = TRUE)
```

# Entrez fetch

Wrapper for rentrez::entrez_fetch.

## Usage

``` r
entrez_fetch(db, id = NULL, rettype, retmode = "", ...)
```

## Arguments

- db:

  character, name of the database

- id:

  vector, unique ID(s) for record(s)

- rettype:

  character, data format

- retmode:

  character, data mode

- ...:

  Arguments to be passed on to rentrez

## Value

character string containing the file created

## Details

Attempts to first search local database with user-specified parameters,
if the record is missing in the database, the function then calls
rentrez::entrez_fetch to search GenBank remotely.

`rettype='fasta'` and `rettype='gb'` are respectively equivalent to
[`gb_fasta_get()`](https://docs.ropensci.org/restez/reference/gb_fasta_get.md)
and
[`gb_record_get()`](https://docs.ropensci.org/restez/reference/gb_record_get.md).

## Note

It is advisable to call restez and rentrez functions with '::' notation
rather than library() calls to avoid namespace issues. e.g.
restez::entrez_fetch().

## Supported return types and modes

XML retmode is not supported. Rettypes 'seqid', 'ft', 'acc' and 'uilist'
are also not supported.

## See also

[`rentrez::entrez_fetch()`](https://docs.ropensci.org/rentrez/reference/entrez_fetch.html)

## Examples

``` r
library(restez)
restez_path_set(tempdir())
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
# return fasta record
fasta_res <- entrez_fetch(db = 'nucleotide',
                          id = c('demo_1', 'demo_2'),
                          rettype = 'fasta')
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
cat(fasta_res)
#> >demo_1.2 A demonstration sequence | id demo_1
#> ATTAACAGCG
#> 
#> >demo_2.2 A demonstration sequence | id demo_2
#> CCGGCAGAAA
#> 
# return whole GB record in text format
gb_res <- entrez_fetch(db = 'nucleotide',
                       id = c('demo_1', 'demo_2'),
                       rettype = 'gb')
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/RtmpHnubI1/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
cat(gb_res)
#> LOCUS       [This is a mock GenBank data record]
#> DEFINITION  A demonstration sequence | id demo_1
#> ACCESSION   demo_1
#> VERSION     2
#> KEYWORDS    [keyword]
#> SOURCE      [tissue, organism]
#> ORGANISM    Unreal organism 1
#> REFERENCE   [reference data]
#> AUTHORS     [all the authors]
#> TITLE       [title]
#> JOURNAL     [journal]
#> FEATURES    [features]
#> 
#> ORIGIN      
#>         1 attaacagcg
#> 
#> 
#> LOCUS       [This is a mock GenBank data record]
#> DEFINITION  A demonstration sequence | id demo_2
#> ACCESSION   demo_2
#> VERSION     2
#> KEYWORDS    [keyword]
#> SOURCE      [tissue, organism]
#> ORGANISM    Unreal organism 2
#> REFERENCE   [reference data]
#> AUTHORS     [all the authors]
#> TITLE       [title]
#> JOURNAL     [journal]
#> FEATURES    [features]
#> 
#> ORIGIN      
#>         1 ccggcagaaa
#> 
#> 
# NOT RUN
# whereas these request would go through rentrez
# fasta_res <- entrez_fetch(db = 'nucleotide',
#                           id = c('S71333', 'S71334'),
#                           rettype = 'fasta')
# gb_res <- entrez_fetch(db = 'nucleotide',
#                        id = c('S71333', 'S71334'),
#                        rettype = 'gb')

# delete demo after example
db_delete(everything = TRUE)
```

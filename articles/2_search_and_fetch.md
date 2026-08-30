# 2. How to search for and fetch sequences

A downside of the `restez` approach is we are unable to then search the
local database for sequences of interest as the database cannot possibly
contain sufficient metadata (most notably taxonomic information) to
perform as rich a search as online via NCBI. As a result we must perform
the sequence discovery process independently from `restez`. In this
tutorial we will demonstrate how to perform online searches using the
`rentrez` package and then use the search results to look up sequences
in a `restez` database.

To run all the code in this tutorial you will need to have already set
up the rodents database, see [Build a database of all
rodents](https://ropensci.github.io/restez/articles/1_rodents.html).

## Search NCBI GenBank accession numbers

Let’s pretend we’re interested in COI sequences for a group of rodents
called the Sciuromorpha. `restez` provides the
[`ncbi_acc_get()`](https://docs.ropensci.org/restez/reference/ncbi_acc_get.md)
function to make this easy: just provide a text string query [like you
would on NCBI GenBank](https://www.ncbi.nlm.nih.gov/books/NBK49540/),
and it returns a character vector of accession numbers corresponding to
that query. By default, it drops any version number after each accession
number. This is not strictly necessary, but it makes it easier to check
our results from `restez` later.

``` r

library(restez)

# 33553 - Sciuromorpha - squirrel-like things
accessions <- ncbi_acc_get(
  'txid33553[Organism:exp] AND COI [GENE] AND 100:1000[SLEN]')
print(length(accessions))
#> [1] 492
print(accessions[1:10])
#>  [1] "MZ661159" "MZ364430" "HQ966965" "GU670702" "GU670701" "GU670700" "GU670699" "GU670462" "GU670451" "GU670450"
```

## Retrieve sequences

To fetch the sequences from the rodents database, we can use the
`gb_fasta_get` function.

``` r

restez_path_set(rodents_path)
coi_sequences <- gb_fasta_get(id = accessions)
str(coi_sequences[[1]])
#>  chr ">LT630607.1 Sciurus sp. 1 AG-2016 mitochondrial partial COI gene for cytochrome oxidase subunit 1, specimen vou"| __truncated__
# Are all accessions in results?
all(accessions %in% names(coi_sequences))
#> [1] TRUE
```

## Comparing to Entrez

Can we not just use `rentrez` to do the fetching as well? Yes, but
`restez` can be a lot faster. NCBI limits the number of requests per
user, often to as little as 100 items per request with varying time
delays. Additionally for any programmatic retrieval of sequences using
an online server can never be as reliable as a local copy.

``` r

# time via restez
system.time(expr = {
  coi_sequences <- gb_fasta_get(id = accessions)
  })
#>    user  system elapsed 
#>   0.259   0.077   0.272
# time via Entrez
system.time(expr = {
  coi_sequences_p1 <- rentrez::entrez_fetch(db = 'nucleotide',
                                            id = accessions[1:100],
                                            rettype = 'fasta')
  coi_sequences_p2 <- rentrez::entrez_fetch(db = 'nucleotide',
                                            id = accessions[101:200],
                                            rettype = 'fasta')
  coi_sequences_p3 <- rentrez::entrez_fetch(db = 'nucleotide',
                                            id = accessions[201:300],
                                            rettype = 'fasta')
  coi_sequences_p4 <- rentrez::entrez_fetch(db = 'nucleotide',
                                            id = accessions[301:400],
                                            rettype = 'fasta')
  coi_sequences_p5 <- rentrez::entrez_fetch(db = 'nucleotide',
                                            id = accessions[401:456],
                                            rettype = 'fasta')
  })
#>    user  system elapsed 
#>   0.050   0.008   5.536
```

## Next up

**[Advanced parsing of a GenBank
record](https://docs.ropensci.org/restez/articles/3_parsing.html)**

# Create and Query a Local Copy of GenBank in R

## 1. Download GenBank

In the first section of this introduction to `restez` we will explain
how to download parts of GenBank on to your computer and from these
downloads, construct a local database. GenBank can be downloaded from
NCBI using the File Transfer Protocol (FTP), the online portal for these
downloads can be viewed from your web browser, [FTP NCBI
GenBank](ftp://ftp.ncbi.nlm.nih.gov/genbank/). GenBank is hosted at this
portal as 1000s of compressed sequence files called flatfiles. New
versions of these flatfiles are released once a month as new sequence
information is uploaded. For information on the latest GenBank release,
see the [NCBI statistics
page](https://www.ncbi.nlm.nih.gov/genbank/statistics/).

`restez` downloads a selection of these flatfiles and unpacks them into
an SQL-like database (specifically, [DuckDB](https://duckdb.org/)) that
can be queried using `restez`’s functions. Because there are potentially
huge amounts of sequence information, all of which is unlikely to be of
interest to a user, `restez` allows you to select the sets of flatfiles
to download based on GenBank’s domains. For the most part these sets of
flatfile types are determined by taxonomy, for example, a user can
download all primate or plant sequences.

Here, we will explain how to set up `restez`, download genbank and then
create a database from the downloaded files.

### 1.1 Setting up

Before we can download anything, we need to tell `restez` where we would
like to store the downloaded files and the eventual GenBank database. To
do this we use the
[`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md)
function. With this function a user can provide a system file path to a
folder within which the function will create a new folder called
‘restez’. In this example, we will create a `restez` folder in a
temporary folder.

``` r

# set a random number generator seed for reproducibility
set.seed(12345)

library(restez)
# rstz_pth <- tempdir()
restez_path_set(filepath = rstz_pth)
#> ... Creating '/tmp/Rtmp8CGZGK/restez'
#> ... Creating '/tmp/Rtmp8CGZGK/restez/downloads'
```

A user must always set the `restez` path in order to use the `restez`
library. Additionally, by running
[`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md)
on a new folder messages are printed to console telling us that the path
was created and that a downloads subfolder was created.

> **Note**, whenever you intend to use `restez` you will need to specify
> the `restez` path. If you are using it regularly, it might be a good
> idea to set it using your .Rprofile.
> [`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md)
> only needs to be run once per R session, but we will use it repeatedly
> in the chunks below just as a reminder.

### 1.2 Download

Now we can download GenBank files using
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md).
This is an interactive function that looks up the latest GenBank
release, parses the release notes, and prints to console the available
sets of flatfiles that can be downloaded. For this example, we will
select the smallest available domain which is ‘Unannotated’ and can be
pre-specified with ‘20’. Note that the numbering scheme may change
between GenBank releases, so you shouldn’t assume a given number will
correspond to the same domain if you run it again later. Instead, you
can run this function without the `preselection` argument and wait for
the function to prompt you for a domain selection, which will show the
current numbering scheme.

After launching, the download function will ask you whether it is OK to
download and set up a database for the selected sequence files. If the
selection is likely to be large you can always quit the process using
either `Esc` or `Ctrl+c`. Please note that the diskspace estimates are
preliminary. The package tries to be conservative in its estimates.

``` r

db_download(preselection = '20')
#> ────────────────────────────────────────────────────────────────────────────────
#> Looking up latest GenBank release ...
#> ... release number 2730
#> ... found 8535 sequence files
#> ────────────────────────────────────────────────────────────────────────────────
#> Which sequence file types would you like to download?
#> Choose from those listed below:
#> • 1  - 'Plant (including fungi and algae)'
#>         3343 files and 4050 GB
#> • 2  - 'Invertebrate'
#>         2676 files and 3830 GB
#> • 3  - 'Other vertebrate'
#>         695 files and 998 GB
#> • 4  - 'Bacterial'
#>         518 files and 774 GB
#> • 5  - 'Viral'
#>         346 files and 518 GB
#> • 6  - 'Other mammalian'
#>         244 files and 345 GB
#> • 7  - 'EST (expressed sequence tag)'
#>         164 files and 245 GB
#> • 8  - 'Rodent'
#>         144 files and 203 GB
#> • 9  - 'Patent'
#>         94 files and 141 GB
#> • 10 - 'GSS (genome survey sequence)'
#>         79 files and 117 GB
#> • 11 - 'Constructed'
#>         68 files and 102 GB
#> • 12 - 'Environmental sampling'
#>         53 files and 78.2 GB
#> • 13 - 'TSA (transcriptome shotgun assembly)'
#>         37 files and 54.2 GB
#> • 14 - 'Primate'
#>         28 files and 39.7 GB
#> • 15 - 'HTGS (high throughput genomic sequencing)'
#>         25 files and 36.6 GB
#> • 16 - 'Synthetic and chimeric'
#>         10 files and 13 GB
#> • 17 - 'Phage'
#>         4 files and 4.76 GB
#> • 18 - 'HTC (high throughput cDNA sequencing)'
#>         3 files and 3.49 GB
#> • 19 - 'STS (sequence tagged site)'
#>         3 files and 4.43 GB
#> • 20 - 'Unannotated'
#>         1 files and 0.00816 GB
#> Provide one or more numbers separated by spaces.
#> e.g. to download all Mammalian sequences, type: "6 8 14" followed by Enter
#> 
#> Which files would you like to download?
#> ────────────────────────────────────────────────────────────────────────────────
#> You've selected a total of 1 file(s) and 0.00816 GB of uncompressed data.
#> These represent: 
#> • 'Unannotated'
#> 
#> Based on stated GenBank files sizes, we estimate ... 
#> ... 0.00163 GB for  compressed, downloaded files
#> ... 0.00996 GB for the SQL database
#> Leading to a total of 0.0116 GB
#> 
#> Please note, the real sizes of the database and its downloads cannot be
#> accurately predicted beforehand.
#> These are just estimates, actual sizes may differ by up to a factor of two.
#> 
#> Is this OK?
#> ────────────────────────────────────────────────────────────────────────────────
#> Downloading ...
#> ... 'gbuna1.seq' (1/1)
#> Done. Enjoy your day.
```

Now the download has begun, we just need to wait for it to finish. For
the largest domains, this can take quite a while and may be prone to
server errors. In this case, you may want to set the `max_tries`
argument of
[`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md)
to a relatively high number to automatically re-try downloading until
that number of tries is exceeded (in this case, be sure to set
`overwrite` to `FALSE` or the download will start over from scratch).

### 1.3 Create a database

After the download has completed, we need to use
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md)
to create our local database. This looks in the downloads folder of our
`restez` path, breaks these files up into separate GenBank records and
adds them to the SQL-like database. Again, for very large collections of
sequences this can take quite a while.

``` r

db_create()
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> Inspecting 1 file(s) to add to the database ...
#> ... 'gbuna1.seq.gz' (1/1)
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> Done.
```

[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md)
allows a user to specify minimum and maximum sequence lengths. It’s
always a good idea to limit the number of sequences in a database so
that look-up times are faster. If you know you are only interested in
certain lengths of sequences it is a good idea to limit the sequences in
the database at this stage. This can also be done with the `acc_filter`
argument, as described in the [“Tips and Tricks”
vignette](https://docs.ropensci.org/restez/articles/5_tips_and_tricks.html).
You can always run
[`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md)
again to change the limits. You will simply need to delete the original
database first with
[`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md).

### 1.4 Checking the setup

After the download and the database creation steps are complete, we can
confirm our setup using
[`restez_status()`](https://docs.ropensci.org/restez/reference/restez_status.md).

``` r

restez_path_set(rstz_pth)
restez_status()
#> Checking setup status at  ...
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> ────────────────────────────────────────────────────────────────────────────────
#> Restez path ...
#> ... Path '/tmp/Rtmp8CGZGK/restez'
#> ... Does path exist? 'Yes'
#> ────────────────────────────────────────────────────────────────────────────────
#> Download ...
#> ... Path '/tmp/Rtmp8CGZGK/restez/downloads'
#> ... Does path exist? 'Yes'
#> ... N. files 2
#> ... Total size 3.21M
#> ... GenBank division selections 'Unannotated'
#> ... GenBank Release 2730
#> ... Last updated '2026-08-30 07:14:24.954651'
#> ────────────────────────────────────────────────────────────────────────────────
#> Database ...
#> ... Path '/tmp/Rtmp8CGZGK/restez/sql_db'
#> ... Does path exist? 'Yes'
#> ... Total size 9.76M
#> ... Does the database have data? 'Yes'
#> ... Number of sequences 1086
#> ... Min. sequence length 0
#> ... Max. sequence length Inf
#> ... Last_updated '2026-08-30 07:14:26.409356'
```

The status function allows a user to always touch base with their
`restez` set-up. It can be run at any point, before and/or after
download or database creation. It is also designed to provide useful
messages to a user for what they need to do next in order for them to
make queries to their database. If you ever get confused, run
[`restez_status()`](https://docs.ropensci.org/restez/reference/restez_status.md)
to see what is happening.

Additionally, if you are developing your own functions that depend on
`restez`, you can use
[`restez_ready()`](https://docs.ropensci.org/restez/reference/restez_ready.md)
which will simply return TRUE or FALSE on whether the database can be
queried.

``` r

restez_path_set(rstz_pth)
if (restez_ready()) {
  print('Database is ready to be queried!')
} else {
  print('Database cannot be queried :-(')
}
#> [1] "Database is ready to be queried!"
```

## 2. Query

Once a restez database has been set up we can query the database using
the `gb_*_get()` functions. These functions allow us to retrieve
specific columns in the SQL-like database: ‘sequence’, ‘definition’,
‘accession’, ‘version’ and ‘organism’. Also, they allow us to get the
whole text formatted record and sequence data in fasta format. In this
example, we can use
[`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)
to identify accession numbers in the database. We could also use
`entrez_search()` provided the database contains sequences of interest
to us, see [‘search and
fetch’](https://docs.ropensci.org/restez/articles/2_search_and_fetch.html).

``` r

restez_path_set(rstz_pth)
ids <- suppressWarnings(list_db_ids(db = 'nucleotide', n = 100))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
(id <- sample(ids, 1))
#> [1] "AH000952"
# sequence
str(gb_sequence_get(id))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>  Named chr "GGGGTCTGACGCTCAGTGGAACGAAAACTCACGTTAAGGGATTTTGGTCATGAGATTATCAAAAAGGATCTTCACCTAGATCCTTTTAAATTAAAAATGAAGTTTTAAATC"| __truncated__
#>  - attr(*, "names")= chr "AH000952"
# definition
(gb_definition_get(id))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>                                                                                AH000952 
#> "Transposon Tn3 transposon Tn3 ampicillin resistance (amp-r) product gene, partial cds"
# version
(gb_version_get(id))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>     AH000952 
#> "AH000952.2"
# organism
(gb_organism_get(id))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#>         AH000952 
#> "Transposon Tn3"
# fasta
cat(gb_fasta_get(id))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> >AH000952.2 Transposon Tn3 transposon Tn3 ampicillin resistance (amp-r) product gene, partial cds
#> GGGGTCTGACGCTCAGTGGAACGAAAACTCACGTTAAGGGATTTTGGTCATGAGATTATCAAAAAGGATC
#> TTCACCTAGATCCTTTTAAATTAAAAATGAAGTTTTAAATCAATCTAAAGTATATATGAGTAAACTTGGT
#> CTGACAGTTACCAATGCTTAATCAGTGAGGCACCTATCTCAGCGATCTGTCTATTTCGTTCATCCATAGT
#> TGCCTGACTCCCCGTCGTGTAGATAACTACGATACGGGAGGGCTTACCATCTGGCCNNNNNNNNNNNNNN
#> NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
#> NNNNNNNNNNNNNNNNGGCCATTATTCCTTCACGCTGGCAGAACTGGTGACCAAAGGTCATCTGAGACCA
#> TTAAAAGAGGCGTCAGAGGCAGAAAACGTTGCTTAACGTGAGTTTTCGTTCCACTGAGCGTCAGACCCC
# Note, for large databases these requests can take a long time to complete.
# Always try and limit the size of the database by specifying min and max
# sequence lengths with db_create()
# Also note, if an id is not present in the database nothing is returned
cat(gb_fasta_get(id = c(id, 'notanid')))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> >AH000952.2 Transposon Tn3 transposon Tn3 ampicillin resistance (amp-r) product gene, partial cds
#> GGGGTCTGACGCTCAGTGGAACGAAAACTCACGTTAAGGGATTTTGGTCATGAGATTATCAAAAAGGATC
#> TTCACCTAGATCCTTTTAAATTAAAAATGAAGTTTTAAATCAATCTAAAGTATATATGAGTAAACTTGGT
#> CTGACAGTTACCAATGCTTAATCAGTGAGGCACCTATCTCAGCGATCTGTCTATTTCGTTCATCCATAGT
#> TGCCTGACTCCCCGTCGTGTAGATAACTACGATACGGGAGGGCTTACCATCTGGCCNNNNNNNNNNNNNN
#> NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
#> NNNNNNNNNNNNNNNNGGCCATTATTCCTTCACGCTGGCAGAACTGGTGACCAAAGGTCATCTGAGACCA
#> TTAAAAGAGGCGTCAGAGGCAGAAAACGTTGCTTAACGTGAGTTTTCGTTCCACTGAGCGTCAGACCCC
```

Additionally, for more flexibility and options for extracting sequence
record information see [GenBank record
parsing](https://docs.ropensci.org/restez/articles/3_parsing.html).

## 3. Entrez

Entrez wrappers are part of the `restez` package. These allow a user to
make use of the local GenBank using functions that were built for
[`rentrez`](https://github.com/ropensci/rentrez). This minimizes the
amount of coding changes required for any Entrez dependent code.

> Currently, only
> [`entrez_fetch()`](https://docs.ropensci.org/restez/reference/entrez_fetch.md)
> is available with restez and only text formatted rettypes are allowed.

``` r

restez_path_set(rstz_pth)
ids <- suppressWarnings(list_db_ids(db = 'nucleotide', n = 100))
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
(id <- sample(ids, 1))
#> [1] "AF298087"
# get fasta sequences with entrez
res <- restez::entrez_fetch(db = 'nucleotide', id = id, rettype = 'fasta')
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
cat(res)
#> >AF298087.1 Unidentified clone A5 DNA sequence from ocean beach sand
#> GATCCGGTCNTCGCGCTTTGCGCCTCGCGGATCTCGCGCACCTGCAGCTGGGTCACCAGCGGCGAGATGA
#> TGGTGCCTAGCAGCAGCCCGAAGACCACCATCACCACCAGGATCTCGATCAGGGTGAAGCCCTGGTCAGG
#> ACGCCGGCTCACGGCGCGGGCGGTGGCTTCGCGGCGCATCACAGGCACGGCCTTGCTGGCGTGGTTGGGG
#> GCGGCACTGGATTATTGCAGGCCACCATTTCCAGGTAATCGTTAAAGCCCATCTTACGTGCCGTGCGCTC
#> CATGAGCAGGTCGACACCATTCGCGTTGTCTTCCTCGAAGCCGGCCTGGCCGGGAGTCGCCAGGGTGAGG
#> TCCTGCGTTGGCGCAAGCTCACCGCTCACGATCACCACCGCGTGGGCATCGTCCACGACTGAAGCCCCAT
#> CGGCGACGTTGACGACGACGCANTCGCCTCCGACGGTGCAGGGGTCGGACGGGCCCCCGGCTCCNGTGGG
#> GCTGAAGCCGTTGGCGTANCTCGCATANACAAACTGNGCCCACCGTTCTCGGNGAACCANGCGGGAGATC
#> CCAGGGTTTCCGGGCCTG
# entrez_fetch will also search via Entrez for any ids not in the db
plant_sequence <- 'AY952423'
res <- restez::entrez_fetch(db = 'nucleotide', id = c(id, plant_sequence),
                            rettype = 'fasta')
#> duckdb keeps downloaded extensions and secrets in a temporary directory:
#> ℹ /tmp/Rtmp8CGZGK/duckdb
#> This is removed when the R session ends.
#> • Extensions are re-downloaded each session.
#> • Secrets are lost.
#> ℹ Run duckdb(shared_home = TRUE) (or create ~/.duckdb) to keep them (suitable for most users).
#> ℹ Run duckdb(shared_home = FALSE) to accept the temporary directory (and silence this message).
#> ℹ See ?duckdb_storage for details and alternatives.
#> [1] id(s) are unavailable locally, searching online.
cat(res)
#> >AF298087.1 Unidentified clone A5 DNA sequence from ocean beach sand
#> GATCCGGTCNTCGCGCTTTGCGCCTCGCGGATCTCGCGCACCTGCAGCTGGGTCACCAGCGGCGAGATGA
#> TGGTGCCTAGCAGCAGCCCGAAGACCACCATCACCACCAGGATCTCGATCAGGGTGAAGCCCTGGTCAGG
#> ACGCCGGCTCACGGCGCGGGCGGTGGCTTCGCGGCGCATCACAGGCACGGCCTTGCTGGCGTGGTTGGGG
#> GCGGCACTGGATTATTGCAGGCCACCATTTCCAGGTAATCGTTAAAGCCCATCTTACGTGCCGTGCGCTC
#> CATGAGCAGGTCGACACCATTCGCGTTGTCTTCCTCGAAGCCGGCCTGGCCGGGAGTCGCCAGGGTGAGG
#> TCCTGCGTTGGCGCAAGCTCACCGCTCACGATCACCACCGCGTGGGCATCGTCCACGACTGAAGCCCCAT
#> CGGCGACGTTGACGACGACGCANTCGCCTCCGACGGTGCAGGGGTCGGACGGGCCCCCGGCTCCNGTGGG
#> GCTGAAGCCGTTGGCGTANCTCGCATANACAAACTGNGCCCACCGTTCTCGGNGAACCANGCGGGAGATC
#> CCAGGGTTTCCGGGCCTG
#> 
#> >AY952423.1 Livistona chinensis tRNA-Lys (trnK) gene, partial sequence; and matK gene, complete sequence; chloroplast
#> ATTGGGGTTGCTAACTCAACGGTAGAGTACTCGGCTTTTAAGTGCGACTATCATCTTTTACACATTTGGA
#> TGAAGTAAGGAATTCGTCCAGACTATTGGTAGAGTCTATAAGACCACGACTGATCCTGAAAGGTAATGAA
#> TGGAAAAAATAGCATGTCGTACGTAATACAATGAGAAACTTGTAATTTCTTATTGTAATTTTTTAAGTAG
#> AACTTTGAGTTTATCCTTACTGGATCATTACAAAAATATTGTATTTTATTTTTGGAAGGGGACGAAAAAA
#> AGGAAATTCCCAACATTTATTGTTTGGTCTAATGAATAAATGGATAGGGGCCTAGGGTAGGGCCCAATTT
#> TTGTAAAACAAAAAGCAACGAGCTTATGTTCTTAATTTGAATAATTACCCGATCTAATTAGATGTTAAAA
#> ATAAATTAGTGCCAGATGTGGTAAAGGGTTCTACTGTAAGTGGACCTTTTTTTTTTTTTTTTATGAATCC
#> TACCTATTATCTATTATGGATTAAAGATGGATGTGTATAAGAAGAAGTATACTGATAAAGAGAATTTTTC
#> CAAAGTCAAAAGAGCAATCGGGTTGCAAAAATAAAGGATTTTTACCTCCGAGAATTATAAATTAATTGGA
#> TCAAAAGGAGAGGAAAAAGTCTGTGATTGGACTCCTTCTATCCGCGGGTATGGGTATATAGTAGGTATAT
#> ATGTATATTTGTATACTATATAAATTACATGCCCTGTTCTGACCGTATTGCACTATGTATTATTTGATAA
#> TCCAAGAAATGCCTCCTACTTCTGGTTCAAGTAGAAATGAAAATAGAAGAATTACAAGAATATTTAGAAA
#> AAGATAGATCTCGGCAACAACACTTCCTATACCCACTTTTCTTTCAGGAGTATATTTATGCACTTGCTCA
#> TGATTATGGGTTTAAAGGGTTCGATTTTTTACGAACCTATGGAAATTGGGGGTTATGATAATAAATCTAG
#> TTCAGTACTTGTAAAACATTTAATTACTCGAATGTATCAACAGAATTATTTGATTTATTCTGTTAATGAA
#> TCTAACCAAAATCGATTGATTGAGCATAACAATTCTTTTTATTCTCAAATGATATCTGAAGTTTTTGCGA
#> TCATTGCAGAAATTCCATTCTCTCAGCAATTACTATTTTCTCTTCGAGGAAAAAAGAATACCAAAATCTC
#> AGACTTTACGATCTATTCATTCAATATTTCCCTTTTTAGAAGACAAATTATCACATTTAAACTATGTGTC
#> AGATATATTAATACCCTATCCCATCCATTTGGAAATCTTGGTGCAAATTCTTCAATGCTGGATCCAAGAT
#> GTTTCTTCTTTGCATTTATTGCGATTCTTTCTCCACGAACATCATAATGGGAATAGTTTTTTTTTTCCAA
#> AGAAATCCTTTTCAAAAGAAAATAAAAGACTCTTTCGATTCCTATATAATTCTTATGTATCTGAATGTGA
#> ATTTGTCTTAGTGTTTCTTCGTAAACAATCCTCTTATTTACAATCAAAATCCTATGGAATCTTTCTTGAG
#> CGAACACATTTCTATGGAAGAATGGAACATCTTATAGTAGTGTGTCATAATTATTGTCAGAAGGCCTTTT
#> GGGTCTTCAAGGATCCTTTTATGCATTATGTTCGATATCAAGGAAAAGCAATTCTGGCATCAAAAGGATC
#> TTATCTTTTGATGAAGAAATGGAGATGTCATCTTGTCAATTTCTGGCAATATTATTTTCATTTTTGGGCT
#> CAGCCTTACAGAATTTCAATAAACCAATTAGGAAATCATTCCTTCTATTTTCTCGGTTATCTTTCAAGTG
#> TATTAAAAAATACTTCGTCTGTAAGGAATCAAATGCTAGAGAATTCCTTTTTAATAGATACTATTACTAA
#> TAAATTGGATACCATAGTCCCAGTTCTTCCTCTTATTGGATCTTTGTCTAAAGCTAAATTTTGTACCGTA
#> TCCGGGCATCCTAGTAGTAAGCCAATCTGGACGGATTTATCGGATTCTGATATTATTGATAGATTTGGTC
#> GGATATGTAGAAATCTTTCTCATTATTATAGTGGATCCTCAAAAAAACAGAGCTTATATCGAATAAGGTA
#> TATACTTCGACTTTCTTGTGCTAGAACTTTAGCTCGTAAACATAAAAGTACAGTACGTGCTTTTTTGCAA
#> AGATTAGGTTCGGAATTATTAGAAGAATTCTTTACAGAAGAAGAAGGAGTTGTTTTTTTGATTTCCCAAA
#> AGAACAAAACCTCTTTTCCTCTCTATAGGTCACATAGAGAACGCATTTGGTATTTGGATATTATCCATAT
#> TAATGAATTGGTGAATTCATTTATGATGGGGCGATAAGCCCCTATAAAATAAGAAATATAAATTTTTTCT
#> AATGTCTAATAAATAGACGACAAATTCATTAATTTTCATTCTGAAATGCTCATCTAGTAGTGTAGTGATT
#> GAATCAACTGAGTATTCAAAATTTTTAGACAAACTTCTAGGGATAGAAGTTTGTTTTATCTGTATACATA
#> GGTAAAGTCGTGTGCAATGAAAAATGCAAGCACGATTTGGGGAGAGATAATTTTCTCTATTGTAACAAAT
#> AAAAATTATCTACTCCATCCGACTAGTTAATCG
```

## 4. More information

For more information about `restez` see the other tutorials:

1.  [Build a database of all
    rodents](https://docs.ropensci.org/restez/articles/1_rodents.html)
2.  [How to search for and fetch
    sequences](https://docs.ropensci.org/restez/articles/2_search_and_fetch.html)
3.  [Advanced parsing of a GenBank
    record](https://docs.ropensci.org/restez/articles/3_parsing.html)
4.  [Running phylotaR with
    restez](https://docs.ropensci.org/restez/articles/4_phylotar.html)
5.  [Tips and
    tricks](https://docs.ropensci.org/restez/articles/5_tips_and_tricks.html)

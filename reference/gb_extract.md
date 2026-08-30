# Extract elements of a GenBank record

Return elements of GenBank record e.g. sequence, definition ...

## Usage

``` r
gb_extract(
  record,
  what = c("accession", "version", "organism", "sequence", "definition", "locus",
    "features", "keywords")
)
```

## Arguments

- record:

  GenBank record in text format, character

- what:

  Which element to extract

## Value

character or list of lists (what='features') or named character vector
(what='locus')

## Details

This function uses a REGEX to extract particular elements of a GenBank
record. All of the what options return a single character with the
exception of 'locus' or 'keywords' that return character vectors and
'features' that returns a list of lists for all features.

The accuracy of these functions cannot be guaranteed due to the enormity
of the GenBank database. But the function is regularly tested on a range
of GenBank records.

Note: all non-latin1 characters are converted to '-'.

## Examples

``` r
library(restez)
data('record')
(gb_extract(record = record, what = 'locus'))
#>     accession        length           mol          type        domain 
#>    "AY952423"        "2623"         "DNA"      "linear"         "PLN" 
#>          date 
#> "17-APR-2005" 
```

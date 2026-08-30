# Set restez path

Specify the filepath for the local GenBank database.

## Usage

``` r
restez_path_set(filepath)
```

## Arguments

- filepath:

  character, valid filepath to the folder where the database should be
  stored.

## Details

Adds 'restez_path' to options(). In this path the folder 'restez' will
be created and all downloaded and database files will be stored there.

## See also

Other setup:
[`restez_path_get()`](https://docs.ropensci.org/restez/reference/restez_path_get.md),
[`restez_path_unset()`](https://docs.ropensci.org/restez/reference/restez_path_unset.md),
[`restez_ready()`](https://docs.ropensci.org/restez/reference/restez_ready.md),
[`restez_status()`](https://docs.ropensci.org/restez/reference/restez_status.md)

## Examples

``` r
if (FALSE) { # \dontrun{
library(restez)
restez_path_set(filepath = 'path/to/where/you/want/files/to/download')
} # }
```

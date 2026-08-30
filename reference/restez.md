# restez: Create and Query a Local Copy of GenBank in R

The restez package comes with five families of functions: setup,
database, get, entrez and internal/private.

## Setup functions

These functions allow a user to set the filepath for where the GenBank
files should be stored, create connections and verify these settings.

## Database functions

These functions download specific parts of GenBank and create the local
SQL-like database.

## GenBank functions

These functions allow a user to query the local SQL-like database. A
user can use an NCBI accession ID to retrieve sequences or whole GenBank
records.

## Entrez functions

The entrez functions are wrappers to the `entrez_*` functions in the
rentrez package. e.g the restez's entrez_fetch will first try to search
the local database, if it fails it will then call rentrez's
[`rentrez::entrez_fetch()`](https://docs.ropensci.org/rentrez/reference/entrez_fetch.html)
with the same arguments.

## Private/internal functions

These functions work behind the scenes to make everything work. If
you're curious you can read their documentation using the form
`?restez:::functionname`.

## See also

Useful links:

- <https://github.com/ropensci/restez>

- <https://docs.ropensci.org/restez/>

- Report bugs at <https://github.com/ropensci/restez/issues>

## Author

**Maintainer**: Joel H. Nitta <joelnitta@gmail.com>
([ORCID](https://orcid.org/0000-0003-4719-7472))

Authors:

- Dom Bennett <dominic.john.bennett@gmail.com>
  ([ORCID](https://orcid.org/0000-0003-2722-1359))

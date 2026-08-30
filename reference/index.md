# Package index

## Set-up

Set and verify your restez path

- [`restez_path_set()`](https://docs.ropensci.org/restez/reference/restez_path_set.md)
  : Set restez path
- [`restez_path_get()`](https://docs.ropensci.org/restez/reference/restez_path_get.md)
  : Get restez path
- [`restez_path_unset()`](https://docs.ropensci.org/restez/reference/restez_path_unset.md)
  : Unset restez path
- [`restez_connect()`](https://docs.ropensci.org/restez/reference/restez_connect.md)
  : Connect to the restez database
- [`restez_disconnect()`](https://docs.ropensci.org/restez/reference/restez_disconnect.md)
  : Disconnect from restez database
- [`restez_status()`](https://docs.ropensci.org/restez/reference/restez_status.md)
  : Check restez status
- [`restez_ready()`](https://docs.ropensci.org/restez/reference/restez_ready.md)
  : Is restez ready?

## Database

Download, create, delete and verify your local database

- [`db_create()`](https://docs.ropensci.org/restez/reference/db_create.md)
  : Create new NCBI database
- [`db_delete()`](https://docs.ropensci.org/restez/reference/db_delete.md)
  : Delete database
- [`db_download()`](https://docs.ropensci.org/restez/reference/db_download.md)
  : Download database
- [`demo_db_create()`](https://docs.ropensci.org/restez/reference/demo_db_create.md)
  : Create demo database
- [`is_in_db()`](https://docs.ropensci.org/restez/reference/is_in_db.md)
  : Is in db
- [`list_db_ids()`](https://docs.ropensci.org/restez/reference/list_db_ids.md)
  : List database IDs
- [`count_db_ids()`](https://docs.ropensci.org/restez/reference/count_db_ids.md)
  : Return the number of ids
- [`ncbi_acc_get()`](https://docs.ropensci.org/restez/reference/ncbi_acc_get.md)
  : Get accession numbers by querying NCBI GenBank
- [`print(`*`<status>`*`)`](https://docs.ropensci.org/restez/reference/print.status.md)
  : Print method for status class

## GenBank

Retrieve data from the local GenBank database

- [`gb_definition_get()`](https://docs.ropensci.org/restez/reference/gb_definition_get.md)
  : Get definition from GenBank
- [`gb_fasta_get()`](https://docs.ropensci.org/restez/reference/gb_fasta_get.md)
  : Get fasta from GenBank
- [`gb_organism_get()`](https://docs.ropensci.org/restez/reference/gb_organism_get.md)
  : Get organism from GenBank
- [`gb_record_get()`](https://docs.ropensci.org/restez/reference/gb_record_get.md)
  : Get record from GenBank
- [`gb_sequence_get()`](https://docs.ropensci.org/restez/reference/gb_sequence_get.md)
  : Get sequence from GenBank
- [`gb_version_get()`](https://docs.ropensci.org/restez/reference/gb_version_get.md)
  : Get version from GenBank
- [`gb_extract()`](https://docs.ropensci.org/restez/reference/gb_extract.md)
  : Extract elements of a GenBank record

## Entrez wrappers

Wrappers for integration with the R package rentrez

- [`entrez_fetch()`](https://docs.ropensci.org/restez/reference/entrez_fetch.md)
  : Entrez fetch

## Data

Example data

- [`record`](https://docs.ropensci.org/restez/reference/record.md) :
  Example GenBank record

## Internal functions

Private internal functions, documented here for openness

- [`add_rcrd_log()`](https://docs.ropensci.org/restez/reference/add_rcrd_log.md)
  : Log files added to the SQL database in the restez path
- [`cat_line()`](https://docs.ropensci.org/restez/reference/cat_line.md)
  : Cat lines
- [`char()`](https://docs.ropensci.org/restez/reference/char.md) : Print
  green
- [`check_connection()`](https://docs.ropensci.org/restez/reference/check_connection.md)
  : Helper function to test if a stable internet connection can be
  established.
- [`cleanup()`](https://docs.ropensci.org/restez/reference/cleanup.md) :
  Clean up test data
- [`connected()`](https://docs.ropensci.org/restez/reference/connected.md)
  : Is restez connected?
- [`connection_get()`](https://docs.ropensci.org/restez/reference/connection_get.md)
  : Retrieve restez connection
- [`db_download_intern()`](https://docs.ropensci.org/restez/reference/db_download_intern.md)
  : Download database (internal version)
- [`db_sqlngths_get()`](https://docs.ropensci.org/restez/reference/db_sqlngths_get.md)
  : Return the minimum and maximum sequence lengths in db
- [`db_sqlngths_log()`](https://docs.ropensci.org/restez/reference/db_sqlngths_log.md)
  : Log the min and max sequence lengths
- [`dir_size()`](https://docs.ropensci.org/restez/reference/dir_size.md)
  : Calculate the size of a directory
- [`dwnld_path_get()`](https://docs.ropensci.org/restez/reference/dwnld_path_get.md)
  : Get dwnld path
- [`dwnld_rcrd_log()`](https://docs.ropensci.org/restez/reference/dwnld_rcrd_log.md)
  : Log a downloaded file in the restez path
- [`entrez_fasta_get()`](https://docs.ropensci.org/restez/reference/entrez_fasta_get.md)
  : Get Entrez fasta
- [`entrez_gb_get()`](https://docs.ropensci.org/restez/reference/entrez_gb_get.md)
  : Get Entrez GenBank record
- [`extract_accession()`](https://docs.ropensci.org/restez/reference/extract_accession.md)
  : Extract accession
- [`extract_by_patterns()`](https://docs.ropensci.org/restez/reference/extract_by_patterns.md)
  : Extract by keyword
- [`extract_clean_sequence()`](https://docs.ropensci.org/restez/reference/extract_clean_sequence.md)
  : Extract clean sequence from sequence part
- [`extract_definition()`](https://docs.ropensci.org/restez/reference/extract_definition.md)
  : Extract definition
- [`extract_features()`](https://docs.ropensci.org/restez/reference/extract_features.md)
  : Extract features
- [`extract_inforecpart()`](https://docs.ropensci.org/restez/reference/extract_inforecpart.md)
  : Extract the information record part
- [`extract_keywords()`](https://docs.ropensci.org/restez/reference/extract_keywords.md)
  : Extract keywords
- [`extract_locus()`](https://docs.ropensci.org/restez/reference/extract_locus.md)
  : Extract locus
- [`extract_organism()`](https://docs.ropensci.org/restez/reference/extract_organism.md)
  : Extract organism
- [`extract_seqrecpart()`](https://docs.ropensci.org/restez/reference/extract_seqrecpart.md)
  : Extract the sequence record part
- [`extract_sequence()`](https://docs.ropensci.org/restez/reference/extract_sequence.md)
  : Extract sequence
- [`extract_version()`](https://docs.ropensci.org/restez/reference/extract_version.md)
  : Extract version
- [`file_download()`](https://docs.ropensci.org/restez/reference/file_download.md)
  : Download a file
- [`filename_log()`](https://docs.ropensci.org/restez/reference/filename_log.md)
  : Write filenames to log files
- [`flatfile_read()`](https://docs.ropensci.org/restez/reference/flatfile_read.md)
  : Read flatfile sequence records
- [`gb_build()`](https://docs.ropensci.org/restez/reference/gb_build.md)
  : Read and add .seq files to database
- [`gb_df_create()`](https://docs.ropensci.org/restez/reference/gb_df_create.md)
  : Create GenBank data.frame
- [`gb_df_generate()`](https://docs.ropensci.org/restez/reference/gb_df_generate.md)
  : Generate GenBank records data.frame
- [`gb_sql_add()`](https://docs.ropensci.org/restez/reference/gb_sql_add.md)
  : Add to GenBank SQL database
- [`gb_sql_query()`](https://docs.ropensci.org/restez/reference/gb_sql_query.md)
  : Query the GenBank SQL
- [`gbrelease_check()`](https://docs.ropensci.org/restez/reference/gbrelease_check.md)
  : Check if the last GenBank release number is the latest
- [`gbrelease_get()`](https://docs.ropensci.org/restez/reference/gbrelease_get.md)
  : Get the GenBank release number in the restez path
- [`gbrelease_log()`](https://docs.ropensci.org/restez/reference/gbrelease_log.md)
  : Log the GenBank release number in the restez path
- [`has_data()`](https://docs.ropensci.org/restez/reference/has_data.md)
  : Does the connected database have data?
- [`identify_downloadable_files()`](https://docs.ropensci.org/restez/reference/identify_downloadable_files.md)
  : Identify downloadable files
- [`last_add_get()`](https://docs.ropensci.org/restez/reference/last_add_get.md)
  : Return date and time of the last added sequence
- [`last_dwnld_get()`](https://docs.ropensci.org/restez/reference/last_dwnld_get.md)
  : Return date and time of the last download
- [`last_entry_get()`](https://docs.ropensci.org/restez/reference/last_entry_get.md)
  : Return the last entry
- [`latest_genbank_release()`](https://docs.ropensci.org/restez/reference/latest_genbank_release.md)
  : Retrieve latest GenBank release number
- [`latest_genbank_release_notes()`](https://docs.ropensci.org/restez/reference/latest_genbank_release_notes.md)
  : Download the latest GenBank Release Notes
- [`message_missing()`](https://docs.ropensci.org/restez/reference/message_missing.md)
  : Produce message of missing IDs
- [`mock_def()`](https://docs.ropensci.org/restez/reference/mock_def.md)
  : Mock def
- [`mock_gb_df_generate()`](https://docs.ropensci.org/restez/reference/mock_gb_df_generate.md)
  : Generate mock GenBank records data.frame
- [`mock_org()`](https://docs.ropensci.org/restez/reference/mock_org.md)
  : Mock org
- [`mock_rec()`](https://docs.ropensci.org/restez/reference/mock_rec.md)
  : Mock rec
- [`mock_seq()`](https://docs.ropensci.org/restez/reference/mock_seq.md)
  : Mock seq
- [`predict_datasizes()`](https://docs.ropensci.org/restez/reference/predict_datasizes.md)
  : Print file size predictions to screen
- [`readme_log()`](https://docs.ropensci.org/restez/reference/readme_log.md)
  : Create README in restez_path
- [`restez_path_check()`](https://docs.ropensci.org/restez/reference/restez_path_check.md)
  : Check restez filepath
- [`restez_rl()`](https://docs.ropensci.org/restez/reference/restez_rl.md)
  : Restez readline
- [`search_gz()`](https://docs.ropensci.org/restez/reference/search_gz.md)
  : Scan a gzipped file for text
- [`seshinfo_log()`](https://docs.ropensci.org/restez/reference/seshinfo_log.md)
  : Log the system session information in restez path
- [`setup()`](https://docs.ropensci.org/restez/reference/setup.md) : Set
  up test common test data
- [`slctn_get()`](https://docs.ropensci.org/restez/reference/slctn_get.md)
  : Retrieve GenBank selections made by user
- [`slctn_log()`](https://docs.ropensci.org/restez/reference/slctn_log.md)
  : Log the GenBank selection made by a user
- [`sql_path_get()`](https://docs.ropensci.org/restez/reference/sql_path_get.md)
  : Get SQL path
- [`stat()`](https://docs.ropensci.org/restez/reference/stat.md) : Print
  blue
- [`status_class()`](https://docs.ropensci.org/restez/reference/status_class.md)
  : Generate a list class for storing status information
- [`testdatadir_get()`](https://docs.ropensci.org/restez/reference/testdatadir_get.md)
  : Get test data directory

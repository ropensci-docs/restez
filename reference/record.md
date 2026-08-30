# Example GenBank record

Example GenBank record in text format for demonstration purposes.

## Usage

``` r
data("record")
```

## Format

A large character object containing record information and DNA sequence.

## Source

<https://www.ncbi.nlm.nih.gov/nuccore/AY952423.1>

## References

GenBank

## Examples

``` r
data(record)
cat(record)
#> LOCUS       AY952423                2623 bp    DNA     linear   PLN 17-APR-2005
#> DEFINITION  Livistona chinensis tRNA-Lys (trnK) gene, partial sequence; and
#>             matK gene, complete sequence; chloroplast.
#> ACCESSION   AY952423
#> VERSION     AY952423.1
#> KEYWORDS    .
#> SOURCE      chloroplast Livistona chinensis
#>   ORGANISM  Livistona chinensis
#>             Eukaryota; Viridiplantae; Streptophyta; Embryophyta; Tracheophyta;
#>             Spermatophyta; Magnoliophyta; Liliopsida; Arecaceae; Coryphoideae;
#>             Livistoneae; Livistoninae; Livistona.
#> REFERENCE   1  (bases 1 to 2623)
#>   AUTHORS   Li,X.X. and Zhou,Z.K.
#>   TITLE     Monocotyledons phylogeny based on three genes (matK, rbcL and 18S
#>             rDNA) sequences
#>   JOURNAL   Unpublished
#> REFERENCE   2  (bases 1 to 2623)
#>   AUTHORS   Li,X.X. and Zhou,Z.K.
#>   TITLE     Direct Submission
#>   JOURNAL   Submitted (03-MAR-2005) Taxonomical and Ethnobotanical Department,
#>             Kunming Institute of Botany, The Chinese Academy of Sciences,
#>             Heilongtan, Kunming, Yunnan 650204, China
#> FEATURES             Location/Qualifiers
#>      source          1..2623
#>                      /organism="Livistona chinensis"
#>                      /organelle="plastid:chloroplast"
#>                      /mol_type="genomic DNA"
#>                      /db_xref="taxon:115492"
#>      gene            <1..>2623
#>                      /gene="trnK"
#>                      /note="tRNA-Lys"
#>      intron          <1..>2623
#>                      /gene="trnK"
#>      gene            813..2347
#>                      /gene="matK"
#>      misc_feature    813..2347
#>                      /gene="matK"
#>                      /note="similar to maturase K"
#> ORIGIN      
#>         1 attggggttg ctaactcaac ggtagagtac tcggctttta agtgcgacta tcatctttta
#>        61 cacatttgga tgaagtaagg aattcgtcca gactattggt agagtctata agaccacgac
#>       121 tgatcctgaa aggtaatgaa tggaaaaaat agcatgtcgt acgtaataca atgagaaact
#>       181 tgtaatttct tattgtaatt ttttaagtag aactttgagt ttatccttac tggatcatta
#>       241 caaaaatatt gtattttatt tttggaaggg gacgaaaaaa aggaaattcc caacatttat
#>       301 tgtttggtct aatgaataaa tggatagggg cctagggtag ggcccaattt ttgtaaaaca
#>       361 aaaagcaacg agcttatgtt cttaatttga ataattaccc gatctaatta gatgttaaaa
#>       421 ataaattagt gccagatgtg gtaaagggtt ctactgtaag tggacctttt tttttttttt
#>       481 ttatgaatcc tacctattat ctattatgga ttaaagatgg atgtgtataa gaagaagtat
#>       541 actgataaag agaatttttc caaagtcaaa agagcaatcg ggttgcaaaa ataaaggatt
#>       601 tttacctccg agaattataa attaattgga tcaaaaggag aggaaaaagt ctgtgattgg
#>       661 actccttcta tccgcgggta tgggtatata gtaggtatat atgtatattt gtatactata
#>       721 taaattacat gccctgttct gaccgtattg cactatgtat tatttgataa tccaagaaat
#>       781 gcctcctact tctggttcaa gtagaaatga aaatagaaga attacaagaa tatttagaaa
#>       841 aagatagatc tcggcaacaa cacttcctat acccactttt ctttcaggag tatatttatg
#>       901 cacttgctca tgattatggg tttaaagggt tcgatttttt acgaacctat ggaaattggg
#>       961 ggttatgata ataaatctag ttcagtactt gtaaaacatt taattactcg aatgtatcaa
#>      1021 cagaattatt tgatttattc tgttaatgaa tctaaccaaa atcgattgat tgagcataac
#>      1081 aattcttttt attctcaaat gatatctgaa gtttttgcga tcattgcaga aattccattc
#>      1141 tctcagcaat tactattttc tcttcgagga aaaaagaata ccaaaatctc agactttacg
#>      1201 atctattcat tcaatatttc cctttttaga agacaaatta tcacatttaa actatgtgtc
#>      1261 agatatatta ataccctatc ccatccattt ggaaatcttg gtgcaaattc ttcaatgctg
#>      1321 gatccaagat gtttcttctt tgcatttatt gcgattcttt ctccacgaac atcataatgg
#>      1381 gaatagtttt ttttttccaa agaaatcctt ttcaaaagaa aataaaagac tctttcgatt
#>      1441 cctatataat tcttatgtat ctgaatgtga atttgtctta gtgtttcttc gtaaacaatc
#>      1501 ctcttattta caatcaaaat cctatggaat ctttcttgag cgaacacatt tctatggaag
#>      1561 aatggaacat cttatagtag tgtgtcataa ttattgtcag aaggcctttt gggtcttcaa
#>      1621 ggatcctttt atgcattatg ttcgatatca aggaaaagca attctggcat caaaaggatc
#>      1681 ttatcttttg atgaagaaat ggagatgtca tcttgtcaat ttctggcaat attattttca
#>      1741 tttttgggct cagccttaca gaatttcaat aaaccaatta ggaaatcatt ccttctattt
#>      1801 tctcggttat ctttcaagtg tattaaaaaa tacttcgtct gtaaggaatc aaatgctaga
#>      1861 gaattccttt ttaatagata ctattactaa taaattggat accatagtcc cagttcttcc
#>      1921 tcttattgga tctttgtcta aagctaaatt ttgtaccgta tccgggcatc ctagtagtaa
#>      1981 gccaatctgg acggatttat cggattctga tattattgat agatttggtc ggatatgtag
#>      2041 aaatctttct cattattata gtggatcctc aaaaaaacag agcttatatc gaataaggta
#>      2101 tatacttcga ctttcttgtg ctagaacttt agctcgtaaa cataaaagta cagtacgtgc
#>      2161 ttttttgcaa agattaggtt cggaattatt agaagaattc tttacagaag aagaaggagt
#>      2221 tgtttttttg atttcccaaa agaacaaaac ctcttttcct ctctataggt cacatagaga
#>      2281 acgcatttgg tatttggata ttatccatat taatgaattg gtgaattcat ttatgatggg
#>      2341 gcgataagcc cctataaaat aagaaatata aattttttct aatgtctaat aaatagacga
#>      2401 caaattcatt aattttcatt ctgaaatgct catctagtag tgtagtgatt gaatcaactg
#>      2461 agtattcaaa atttttagac aaacttctag ggatagaagt ttgttttatc tgtatacata
#>      2521 ggtaaagtcg tgtgcaatga aaaatgcaag cacgatttgg ggagagataa ttttctctat
#>      2581 tgtaacaaat aaaaattatc tactccatcc gactagttaa tcg
#> //
#> 
```

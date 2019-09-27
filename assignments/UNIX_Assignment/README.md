#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```
$ wc fang_et_al_genotypes.txt
$ tail -n +2 fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'
$ head -n 1 fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'
$ tail -n +2 fang_et_al_genotypes.txt | wc
$ tail -n +2 fang_et_al_genotypes.txt | du -h
```

By inspecting this file I learned that:

1. The file has 986 columns and 2783 lines
2. The header has the same number of columns as the rest of the data
3. There are about 11 million bytes of data


###Attributes of `snp_position.txt`

```
$ wc snp_position.txt
$ tail -n +2 snp_position.txt | awk -F "\t" '{print NF; exit}'
$ ls -lh snp_position.txt
$ du -h snp_position.txt
```

By inspecting this file I learned that:

1. There are 384 lines in the file
2. There are 15 columns in the file
3. There are about 84 thousand bytes in the file


##Data Processing

###Maize Data

```
$ head -n 1 fang_et_al_genotypes.txt > maize.txt
$ grep "ZMMIL\|ZMMLR\|ZMMMR" fang_et_al_genotypes.txt >> maize.txt
```
Creates maize-only file with header

```
$ awk -f transpose.awk maize.txt > transposed_maize_genotypes.txt
$ sort -k1 transposed_maize_genotypes.txt > sorted_transposed_maize.txt
$ sort -k1 snp_position.txt > sorted_snp_position.txt
$ join -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_maize.txt > joined_maize.txt
```
Transposes maize-only file, sorts transposed maize file and SNP file, and joins them by their first columns

```
$ awk '{if ($3=="1") print $0}' joined_maize.txt > maize_1.txt
$ awk '{if ($3=="2") print $0}' joined_maize.txt > maize_2.txt
$ awk '{if ($3=="3") print $0}' joined_maize.txt > maize_3.txt
$ awk '{if ($3=="4") print $0}' joined_maize.txt > maize_4.txt
$ awk '{if ($3=="5") print $0}' joined_maize.txt > maize_5.txt
$ awk '{if ($3=="6") print $0}' joined_maize.txt > maize_6.txt
$ awk '{if ($3=="7") print $0}' joined_maize.txt > maize_7.txt
$ awk '{if ($3=="8") print $0}' joined_maize.txt > maize_8.txt
$ awk '{if ($3=="9") print $0}' joined_maize.txt > maize_9.txt
$ awk '{if ($3=="10") print $0}' joined_maize.txt > maize_10.txt
```
Separates joined files by chromosome number and creates new files for each chromosome

```
$ sort -k4 maize_1.txt > maize_inc_1.txt
$ sort -k4 maize_2.txt > maize_inc_2.txt
$ sort -k4 maize_3.txt > maize_inc_3.txt
$ sort -k4 maize_4.txt > maize_inc_4.txt
$ sort -k4 maize_5.txt > maize_inc_5.txt
$ sort -k4 maize_6.txt > maize_inc_6.txt
$ sort -k4 maize_7.txt > maize_inc_7.txt
$ sort -k4 maize_8.txt > maize_inc_8.txt
$ sort -k4 maize_9.txt > maize_inc_9.txt
$ sort -k4 maize_10.txt > maize_inc_10.txt
```
Sorts each chromosome file by position and creates a new file. Unknown data is already denoted as "?" by default. 

```
$ sort -k4 -r maize_1.txt | sed 's/?/-/g' > maize_dec_1.txt
$ sort -k4 -r maize_2.txt | sed 's/?/-/g' > maize_dec_2.txt
$ sort -k4 -r maize_3.txt | sed 's/?/-/g' > maize_dec_3.txt
and so on...
```
Sorts each chromosome file in reverse order and creates a new file. Unknown data is replaced by "-". 

```
$ awk '{if ($4=="unknown") print $0}' joined_maize.txt > maize_unknown.txt
$ awk '{if ($4=="multiple") print $0}' joined_maize.txt > maize_multiple.txt
```
This creates new files for SNPs with unknown or multiple positions

```
$ mkdir maize_final
$ mv maize_inc*.txt maize_final
$ mv maize_dec*.txt maize_final
$ mv maize_multiple.txt maize_final
$ mv maize_unknown.txt maize_final
```
Creates a new directory for final files and moves those files into the directory.


###Teosinte Data

```
$ head -n 1 fang_et_al_genotypes.txt > teosinte.txt
$ grep "ZMPBA\|ZMPIL\|ZMPJA" fang_et_al_genotypes.txt >> teosinte.txt
```
Creates teosinte-only file with header

```
$ awk -f transpose.awk teosinte.txt > transposed_teosinte_genotypes.txt
$ sort -k1 transposed_teosinte_genotypes.txt > sorted_transposed_teosinte.txt
$ join -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_teosinte.txt > joined_teosinte.txt
```
Transposes teosinte-only file, sorts transposed maize file and SNP file, and joins them by their first columns.

```
$ awk '{if ($3=="1") print $0}' joined_teosinte.txt > teosinte_1.txt
$ awk '{if ($3=="2") print $0}' joined_teosinte.txt > teosinte_2.txt
$ awk '{if ($3=="3") print $0}' joined_teosinte.txt > teosinte_3.txt
and so on...

```
Separates joined files by chromosome number and creates new files for each chromosome

```
$ awk '{if ($4=="multiple") print $0}' joined_teosinte.txt > teosinte_multiple.txt
$ awk '{if ($4=="unknown") print $0}' joined_teosinte.txt > teosinte_unknown.txt
```
This creates new files for SNPs with unknown or multiple positions.

```
$ sort -k4 teosinte_1.txt > teosinte_inc_1.txt
$ sort -k4 teosinte_2.txt > teosinte_inc_2.txt
$ sort -k4 teosinte_3.txt > teosinte_inc_3.txt
and so on...
```
Sorts each chromosome file by position and creates a new file. Unknown data is already denoted as "?" by default.

```
$ sort -k4 -r teosinte_1.txt | sed 's/?/-/g' > teosinte_dec_1.txt
$ sort -k4 -r teosinte_2.txt | sed 's/?/-/g' > teosinte_dec_2.txt
$ sort -k4 -r teosinte_3.txt | sed 's/?/-/g' > teosinte_dec_3.txt
and so on...
```
Sorts each chromosome file in reverse order and creates a new file. Unknown data is replaced by "-".

```
$ mkdir teosinte_final
$ mv teosinte_inc*.txt teosinte_final
$ mv teosinte_dec*.txt teosinte_final
$ mv teosinte_multiple.txt teosinte_final
$ mv teosinte_unknown.txt teosinte_final
```
Creates a new directory for final files and moves those files into the directory.


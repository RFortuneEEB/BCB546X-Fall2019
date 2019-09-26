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
here is my snippet of code used for data processing
```

Here is my brief description of what this code does


###Teosinte Data

```
here is my snippet of code used for data processing
```

# Tutorial: Name

Description

# Introduction

As sequencing methods become more inexpensive, producing genomic and metagenomic data becomes more available for large-scale analyses. Therefore, the development of quick and accuarate computational approaches become essential. Here, we introduce one such program, sourmash, which enables the minimization of sequencing data, similarity comparisons, species identification, among other tasks.

**What do we mean by minimization?** Utilizing sourmash, we can sketch a simpler representation of the original genomic or metagenomic datasets using the FracMinHash approach. 

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture3.png)

Simply put it, a minimized set of k-mers (a subset of a string of length k) is produced from a fasta file with sequences of interest. The threshold to which the set is minimized is indicated by a scale factor, a parameter used to reduce the original set. Note that if a scale factor of 1 is utilized, the final FracMinHash sketch will be the original set of k-mers and as this number increases, the more the original set of k-mers will decrease for the final FracMinHash sketch. Each k-mer in the original set is passed through a Hash function, k-mers that minimize this function by having a value that is equal or less to the scale factor are used in the final FracMinHash sketch, FRAC(A) for example. 

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture6.png)

# Preprocessing data utilizing sourmash sketch

To start our sourmash tutorial, we will sketch our fasta file of interest. This fasta file contains XYZ. 

`sourmash sketch dna filename k=33,scaled=500`

|Parameter      |Description|
|---------------|----------|
|sourmash sketch| The command that sourmash utilizes to produce a sketch. |
|dna            | Identify that the sequences in our X file are DNA. If a different sequence type is used, like protein sequences, then this would be indicated as **protein** instead.|
|filename       | Filename of interest. Please note that sourmash can produce sketches from either FASTA or FASTQ fules.|
|k=33           | Tunable parameter required by the user to set. Check how the ksize can affect further analyses here: (CITE). |
|scaled=500     | Our scale factor, which is also tunable.|

# Estimating similarity with sourmash compare

Minhash, Jaccard

Containment

picture

`sourmash compare <ref signature> <query signature> --containment --ksize <ksize>`

ANI


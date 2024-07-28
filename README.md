# Introduction

As sequencing methods become more inexpensive, producing genomic and metagenomic data becomes more available for large-scale analyses. Therefore, the development of quick and accuarate computational approaches become essential. Here, we introduce one such program, sourmash, which enables the minimization of sequencing data, similarity comparisons, enables species identification, among other tasks.

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture4.png)

## What do we mean by minimization?

If you're from Penn State, like we are, you would know who this. The minization of our mascot by sketching the photo could still be identified as the Nittany Lion.

## We can do the same using sequencing data!
![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture3.png)

Utilizing sourmash, we can sketch a simpler version of larger genomic datasets such as metagenomic data. 

# Preprocessing data utilizing sourmash sketch

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture1.png)

`sourmash sketch <dna, protein> <FASTA/FASTQ> k=<ksize>,scaled=<scale factor>`

|Parameter|Description|
|-|-|
|< dna, protein >| Identify whether the sequence input is DNA or protein. |
|< FASTA/FASTQ >| The filename that will be sketched. |
|< ksize >| The user is required to identify the ksize. |
|< scale factor >| The number to which our data will be scaled.|

**Keep in mind:**
+ The **ksize** is a subset of length k for a sequence.
+ The **scale factor** is XYZ. For example, a scale factor =1 results in using all k-mers.





# Estimating similarity with sourmash compare

Minhash, Jaccard

Containment

picture

`sourmash compare <ref signature> <query signature> --containment --ksize <ksize>`

ANI

# Tutorial

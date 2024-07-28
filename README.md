# Introduction

As sequencing methods become more inexpensive, producing genomic and metagenomic data becomes more available for large-scale analyses. Therefore, the development of quick and accuarate computational approaches become essential. Here, we introduce one such program, sourmash, which enables the minimization of sequencing data, similarity comparisons, enables species identification, among other tasks.

## What do we mean by minimization?

If you're from Penn State, like we are, you would know who this.

picture

What would minization look like for our mascot?

picture

If we reduce the resolution of this photo, we can still identify that this is the Nittany Lion.

**We can do the same using sequencing data!**
![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture3.png)

# Preprocessing data utilizing sourmash sketch

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/Picture1.png)

`sourmash sketch <dna, protein, translate> <FASTA/FASTQ> k=<ksize>,scaled=<int>`

# Estimating similarity with sourmash compare

Minhash, Jaccard

Containment

picture

`sourmash compare <ref signature> <query signature> --containment --ksize <ksize>`

ANI

# Tutorial

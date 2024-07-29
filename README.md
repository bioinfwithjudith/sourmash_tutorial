# Tutorial: Name

Description

# Introduction

As sequencing methods become more inexpensive, producing genomic and metagenomic data becomes more available for large-scale analyses. Therefore, the development of quick and accuarate computational approaches become essential. Here, we introduce one such program, sourmash, which enables the minimization of sequencing data, similarity comparisons, species identification, among other tasks.

**What do we mean by minimization?** Utilizing sourmash, we can sketch a simpler representation of the original genomic or metagenomic datasets using the FracMinHash approach. 

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/src/Picture3.png)

Simply put it, a minimized set of k-mers (a subset of a string of length k) is produced from a fasta file with sequences of interest. The threshold to which the set is minimized is indicated by a scale factor, a parameter used to reduce the original set. Note that if a scale factor of 1 is utilized, the final FracMinHash sketch will be the original set of k-mers and as this number increases, the more the original set of k-mers will decrease for the final FracMinHash sketch. Each k-mer in the original set is passed through a Hash function, k-mers that minimize this function by having a value that is equal or less to the scale factor are used in the final FracMinHash sketch, FRAC(A) for example. 

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/src/Picture6.png)

**Comparing two FracMinHash sketches is possible.** 

Minhash, Jaccard, ANI, Containment

Comparison facilitates further analyses such as dN/dS estimates. Check out fmh_dnds.

![alt text](https://github.com/bioinfwithjudith/sourmash_tutorial/blob/main/src/Picture7.png)


# Preprocessing data utilizing sourmash sketch

To start our sourmash tutorial, we will sketch our fasta file of interest: **sample_001.fna**. This file does not contain any meaningfull information but is just a play dataset for tutorial purposes. 

`sourmash sketch dna datasets/sample_001.fna -p k=31,scaled=500`

|Parameter      |Description|
|---------------|----------|
|sourmash sketch| The command that sourmash utilizes to produce a sketch. |
|dna            | Identify that the sequences in our X file are DNA. If a different sequence type is used, like protein sequences, then this would be indicated as **protein** instead.|
|sample_001.fna       | Filename of interest. Please note that sourmash can produce sketches from either FASTA or FASTQ fules.|
|-p           | Flag to indicate a list of parameters. |
|k=33           | Tunable parameter required by the user to set. Check how the ksize can affect further analyses here: (CITE). |
|scaled=500     | Our scale factor, which is also tunable.|

Utilizing sourmash sketch, we have produced the following  file, known as a signature file: **sample_001.fna.sig**. 

Let's be a bit anosey and see what this file contains:

`sourmash sig describe sample_001.fna.sig`

Below is the information you should see displayed on your end. Information such as the signature filename, sequence type, ksize and scale factor used are report. Additional information, such as total number of signatures and hashes are also shown, alongside other information.

```
== This is sourmash version 4.8.6. ==
== Please cite Brown and Irber (2016), doi:10.21105/joss.00027. ==

** loading from 'sample_001.fna.sig'
path filetype: MultiIndex
location: sample_001.fna.sig
is database? no
has manifest? yes
num signatures: 1
** examining manifest...
total hashes: 21
summary of sketches:
   1 sketches with DNA, k=31, scaled=1000             21 total hashes
```

# Comparing two sketches with sourmash compare

Now that we feel a bit more comfortable with a sketching fasta file. Let's sketch a another file to compare it to the previous signature file we produced.

`sourmash sketch dna datasets/sample_002.fna -p k=31,scaled=500`

Notice, that we are using the same ksize and scale factor, sourmash requires that two signatures have parameters tuned in the same way for comparison. 

`sourmash compare sample_001.fna.sig sample_002.fna.sig --containment`

```
== This is sourmash version 4.8.6. ==
== Please cite Brown and Irber (2016), doi:10.21105/joss.00027. ==

loaded 2 signatures total.
NOTE: downsampling to scaled value of 1000

0-sample_001.fna        [1.    0.696]
1-sample_002.fna        [0.762 1.   ]
min similarity in matrix: 0.696
WARNING: size estimation for at least one of these sketches may be inaccurate. ANI values will be set to 1 for these comparisons.
```

These results can be reported to a csv file for further analyses.

` sourmash compare sample_001.fna.sig sample_002.fna.sig --containment --csv compare.csv`

|Parameter      |Description|
|---------------|----------|
|sourmash compare| The command that sourmash utilizes to compare two signatures. |
|sample_001.fna.sig       | signature filename 1. |
|sample_002.fna.sig       | signature filename 2. |
|--containment           | Flag to indicate we are using the similarity index containment. Other similarity indexes that can be used are **--jaccard** or **--ani** |
|--csv           | Flag to indicate we want to produce a CSV file to report a matrix with similarity indexes |

Looking at our newly produced csv file, we would expect a similarity matrix:

```
sample_001.fna,sample_002.fna
1.0,0.6956521739836137
0.7619047624764425,1.0
```

**Comparing individual sequences between sigantures.** As you may have noticed, the comparisons reported are between two fasta files as a whole. However, you might be interested in comparing the sequences individually than the sequences as a whole. To accomplish this, we revisit `sourmash sketch`. 

Your sourmash sketch command will be modified by adding the **--singleton** flag, this will produce a signature file where each sequence is sketched individually.

`sourmash sketch dna datasets/sample_001.fna --singleton -p k=31,scaled=500 -o sample_001.fna.singleton.sig`

Compare the description between the first signature file we produced without the `--singleton` flag, **sample_001.fna.sig** and **sample_001.fna.singleton.sig**.

`sourmash sig fileinfo sample_001.fna.singleton.sig`

Instead of having just one sketch representing the fasta file as a whole, the `--singleton` flag produces a signature file with 10 sketches representing the 10 sequences within our fasta file of interest. 

```

== This is sourmash version 4.8.6. ==
== Please cite Brown and Irber (2016), doi:10.21105/joss.00027. ==

** loading from 'test.sig'
path filetype: MultiIndex
location: sample_001.fna.singleton.sig
is database? no
has manifest? yes
num signatures: 10
** examining manifest...
total hashes: 210
summary of sketches:
   10 sketches with DNA, k=31, scaled=500             210 total hashes
```

We can run the same command for coomparing two signature files, and the csv file produced will ccontain the matrix for individual sequences.

`sourmash compare sample_001.fna.singleton.sig sample_002.fna.singleton.sig --containment --csv compare.singleton.sig.csv`



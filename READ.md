# Sourmash tutorialD

In this tutorial, we will XYZ.

## Data

Reference: combination of ecoli_GCF_000008865.2, scerevisiae_GCF_000146045.2, sjaponicus_GCF_000149845.2, sparadoxus_GCF_002079055.1, spombe_GCF_000002945.1

Samples: sample1.fna (ecoli) is present and sample2.fna (smikatae) is not present in reference

## Preprocess FASTA and FASTQ files before using sourmash

Before getting started with analyzing your metagenomic data, preprocess your files by converting them into a minhash or fracminhash sketch. Minhash and Fracminhash sketches are hash sketches that create sketches using minimizers (minhash sketch) or a scale factor (i.e frac minhash sketch). Produce your sketches by using the sourmash sketch command. Depending on the type of sequences (i.e. DNA or protein sequneces) that you are using you are requireed to identify these. Your sourmash sketch command will take in a ksize and a scaled factor, where the kmers of your sequences will be obtained and will be scaled down to your sketch.

### sourmash sketch

#### sourmash sketch dna

Let's create a fracminhash sketch for my reference and query fasta files that uses a ksize of 30 and uses 1 out of 10 kmers. Note that as the scaled factor decreases, the more kmers are selected from the set of kmers for the desired sketch.


Sketch reference file

```
sourmash sketch dna ../data/reference.fna -p k=30,scaled=1
```

Sketch the following query files

```
sourmash sketch dna ../data/samples/sample1.fna -p k=30,scaled=10 
sourmash sketch dna ../data/samples/sample2.fna -p k=30,scaled=10
```

#### sourmash sketch protein

If you are dealing with protein sqquences, just change sourmash dna to sourmash protein. The ksize and scaled factor options are used similariily but consider that protein sequences are a third of protein coding sequences and reducing your ksize should be considered.

```
sourmash sketch protein ../data/samples/sample1.fna -p k=30,scaled=1 
```

### options

The additional options that sourmash provides to create your sketches is important and can influence downstream sourmash results.

#### using --singleton flag

When the --singleton flag is used, this will produce a sketch for each record in your file. This flag is useful if you want a to search through each record or compare between each record. 

```
sourmash sketch dna ../data/samples/sample1.fna -p k=30,scaled=1 --singleton
```

#### other options

Create a text file with a list of fasta files and identify it via the --from-file flag in your sourmash sketch command.

Merging signatures is possible by using the --merge flag and is a good option to XYZ.

### output






Commands:


Check signature fileinfo

sourmash signature fileinfo reference.fna.sig
sourmash signature fileinfo sample1.fna.sig
sourmash signature fileinfo sample2.fna.sig

Compare signatures

sourmash compare signatures/reference.fna.sig signatures/sample1.fna.sig --ksize 30 --output results/sample1/jaccard.mat --csv results/sample1/jaccard.csv
sourmash compare signatures/reference.fna.sig signatures/sample1.fna.sig --containment --ksize 30 --output results/sample1/containment.mat --csv results/sample1/containment.csv
sourmash compare signatures/reference.fna.sig signatures/sample1.fna.sig --ani --ksize 30 --output results/sample1/ani.mat --csv results/sample1/ani.csv


sourmash compare signatures/reference.fna.sig signatures/sample2.fna.sig --ksize 30 --output results/sample2/jaccard.mat --csv results/sample2/jaccard.csv
sourmash compare signatures/reference.fna.sig signatures/sample2.fna.sig --containment --ksize 30 --output results/sample2/containment.mat --csv results/sample2/containment.csv
sourmash compare signatures/reference.fna.sig signatures/sample2.fna.sig --ani --ksize 30 --output results/sample2/ani.mat --csv results/sample2/ani.csv

Plot coparisons

sourmash plot ../../results/sample1/jaccard.mat
sourmash plot ../../results/sample1/ani.mat
sourmash plot ../../results/sample1/containment.mat

sourmash plot ../../results/sample2/jaccard.mat
sourmash plot ../../results/sample2/ani.mat
sourmash plot ../../results/sample2/containment.mat


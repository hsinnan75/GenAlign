GSAlign: an ultra-fast genome sequence alignment tool
===================

Developers: Dr. Hsin-Nan Lin and Dr. Wen-Lian Hsu Institute of Information Science, Academia Sinica, Taiwan.

# Introduction

Personal genomics and comparative genomics are two fields that are more and more important in clinical practices and genome researches. Both fields require sequence alignment to discover sequence conservation and structural variation. Though many methods have been developed to handle genome sequence alignment, some are designed for small genome comparison while some are not efficient for large genome comparison. Here, we present GSAlign to handle large genome comparison efficiently. GSAlign includes three unique features: 1) it is the first attempt to use Burrows-Wheeler Transform on genome sequence alignment; 2) it supports parallel computing; 3) it adopts a divide-and-conquer strategy to separate a query sequence into regions that are easy to align and regions that require gapped alignment. With all these features, we demonstrated GSAlign is very efficient and sensitive in finding both the exact matches and differences between two genome sequences and it is much faster than existing state-of-the-art methods. 

# Download

Current version: 0.9.2 Please use the command 
  ```
  $ git clone https://github.com/hsinnan75/GSAlign.git
  ```
to download the package of Kart.

# Compiling

To compile GSAlign and the index tool, please change to GSAlign's folder and just type 'make' to compile GSAlign and bwt_index. If the compilation or the programs fail, please contact me (arith@iis.sinica.edu.tw), Thanks.

# Changes
version 0.9.2: Fixed a bug in removing overlaps between seed pairs, and fixed a bug in reporting alignment coordinates.

version 0.9.1: Added MAF output.

version 0.9.0: First release version.

# Instructions

To index a reference genome, GSAlign requires the target genome file (in fasta format) and the prefix of the index files (including the directory path).

  ```
  $ ./bwt_index ref_file[ex.ecoli.fa] index_prefix[ex. Ecoli]
  ```
The above command is to index the genome file Ecoli.fa and store the index files begining with ecoli.
If the index files are not mdade beforehand, GSAlign will generate index files istself with the given reference genome sequences.

To align two genome sequences, GSAlign requires two genome files (in fasta format)

  ```
  $ ./GSAlign -r fa1 -q fa2 -o output
  ```
or with a pre-built index file

  ```
  $ ./GSAlign -i idx_prefix -q fa2 -o output
  ```

# Datasets

You may download the test datasets at http://bioapp.iis.sinica.edu.tw/~arith/GSAlign/ to test the performance of GSAlign.
You can also use the evaulation tool (Evaluation.cpp) to measure the precision and recall of the resulting VCF files. 
To compile Evaluation.cpp, just type 'g++ Evaluation.cpp -o eva'

# File formats

- Reference and query genome files

    Both the reference genome and query genome files should be in FASTA format.

- Output file

	1. maf file: it shows the pairwise alignments between the two genomes (standard MAF format).
	2. vcf file: it shows the sequence variants between the two genomes (standard VCF format).
	3. ps  file: it shows the dotplot between two chromosomes (gnuplot is required).
	4. snp file: it shows all the SNPs of the query genome (compared to the reference genome).
	5. ind file: it shows all the insertions and deletions of the query genome (compared to the reference genome).

All above file formats are in text mode.

# Parameter setting

 ```
-t INT number of threads [4]

-i STR index prefix [BWT based (BWA)]

-r STR reference genome filename [fasta]

-q STR query genome filename [fasta]

-o STR prefix of output files

-dp Output Dot-plots

-fmt INT Set the output format [0]: 0:maf, 1:aln

-slen set the minimal seed length [20]

-alen set the minimal alignment length [200]

-clr set the minimal cluster size [100]

-gap set the maximal gaps between adjacent seeds [200]

  ```

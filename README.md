# CRISpyJZ
A modified version of CRIS.py (https://github.com/pinbo/CRIS.py).

CRIS.py searches two flanking sequences of gRNA in fastq files (plan text files), and check whether the gRNA was edited and compare the length with the wild type sequence to see whether there is an indel.

Please read the original paper, [CRIS.py: A Versatile and High-throughput Analysis Program for CRISPR-based Genome Editing](https://www.nature.com/articles/s41598-019-40896-w), to see how it works.

## Modification

1. Change inputs to command line parameters (reference sequence now saved in a fasta file)
2. Removed pandas dependency
3. Report all coverages (the original file ignore regions with coverage less than 10)
4. Now only one guide RNA at a time
5. Compatible to both python2 and python3
6. Search both R1 and R2 fastq files

## Usage

``` sh
python2 CRISpy_JZ_v2.py reference-file project-ID gene_name strand seq_start seq_end gRNA

# Example
python2 CRISpy_JZ_v2.py ../reference-example.fasta gene1-g10 gene1 + gcggagaactg ccggcccgga GAGGCAGGCGTCGAAGAGTACGG
```

Command line parameters:

1. **reference-file**: a fasta file with all reference sequences you will need, for example, "*../reference-example.fasta*".
2. **project ID**: a folder with this name will be created containing the result files, for example, "*gene1-g10*"
3. **gene_name**: the name of the target gene in the reference-example.fasta file, for example, "*gene1*"
4. **strand**: the strand of the reference where the three sequences after this are located. Two options "+" or "-".
5. **seq_start**: left flanking sequence, a unique 12-20bp sequence in your reference. Must be **5'** of the gRNA sequence. Case insensitive. For example, "*gcggagaactg*".
6. **seq_end**: right flanking sequence, a unique 12-20bp sequence in your reference. Must be **3'** of the gRNA sequence. Case insensitive. For example, "*ccggcccgga*"
7. **gRNA** : your gRNA sequence or its reverse complement sequence if you want to search on the "-" strand. Case insensitive. For example, "*GAGGCAGGCGTCGAAGAGTACGG*".

## Notes

1. The left and right flanking sequences and gRNA sequence must be on the same strand.
2. The left and right flanking sequences are used to find reads from your gene. For wheat, choose homeolog specific sequences around your gRNAs.
3. Use the commands in the `commands.sh` file in the *CRISpy_example* folder to see how it works. You can also run `sh commands.sh` to run all the commands. In your work, you can prepare the commands in an Excel sheet and paste them in a .sh file and run all of them at once.
4. You need open the terminal or `cd` to the folder with all the fastq files, then run the command, because the script searches fastq files in the working directory.


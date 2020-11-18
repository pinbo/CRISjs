# CRISjs
JavaScript to analyze CRISPR sequencing result on client side.

It is a JavaScript implementation of CRISpyJZ (https://github.com/pinbo/CRISpyJZ). All the processing happens on the client side (the users' computer), so you can put this tool on your static website.

Just like CRISpyJZ, CRISjs searches two flanking sequences of gRNA in fastq files (plan text files), and check whether the gRNA was edited and compare the length with the wild type sequence to see whether there is an indel.

To understand how it works, check out the **README** of [CRISpyJZ](https://github.com/pinbo/CRISpyJZ) and [CRIS.py](https://github.com/patrickc01/CRIS.py), and read the original CRIS.py paper, [CRIS.py: A Versatile and High-throughput Analysis Program for CRISPR-based Genome Editing](https://www.nature.com/articles/s41598-019-40896-w).

**If you need to do high-capacity analysis or just prefer the command line, check out the standalone command line tool [CRISgo](https://github.com/pinbo/CRISgo).**

## Usage

Just download or clone this repository, then click "**demultiplex-NGS.html**" if you need to demultiplex an interleaved fastq or fastq.gz file, then click "**CRISPR-editing-check.html**" to start processing individual fastq files.

You can try the example data by clicking "**Example Input**" and select the fastq.gz files in the "example-input" folder.

## Output
The output of "**demultiplex-NGS.html**" is a zipped file containing demultiplexed fastq.gz files.

The output of "**CRISPR-editing-check.html**" has part that is the same as the [CRIS.py](https://github.com/patrickc01/CRIS.py) output, but I also added the top 2 mutations and their positions (distance from the PAM).

The program will output a csv files reporting the percentage of intact gRNAs (no editing) and percentage of indels. It also gives the sequences and locations of the top 2 mutations (SNP or indel) and their percentages.

The first line is "Intact reference": the unedited sequences from the left flanking to the right flanking sequences. The 3rd line is the header of the output table. Explanations here:

> **fastq_file**: the fastq file name  
> **number_of_matched_reads**: number of reads that have both flanking sequences  
> **number_of_reads_with_intact_gRNA**: matched reads with intact gRNA sequence  
> **%intact_gRNA**: % of reads with intact gRNA sequence  
> **total_indel**: number of reads with an indel  
> **%indel**: %number of reads with an indel  
> **number_of_reads_with_leftSeq**: number of reads with the left flanking sequence  
> **number_of_reads_with_rightSeq**: number of reads with the right flanking sequence  
> **nleftSeq/nrightSeq**: number_of_reads_with_leftSeq / number_of_reads_with_rightSeq  
> **#1_mutation**: the most frequenct mutations (SNP or indel)  
> **#1_count**: number of reads with #1_mutation  
> **#1_%**:  #1_count / number_of_matched_reads * 100  
> **#1_seq**: the #1 mutation sequence from the left flanking to the right flanking  
> **#1_ref**: the reference allele  
> **#1_alt**: the mutation allele  
> **#1_bp_left_of_PAM**: distance from the PAM sequence  
> **#2_mutation**: the 2nd most frequenct mutations (SNP or indel)  
> **#2_count**:  number of reads with #2_mutation  
> **#2_%**: #2_count / number_of_matched_reads * 100  
> **#2_seq**: the #2 mutation sequence from the left flanking to the right flanking  
> **#2_ref**: the reference allele  
> **#2_alt**: the mutation allele  
> **#2_bp_left_of_PAM**: distance from the PAM sequence

## Notes

### demultiplex-NGS.html
1. The example input are the random adapters used in our lab.
2. You can use just the left 10 bp of the adapters to avoid PCR mutations if your adapter is long.

### CRISPR-editing-check.html
1. All the sequences should be on the same strand as the template (the wild type sequence of your gene)
2. All the 3 sequences (left and right flanking and the gRNA) should be on the same read (R1 or R2) in the fastq files. Usually we use PE150, which means the intact wild type sequence should be less than 150 bp. If your R1 and R2 has overlap, you can merge them first, so you have more choices of the flanking sequences.
3. If your R2 read (usually from your reverse primer) includes all the 3 input sequences, you should choose "*Reverse Strand*" near the button "**Start Analyze**".

## Acknowledgement
This app used [pako](https://github.com/nodeca/pako) for handling gzip files,  [JSZip](https://github.com/Stuk/jszip) for making a zipped file for download, [FileSaver.js](https://github.com/eligrey/FileSaver.js) for downloading files. Thanks to their authors.
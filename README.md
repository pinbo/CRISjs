# CRISjs
A JavaScript to analyze CRISPR sequencing result on client side.

It is a JavaScript implementation of CRISpyJZ (https://github.com/pinbo/CRISpyJZ). All the processing happens on the client side (the user's computer), so you can put this tool on your static website.

Just like CRISpyJZ, CRISjs searches two flanking sequences of gRNA in fastq files (plan text files), and check whether the gRNA was edited and compare the length with the wild type sequence to see whether there is an indel.

To understand how it works, check out the **README** of [CRISpyJZ](https://github.com/pinbo/CRISpyJZ) and [CRIS.py](https://github.com/patrickc01/CRIS.py), and read the original CRIS.py paper, [CRIS.py: A Versatile and High-throughput Analysis Program for CRISPR-based Genome Editing](https://www.nature.com/articles/s41598-019-40896-w).

## Usage

Just download or clone this repository, then click "**CRISPR-editing-check.html**" to start.

You can try the example data by clicking "**Example Input**" and select the fastq.gz files in the "example-input" folder.

## Output

The output has part that is the same as the [CRIS.py](https://github.com/patrickc01/CRIS.py) output, but I also added the top 2 mutations and their positions (distance from the PAM).

## Notes

1. All the sequences should be on the same strand as the template (the wild type sequence of your gene)
2. All the 3 sequences (left and right flanking and the gRNA) should be on the same read (R1 or R2) in the fastq files. Usually we use PE150, which means the intact wild type sequence should be less than 150 bp. If your R1 and R2 has overlap, you can merge them first, so you have more choices of the flanking sequences.
3. If your R2 read (usually from your reverse primer) includes all the 3 input sequences, you should choose "*Reverse Strand*" near the button "**Start Analyze**".

## Acknowledgement
This app used [pako](https://github.com/nodeca/pako) for handling gzip files,  [JSZip](https://github.com/Stuk/jszip) for making a zipped file for download, [FileSaver.js](https://github.com/eligrey/FileSaver.js) for downloading files.

Thanks to all the authors.
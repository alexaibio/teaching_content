# TOC
Glossary:
- NGS vs First generation sequencing.
- Reference genome, hg37, hg38
- SNPs Indels, CNV structural variations
- VCF file, variant calling


- raw read data, FASTQ file
- WGS, WES, microarray
- genomic alignment
- haplogroup, haplotype, phasing
- locus
- chromosome
- short read sequensing vs long read sequencing
- annotations in context of VCF, dbSNP, ClinVar
- mendelian vs poligenic diseases
- genetic variant databases, ClinVar, OMIM etc



#  DNA, First generation sequencing,  Next Generation Sequencing

To provide context for those unfamiliar with molecular biology, DNA is a crucial biological molecule found in the nucleus of every human cell. It encodes the instructions for producing other molecules (namely proteins) within the cell, specifying their order and the conditions under which they are produced. In other words, DNA serves as a universal software and data guide for biological processes in the cell.

It's important to note that DNA does not reflect the current state of the biological system but rather serves as a "code base" for all possible options. Each cell in the body contains identical DNA, so knowing a person's DNA code cannot provide definitive information about whether a person has a disease, its possible progression, etc. DNA is not used for diagnostics but rather for understanding the potential for certain conditions.

Nevertheless, a person's DNA is a valuable source of information, and various techniques exist to decipher it from a sample.


DNA sequencing technologies have revolutionized genomics and molecular biology. There are two major technologies behind sequencing: First-Generation Sequencing (also known as Sanger sequencing) and Next-Generation Sequencing (NGS), each with distinct processes and applications.

As the name suggests, First-Generation Sequencing was developed earlier. It is labor-intensive but highly precise. Due to its accuracy, it is still used today in scenarios requiring precise certainty, such as confirming a mutation for clinical diagnosis or in forensic science, where it is crucial to know if a mutation exists. Whenever you see an image like the one below, it typically pertains to Sanger first-generation sequencing (courtesy of Wikipedia).

![Sanger First Generation sequencing](img/sanger.png)

Although now somewhat automated, it remains a slow and labor-intensive process.

Due to its laborious nature, it is impractical to check many mutations simultaneously, so Next-Generation Sequencing (NGS) is used for large-scale sequencing.

Without delving deeply into the technology, the process involves cutting long DNA molecules into short pieces, usually 200-250 nucleotides (nt) long. Each piece is then sequenced separately, and the final results are obtained as millions of short sequences (raw reads). These reads are aligned to a reference genome and undergo further bioinformatics processing to generate a Whole Genome Sequence (WGS) or Whole Exome Sequence (WES). Alignments of raw reads look like the following:

![Alignment of Next Generation sequensing raw reads](img/alignment.png)

As a result of NGS, one can finally obtain a VCF (Variant Call Format) file, which represents all of a person's mutations compared to a reference genome.




# Reference genomes: NCBI, UCSC and EMBL notations

The goal of genetic sequencing is to determine how an individual's genome differs from a standard genome, identifying all genetic variations. However, there is no true standard genome, so the choice is somewhat arbitrary.

In 1997, thirteen volunteers from New York donated their blood for the first-ever human genome sequencing. This effort led to the creation of the first reference genome (reference assembly) through the Human Genome Project (HGP), completed in April 2003.

Since then, the reference genome has been regularly refined, resulting in several releases and a somewhat confusing nomenclature. Let's clarify it.

You might hear about GRChXX or hgXX references. Although they refer to the same underlying genome assembly, there are slight differences for historical reasons.

This redundancy exists because multiple organizations have taken on the responsibility of maintaining their own genome references:

    - NCBI (National Center for Biotechnology Information)
    - UCSC (University of California, Santa Cruz)
    - Ensembl / EBI

Each organization updates and manages its reference genomes, leading to different naming conventions and slight variations in their assemblies.



## NCBI
The National Center for Biotechnology Information (NCBI) in the US provides comprehensive genome sequences and annotations through the Genome Reference Consortium (GRC). This is why their reference genomes have names like GRCh38. NCBI focuses on ensuring that the genome assembly is as complete and accurate as possible.

You can download their reference genomes here ( https://www.ncbi.nlm.nih.gov/genome/guide/human/).



## UCSC

The University of California, Santa Cruz (UCSC) is renowned for its online genome browser, the UCSC Genome Browser. UCSC played a significant role in the Genome Reference Consortium (GRC) and actively contributed to the NCBI's effort to create a standard reference genome. They developed their own genome browser and, for reasons of their own, use a different naming convention for the reference genome within this browser, prefixing it with "hg" (human genome), such as hg19. Although it is essentially the same reference, the UCSC version has very subtle differences and richer genome annotations (e.g., marking the start and end of genes, splicing information, etc.). Due to the browser's popularity, the "hgXX" names have also become widely used.


You can download their reference genomes here: https://genome-euro.ucsc.edu/cgi-bin/hgGateway?redirect=manual&source=genome.ucsc.edu

Below is a table showing how the NCBI and UCSC references match up, highlighting the somewhat messy nomenclature.

|   NCBI name        | UCSC name    |   EMBL name  |   Relesae Date    |  
|--------------------|--------------|--------------|-------------------|
| T2T-CHM13          |  hs1         |              | January 2022      |
| GRCh38             |  hg38        |    GRCh38    | Dec 2013          |
| GRCh37             |  hg19        |    GRCh37    | Feb 2009          |  
| NCBI Build 36.1    |  hg18        |              | Mar 2006          |
| NCBI Build 35      |  hg17        |              | May 2004          |
| NCBI Build 34      |  hg16        |              | Jul 2003          |



Additionally, corresponding chromosome names:

|   NCBI name        | UCSC name    |   EMBL name  |   Relesae Date    |  
|--------------------|--------------|--------------|-------------------|
|  NC_000001.1       | chr1, chr2   |  1,2,3       |                   |



But this is not the whole story; Europe is involved too.



## EMBL and Ensembl
The European Bioinformatics Institute (EMBL-EBI) is a European organization responsible for providing comprehensive genome sequences and annotations. They have developed their own genome browser, Ensembl, which is known for its detailed and rich annotations. Ensembl includes extensive gene predictions, comparative genomics data, regulatory elements, and variation data. The Ensembl reference genome is also called GRChXX but has slight differences from the NCBI and UCSC references, adding to the overall complexity.

One of the challenges is that all three organizations use different chromosome names, making cross-annotation difficult. This discrepancy complicates the integration and comparison of data across different references.

Below is a table illustrating the differences in chromosome naming conventions among NCBI, UCSC, and EMBL.
|   NCBI name        | UCSC name    |   EMBL name  |   Relesae Date    |  
|--------------------|--------------|--------------|-------------------|
|  NC_000001.1       | chr1, chr2   |  1,2,3       |                   |


EMBL-EBI can be downloaded here
https://ftp.ensembl.org/pub/release-112/fasta/homo_sapiens/dna/

## Example of each reference

Here we illustrate the differences among the three references by comparing the names of chromosomes used in each reference:
![NCBI](img/ncbi_ref.png)
![UCSC](img/ucsc_ref.png)
![EMBL](img/ensembl_ref.png)


## T2T consortium

### Centromers
The initial sequencing efforts were able to sequence approximately 92% of the DNA found in human cells. Certain regions in human chromosomes are particularly challenging to sequence, namely the centromeres and telomeres.

Centromeres are located in the middle of a chromosome and ensure the proper segregation of chromosomes during cell division. They look like this:
![Centromeres](img/centromers.png)


Centromeres consist of long arrays of repetitive DNA sequences, known as satellite DNA, making them very hard to sequence. Sequencing technologies, especially those based on short reads, struggle to accurately map and assemble these repetitive regions. As a result, these regions often appear with gaps or no variants, depicted as follows:
![Centromeres](img/centromers_gap.jpg)


### Telomers
Telomeres are located at the very ends of chromosomes and consist of repetitive nucleotide sequences, typically TTAGGG repeated thousands of times. Telomeres protect the ends of chromosomes from deterioration and signal the cell to stop dividing when they become too short, a process associated with aging and cellular senescence.
![Telomeres](img/telomeres_1.png)

Telomeres are also repetitive so very hard to accemble by short read requencers

As of May 2020, the Genome Reference Consortium (GRC) reported 79 "unresolved" gaps, accounting for up to 5% of the human genome .

In 2021, it was reported that the Telomere-to-Telomere (T2T) consortium had filled in all of the gaps except five in repetitive regions of ribosomal DNA.


## Conclusion

So, which genome reference should you use? It depends on several factors.

Firstly, the utility of a reference genome is enhanced when it is accompanied by robust gene annotations and linked to mutation databases, which are typically closely tied to a specific reference assembly. For example, chromosome naming conventions must align.

Secondly, the data you have might already be linked to a specific reference. For instance, if you download your own VCF file from services like 23andMe, this file of personal mutations is already associated with a particular reference, so you have no choice but to use that exact reference assembly for subsequent analysis.

For the same reason, using the T2T reference isn't always the best choice currently, because most mutation databases have yet to release versions linked to this T2T reference, limiting the scope of subsequent analysis.

Understanding these nuances helps in making informed decisions about which genome reference to use, ensuring compatibility and maximizing the usefulness of your genetic data.





# Understanding Genetic Variations: SNPs, Indels, CNVs, and Structural Variations



Genetic variations are differences in DNA sequences among individuals, which can influence everything from physical traits to disease susceptibility. These variations can be broadly categorized into several types, including Single Nucleotide Polymorphisms (SNPs), insertions and deletions (Indels), Copy Number Variations (CNVs), and other structural variations.
Single Nucleotide Polymorphisms (SNPs)

Single Nucleotide Polymorphisms, or SNPs (pronounced "snips"), are the most common type of genetic variation. They occur when a single nucleotide in the genome is altered. For example, a SNP might change a DNA sequence from AAGGCT to ATGGCT. These variations can be benign, harmful, or have no effect at all. SNPs are often used in genetic studies to identify associations with diseases, traits, and responses to medications.
Insertions and Deletions (Indels)

Indels refer to the insertion or deletion of small DNA sequences in the genome. These can range from a single nucleotide to several base pairs. Indels can have a significant impact on genes and proteins, potentially causing frameshift mutations that alter the reading frame of a gene. This can lead to changes in protein function, which might result in disease.
Copy Number Variations (CNVs)

Copy Number Variations (CNVs) involve changes in the number of copies of a particular gene or DNA segment. Unlike SNPs and Indels, which affect small regions of DNA, CNVs can encompass large segments, ranging from kilobases to megabases. CNVs can lead to an increased or decreased dosage of the genes within the affected regions, influencing gene expression and potentially contributing to various diseases, including cancer and developmental disorders.
Structural Variations

Structural variations (SVs) are large-scale alterations in the genome that can include deletions, duplications, inversions, translocations, and complex rearrangements. These variations can affect large segments of DNA, sometimes involving entire chromosomes. SVs can disrupt gene function or regulation and are often implicated in genetic disorders and cancers. The main types of structural variations include:

    Deletions: Loss of a DNA segment, which can remove one or more genes.
    Duplications: Replication of a DNA segment, leading to multiple copies of genes.
    Inversions: Reversal of the orientation of a DNA segment.
    Translocations: Transfer of a DNA segment from one chromosome to another, which can disrupt gene function at both ends of the translocated segment.
    Complex Rearrangements: Combinations of multiple structural variations that can result in highly altered genomic regions.
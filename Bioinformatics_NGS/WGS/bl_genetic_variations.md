
# Understanding Genetic Variations: SNPs, Indels, Structural Variations and CNVs


Genetic variations are differences in DNA sequences among individuals, which can influence everything from physical traits to disease susceptibility. Usually by genetic variations people mean not the differences between some random individuals, but the difference bewteen universal **reference genome assembly** (Link) and genome of an individual person.


These variations can be broadly categorized into several types, namely
- Single Nucleotide Polymorphisms or Variations (SNP, SNV), 
- insertions and deletions (Indels), 
- Copy Number Variations (CNVs), 
- other structural variations.


## Single Nucleotide Polymorphisms (SNP or SNV))

Single Nucleotide Polymorphisms, or SNPs (pronounced "snips"), are the most common type of genetic variation. They occur when a single nucleotide in the genome is altered. For example, a SNP might change a DNA sequence from AAGGCT to ATGGCT. These variations can be benign, harmful, or have no effect at all. SNPs are often used in genetic studies to identify associations with diseases, traits, and responses to medications.

(picture from browser)

It worth mentioning that a single mutation (SNP) very reare causes a disease. Most diseases are caused by mutations in more than one gene, i.e they are polygenic. The exception are co-called Mendelian diseaes.

Mendelian diseases are collected in OMIM datamase. 
OMIM, Online Mendelian Inheritance in Man, is a regularly updated, online database established in 1997 by Dr. Victor A. McKusick that is focused on inherited genetic diseases in humans. OMIM reported ~400 human genes of known sequence with a known phenotype, and ~2000 human phenotypes with a known molecular basis.

All the rest are poligenic and making conclusions about them are much more complex.

SNP are usually called from aligned raw NGS data with co-called **variant callers** like GATK, FreeBayes and are included in vcf file


## Insertions and Deletions (Indels)

Indels refer to the insertion or deletion of small DNA sequences in the genome. These can range from a single nucleotide to several base pairs, but by the rule of thomb indels are up to 50bp. 
Indels can have a significant impact on genes and proteins, potentially causing frameshift mutations that alter the reading frame of a gene. This can lead to changes in protein function, which might result in disease.

(picture)

Calling of indels are also done with variant callers above.

In a VCF file, an indel is represented in the ALT field where the alternative allele shows the insertion (e.g., A becomes ATC) or deletion (e.g., ATC becomes A).




## Large structural variations

### Structural variants (SV)
The difference between SNP, indels and structural variants lies in the scale and type of genetic change:
- SNPs involve a change of just one nucleotide in the DNA sequence, like a single base pair substitution.
- indel is up to 50bp
- Structural variants are larger then 50bp. Beside indels it might be duplications, inversions, and translocations.

so, SNP and indels are small-scale changes, while structural variants are larger, more complex alterations in the genome.


The main types of structural variations include:
- Deletions: Loss of a DNA segment, which can remove one or more genes.
- Duplications: Replication of a DNA segment, leading to multiple copies of genes.
- Inversions: Reversal of the orientation of a DNA segment.
- Translocations: Transfer of a DNA segment from one chromosome to another, which can disrupt gene function at both ends of the translocated segment.
- Complex Rearrangements: Combinations of multiple structural variations that can result in highly altered genomic regions.

SVs can be represented in a VCF file, typically using the SVTYPE INFO field to describe the type of structural variant (e.g., DEL for deletions, DUP for duplications).

Also, BED files may be used to describe the genomic intervals affected by SVs.


### Copy Number Variations (CNVs)
Copy number variations are type of structural variant where a segment of the genome is present in more or fewer copies than the normal two copies (one from each parent). 

Types of CNVs:
- Amplifications: Increase in the number of copies of a genomic segment.
- Deletions: Loss of one or more copies of a genomic segment.

CNV is a also a structural variant but by definition (the whole gene must be affected) it affect large segments, ranging from kilobases to megabases. CNVs can lead to an increased or decreased dosage of the genes within the affected regions, influencing gene expression and potentially contributing to various diseases, including cancer and developmental disorders.


CNV коллеры, которые это делают через профили покрытия, хорошо начинают работать где-то с 1000 бп. 
BED: BED files can be used to describe the locations and types of CNVs.

The most popular CNV callers are:
- GATK4 includes a module specifically for detecting CNVs, both gains and lossesб щгезге вфеф шт МСА
- CNVnator is a tool designed for CNV discovery using read depth from next-generation sequencing (NGS) data, output data in BED
- EXCAVATOR2 is tailored for detecting CNVs in whole-exome sequencing (WES) , output in BED
  
CNVs are often implicated in various genetic disorders, including developmental delays, intellectual disabilities, and cancer. Understanding a patient's CNV profile can guide treatment decisions, particularly in oncology, where certain CNVs are associated with prognosis and response to therapy.










## harmless of mutations
- deleterious: transcript ablation , frameshift mutations
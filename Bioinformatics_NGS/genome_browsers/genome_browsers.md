# Genome browsers: a first look at your genome

## Why you might need a genome browser?
A first intention after you finally got you Nexg Generation Sequensing (NGS) data is to take a first look on it and the most convinoent tool for it is genome browser.

The typical result of processed [NGS data](https://offsiteteam.com/knowledge-base/dna__first_generation_sequencing__next_generation_sequencing) whether it is whole genome sequencing (WGS) or whole exome sequensing (WES) is annotated VCF file. 

VCF file contains all individual mutations up to length of 50bp. The typical size of human VCF file with WGS data is in a range of 1G - 2G depending on annotation. 

Often it is also informative to take a look on .BAM file which provides information about coverage of each mutation (depth) so we know the level of certainty for each mutation. The size of BAM file is about 40G (if the sequencing was done with 40x coverage).

Of cource you can just explore these large VCF and BAM files in text editor (it has quite a clear human readable format) or you can use self-written Python/bash script to explore them, but it makes much more sence to use some kind of tool to do that. One of such tool might be a genome browser.


## Which genome browsers exists?

The most widely knowns are the following four:
- IVG ((Integrative Genomics Viewer))
- IGB  ?????
- JBrowse desktop ???? - https://jbrowse.org/jb2/
- Ensembl Genome Browser
- UCSC Genome Browser
- NCBI Genome Data Viewer (GDV)

Genome broswers might be online and offline (stand-alone) and IGV is probably the most known from above offline browser.

Being online/offline provides its own pros and cons. On one hand online genome browsers do not require any installation or updates and always provides up-to-date genome and variation annotation information. On the other hand uploading 1G VCF might be a problem and it is also not secure, after all you are uploading a very sensitive information to somemobody else's server.
Also having browser on your local computer is generally faster and provide less latency with improve usr experience.

In this review I will concentrate on IGV genome browser because amoung all four above it is the only one which is offline.

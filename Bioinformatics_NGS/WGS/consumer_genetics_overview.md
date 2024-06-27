# Consumer Genetics Overview

## Intro
Consumer genetics got some pupularity in past decade because of significant progress in NGS sequencing. Modern sequencers like Illumina provide quite cheap short-read DNA sequensing, currently for a price of order of 300$. 

Glossary:
- NGS vs First generation sequencing.
- VCF file, variant calling
- SNPs Indels, CNV
- Reference genome, hg37, hg38
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

Usually consumer genetics companies request to provide a sampe of your saliva, then do a short read sequensing (or althernatively apply a micro array technology) and send you several base reports (Fitness, wellness, pharmacogenomics etc) along with raw data and processed mutation data. Adding more reports costs more money. Often a subscription is required, so the cost might be doubled. Each company migh have sligtly different focus: Some of the companies might foucus on ansestry, some on genomic pre-disposition reports. Ansestry is a bit more complicated , because it requires collecting a lot of samples from people from diferent regions and this information is not easily available.

## Technical Things to consider when choosing a consumer genomics company
All companies look similar but the devil is in details. Usially a final result of sequnsing is a VCF file which contains all detected mutations and it might have been gotten with different kind of technologies, usually it is  microarray or short read NGS. 
The difference is quite important. 

Microarray is a cheaper option and in essense is a plate with limited number of DNA probes which bind (hybritizr) to a sample DNA in case their match, so one can say if this particular mutation is present in the sample DNA. As you can understand from this description microarrat can only detect existing known mutations (SNP, indels etc) and often quite behind up-to-date databases.

In contrast with NGS technology you merely scan the whole genome (WGS) or exome (WES) for all mutations and can always re-annotated your vcf file with the recent update of clinical and other databases.

WGS companies also probide you with a RAWS read data, so you can not only re-annotate you  data with recent databased but also re-align your genome to a new reference, which ugiall yhappens once in a decade with a new more precise reference genome


## What I can get out of sequencing my genome: reports
That is usually the main question: why do I need it and what can I do with it? 
Companies usually provides reports like
- medical report
- fitness
- wellness
- pharmacogenomics

For medical reports they check your mutation with a ClinVar, OMIM and other databases, where all associations with diseases are written, so you have it like this: People with your genetic profile are likely to have the predisposition for XXX condition.
So if you have a predisposition to any of diseases, they will tell it. It is important to understand that one should get those medical reports with some kind of scepticitism. The point is there are only limited number of diseases which are clearely depends on genetics, they usually caused by a very precise mutations in one or several genes, which make these genes disfunctional and cause disease. Such diseases are called Mendelian and the most famous case is sicle cell anemia. But in contrast to mendelian diseases most of existing diseases have a weak link to a genetic, which means that the real link between genes and diseases is not certain (just assosiated with) and scientist use statistics to assosiate these diseases with a number of genes, like is these 100 people have this diseases and one mutation is overepresented in their population, it means that these mutations have some degree of assosiation with that disease. So if those mutations are found in someone genome, they add up to a risk to have this disease but not guarantee it. 
Before considering a varint as a harmfull, one has to consider many other things, like allele frequency in population etc. So, dont panic even if you found a harmful variant in your report

Why that information anyway might be usefull for someone? Well, in some cases it might motivate one to change his/her lifestyle, for example if one has a predisposition to respiratory disease it might help to quit smoking etc. In some cases it might help to make a better diagnos, but one has to be carefull here, due to statistical nature of NGS there might be artifacts, so for medical purposes it is imperative to confirn NGS by more presice Sanger seguensing.

For fitness you have it like this: People with your genetic profile are likely to have a good starting sprint.

Basically, it shows in which sport activity you can achieve most significant results based on genetic variants. That test might be usefull if you plan a sport career or to simply understand you bode better.

Pharmacogenomics  reports show a possible side and adverse effects for different kind medications. 

## What I can get out of it: Ancestry
Another important information which might be extracted from your genome is your personal ansestry. It might be seen from two different angles, first your personal ansestry, i.e. answering the questins which people are your distant relatives? May be you have someone who is your relative and you even dont knoe that?
Another angle is to define which pieces of world are your ansestors came from. May be you are a distante ansestor of vikings or romans conquers? 

Ansestry is more complicated staff then mutation reports and not all companies can provide it at a nessesary precision and scale. Usually it is a separate type of companies, which try to collect as many as possible samples, crete its own database and then look into this database to find spmeone close to you enough to be marked as relative.

Defining a population ansestry is done by collecting genetic samples from people living in rural areas for a long time, which garantees for some extent that they did not move and represent a stable population. Sequencing people living in big cities does not make a lot of sense, because they all probably move in in receant 100 or so years and might originate from totally different places. Then based on this data, a specific "haplotypes" are defined and linked to places they came from. If such a haplotype is found in your genome, it means that one of your ansestors originated from a very specific place. Thise haplotypes are stored in open databases.

Another issue is that process of sequence analysis is a bit more complicated.  Ansestry is defining with haplogroups, i.e. a genomic regions which are heredited together. Due to recombinations the parents genomes are mixed together in a discrete way, so direct relatives will have a lot of similar haplogrpps but the father people from ansestry point of view the less hapogroups they will have in common. So, for a certain communities there are several haplograoups, so if you have it you belong to that population.

Using haplogroup require more sophicticated analysis, because in contract to SNP detection which basically states which options of a certain locus you have one need to know the sane for each chromocome

# Modern drug development process and Artificial intelligence

# History
Drug discovery proceess, i.e finding new medications to help cure diseases initially was driven either by chance or by a single person who truly belives in his mission and spent significant part of his life to find a new drug. Discovery of a novel drug was rare and that drugs often suffer from unexpected side effects or questionable effectiveness.

Two things have changed the game. First, modern clinnical trials (double blind and placebo-controlled) which which help to prove effectiveness and measure side effects and second a high trhoput screenings (HTS) which make the process of new chemical discovery systematic and not random.

Currently, there are two wide types of drugs: 
- small molecule (usually called drugs), they are  sythetised by pharmaceutical companies
- large molecule or biologics, usually a protein of other biological macromolecules which are not syntesised but created by living bacterial, yeast, or mammalian cells by biotechnology companies.

Usually the creating of a ready for market drug takes up to 10 years and costs up to a billion of dollars

Ricently a large effort to engage Artificial Intellegence (AI) technigs were taken by many companies to make this process shorted and cheaper.

It also worth mentioning that one should distinguish a novel drug discovery process and drug-repurposing process. The latter (re-purposing) is usually much less expencive because the drug is just repurposed for a new indication the company can skip all preclinical development together with Clinical Phase I safety stage.



# Modern Drug Development Cycle

Modern Drug Development Cycle consists of three major stages
- Drug Discovery
- Preclinical development
- Clinical development



# Stage I: Drug Discovery
This is where it all starts.

## Choosing a condition
First of all, one or several related diseases (conditions) have to be selected (a particular cancer type, or a neuro disease etc). Usually this choice is dictated either by business or by previous expertise of the company.

## Target identification/discovery
Then one has to look for a number of biological targets assosiated with this condition. By targets usually people mean enzymes, cell surface receptors (for example most known G-Protein-Coupled Receptors, GPCR), ligand-gated ion channels or gene transcription factor, anything which can influence a disregulated biological process. As targets might be considered both proteins itself or genes which produce those proteins.  

Identifuing a right target is not a trivial task. It might be done in the following ways (link to a separate article)

### use known targets: 
by searching databases like OpenTarget or Therapeutics Target Database (TTD) for known targets assosiated with selected disease. Also looking for a reacent scientific publication might help a lot, because the novel targets might not be in databases but be buried into one of fresh papers (here is where NLP and LLM can come into a play!).

### re-purpose existing target: 
try to "re-purpose" the known target, i.e. take a target assosiated with a disease and try to prove that it also influence another disease (the one under under investigation)

### novel target discovery: 
try to find a completelly novel target. It might be done again by be done several ways, either analytically or be a data driven.
  
  - **by molecular screening through the phenotype** : for example by subsequently applying many potential drugs to a number of cancer cell lines in hight throuput screnning (HTS) settings. If by chance one type of a cancer (cell lines) exchibits lower proliferation under a certain drug it means it worth investigation and look for a particular mutated gene in this cancer line etc, which might help to identify a novel target. Same result might be achieved by gine knock-out screening via CRISP or RNA interference, like in DepMap study, but in this case cancer cell lines affected not by drugs but by knocking out each gene and see if knocking out a paticular gene will influence cancer cell line prolifiration
  - by **more complex phenotupe screening**. In previous screening example the phenotype was quite simple, it was just changing in proliferation of the cancer cell lines. For other indications phenotype can be much more complicated. For example for neuro indications it is not as easy as with cncer cell line proliferation to distinguish disease phenotype from normal one. In this case more complex phenotype might be used like SmartCure from XXX company. They do a video surveilance analysis of mices and from that video recording they extract a simple features like how many time a mouse is sitting in a corner or how fast is it moving etc. Based on that feature it is possible to if this mouse a Normal one or have some kind of neuro disese. Having this it is possible to do a neuro drug screening as well.
  - by exloiting someone's **intuition** or analytically by manually analysing molecular pathways assosiated with disease and finding a weak point in it, then try to reason that this protein/gene might be a target
  - by exploiting **combinations effects** such  as drug synergy or synthetic lethality effect.
  - by studying molecular data and looking for **molecular biomarkers**. For example if we have RNAseq data for control and disease state and we can identify a specifig gene which is differently expressed that gene might be a candidate to futher investigation and be a potential gene target.
  
  - AlphaFold etc?
  - else??? look for a paper
  - COA - co-expression analysis


## How AI can help at the target identification stage?
Actually in many ways. 
Lets start from the **drug screening studies**. Usually screening is done for a limited number of cell lines and drugs. Over time new drugs have emerged or company wants to check their newly developed drug against many cell lines quickly and cheaply, but this combination of disease/drug is not in initial HTS study. In that case an AI model can be created to predict an effect of applying an unseeng drug to each existing cell line. It is usually done by representing each small molecule as a feature vector (as a Morgan fingerprints for example) and training a model to predict effect based on this model. The model might be liner, random forest or even a neural network, it depends on amount of training data presented in an initial study.
Making a predicting model became even more usefull when a drug synergy is tested (applying a combination of drugs to each cell line) because the space to explire grows exponentially and it becoume unpossible to come it all.

For known targets and target re-purposing the Natural Language Processing (NLP) starts playing a significant role. Despite several target databases exists, many potential targets are still buried inside academic publications. So, it becomes crucial to quicky process large amount of publications by either regularly scanning PubMed or better full text publications (of the compaby has access to it) in order to find a unseeing potential target. Large Language Models (LLM) are of greate helt here, they can do it without human intervention quite good.

re-purposing might be done with knowledge graph construction



## Potential Draggability of a target - is there a binding site?
Having a target candidate the next step would be to understand if one can indfuence this target, i.e if this target is druggable. In some cases a drug has already been identified for a target, one can see it from Drug Bank database for example. 
Druggability refers to the likelihood that a target can bind with high affinity to a small molecule or biologic in a way that modulates its activity to achieve a therapeutic effect.
The goal is to assess whether the target has suitable binding sites for small molecules or biologics and whether these interactions can lead to a desired biological response. This step often involves computational modeling, structural biology, and analysis of known binding sites.

If a drug has already been identified for a target, that target is by definition druggable. If no known drugs bind to a target, then druggability is implied or predicted using different methods that rely on evolutionary relationships, 3D-structural properties or other descriptors
- AlphaFold?!
- AI in draggability?


## Target Validation
Before we go for any kind of expensive experiments it is important to preliminary proove that affecting selected taget will ever change to disease progression or biological process.
Target validation might be done by
- by finding a scientific publication which prove it for some extend
- in-silico, for example 
  - by modelling binding targets and their ligands
  - from gene side: by creating a model of nessesary gene expressions and showing that knock-down (reduce expression) or knock-out (stop expression) the target will affect the system in a nessesary way, i.e disease expression profile is moving toward health expression profile
  - from proteomics side: by proving that it is possible to create **antibodies** directed **against target protein**

Usually at this stage it is also common to identify biomarkers, i.e. molecules or any other measurements which can be used to measure effect on our target.

Biomarkers are measurable indicators of a biological state or condition that can be used to identify or predict responses to a drug, the presence or progression of a disease, or the effectiveness of a therapeutic intervention. 

Biomarkers can be genes, proteins, metabolites, or other molecules that provide insight into the underlying mechanisms of a disease and how a drug might interact with those mechanisms.


## Hit identification: a drug candidate
At this stage we have the disease and the target which can affect this disease. 
Now we need to find a drug.
This stage involves finding chemical compounds (referred to as "hits") that interact with the druggable target identified in the previous step. Hits are molecules that show some degree of binding or biological activity against the target. 

It might be a small molecule
- we can find molecule that will bind to the target in-silico (AlphaFold)
- we can do it by HTS, start from compound library (~100 000) and see the effect

or a biologic (might be **monoclonal antibodies: mAb or moAb**)
- how it can be done?


 The primary goal is to identify and validate small molecules or biologics that can interact with the target in a meaningful way. This is usually done through high-throughput **drug screening (HTS)** of large chemical libraries, virtual screening, or fragment-based approaches.


## Lead Generation: some optimization   
At this point we roughly have everything, a disease to cure, a target (proteine or gene) and a number potential drugs (chemical compounds or biologics) which already exchibit some activity on that target.

But to reduce risk on futher expencive preclinical/clinical steps we need to futher refine this drug list

So, **Lead generation** is the process of taking the initial hits and optimizing them to create lead compounds—molecules that are more likely to be effective, safe, and suitable for further development as drugs. Hits from the previous step often have some activity against the target, but they are usually not yet optimized for use as drugs.

So, what we need to do is the following
- Optimization of Activity: Hits may bind to the target, but they might not do so with enough strength (affinity) or selectivity.
- Reduction of Toxicity: Initial hits might show promising activity but could also have toxic effects. (presence of toxic groups) 
- Improvement of Drug-Like Properties: The initial hits may not have ideal drug-like properties. Lead generation addresses:
    Solubility: Ensuring the compound can dissolve properly in biological fluids.
    Stability: Making sure the compound is stable under physiological conditions and doesn’t degrade too quickly.
    Absorption, Distribution, Metabolism, Excretion (ADME): Optimizing how the compound is absorbed, distributed in the body, metabolized, and excreted.
    
At the end of drug discovery process we have at least one **LEAD**,  a tripple of disease-target-drug which potentially can affect disease in a needed way.
But all those conclusions so far were done outside of real biological systems, even if it was on at cell line level it was just concentrated on founding affect without focusing on how the drug affect the cell as a whole, now the next step would be to check if it works on biological non-human models: mises etc.  



---------------------------------------------------

# Preclinical testing
As a result of the drug discovery stage we have one or several candidate tripplets disease-target-drug and the goal of preclinical testing is to prove that it is effective and safe enough to try it on humans.

A result of preclinical testing must be filling of **Investigational New Drug (IND)** application.

Preclinical testing is mainly about **efficacy and safety (toxicity)**.
It includes **in-vitro testing** and **in-vivo** testing on animal models, i.e. usually mices with induced disease-like conditions.

Preclinical testing is mandatory, without it a regulatory authorities (FDA, etc) wont issue a permission to test it on humans.

There are three parts in IND applications: 
- **formulation development** - the best way to prepare a drug in the preclinical phase for its intended clinical use in patients
- **pharmacology** (on animals) - 
  - PK and ADME is the backbone of pharmacology.
  - PD and safety 
- **toxicology** - he toxicology studies aim to look at the effects of longer-term drug exposure on the body, including repeat dose studies.

also clinical protocol and investigator information - detailed protocol for proposed clinical stadies


## PK - pharmacokinetics

Pharmacokinetics (PK) refers to the study of how a drug moves through the body over time (what the body does to a drug?). 

PK is typically divided into four key stages, summarized by the acronym ADME:
- **Absorption**: How the drug enters the bloodstream after administration. Administration might be done as oral, intravenous (injected directly into the bloodstream), or topical (applied to the skin) and absorption heavily depends on this route of administration.
- **Distribution**: This stage determines how much of the drug reaches the target site where it will have its intended effect.
- **Metabolism**: Metabolism typically transforms the drug into more water-soluble compounds that can be more easily excreted from the body. 
- **Excretion**: The process of eliminating the drug from the body, primarily through the kidneys (urine) or the liver (bile/feces). This stage determines how long the drug stays in the body and continues to have an effect.

The usual outcome of these studies is to define
- Concentration-Time Profile: concentration-time curve
- Key Pharmacokinetic Parameters: Cmax (Maximum Concentration): The highest concentration of the drug observed in the blood after administration, Tmax (Time to Maximum Concentration), AUC (Area Under the Curve): Represents the total drug exposure over time;  etc
- Absorption Characteristics: Bioavailability: The fraction of the administered dose that reaches the systemic circulation in an active form (especially important for oral drugs)
- Distribution Profile: Information about how the drug is distributed in different tissues and organs.
- etc

All these properties have to be studied first in-vitro and then on an animal models before it enters clinical trials on human

At this PK stage there is a room for AI:
- Predictive Modeling: AI can be used to predict how a drug will be absorbed, distributed, metabolized, and excreted based on its chemical structure. (references?)
- Virtual Screening: AI can simulate how a drug will interact with the body’s enzymes, proteins, and other molecules. This can help predict potential metabolic pathways and interactions early in the development process, (???? check for references)
- Optimizing Dosing Regimens: AI can help in designing personalized dosing regimens by analyzing patient-specific data, such as genetic factors, that influence how a drug is metabolized and excreted. 
- Accelerating ADME Profiling: AI can speed up the ADME profiling of new compounds by predicting the pharmacokinetic properties of large libraries of compounds, 
- ?????


## PD: pharmacodynamics
Focuses on understanding the effects of a drug on the body, what drug does to a body.
More precisely, it is the relationship between drug concentration and its biological or therapeutic effects.

Identify Therapeutic and Toxic Effects. It is done by:
- more detailed understanding of the **Mechanism of Action (MoA)**: how the drug interacts with its biological target (e.g., receptors, enzymes). It usually requires revisiting primary target interactions as well as Identification  Off-Targets (additional proteins or receptors the drug interacts with, which could lead to side effects)

- targets must be also revisited because in The initial target identification and validation often occur in simplified systems, such as cell lines or biochemical assays (in-vitro). However, a living organism's complexity (in-vivo) can reveal new interactions or effects not seen in these early models.

Evaluate **Drug Potency and Efficacy** and Establish the **Effective Dose Range**
- understanding Binding Affinity: IC50/EC50 Values: Concentration of the drug required to inhibit or activate 50% of its target (measure of drug potency)

- Dose-Response Relationship: quantitative data on the relationship between drug concentration and the magnitude of its effect, usually as 2D plot
 

## Biomarkers at PD stage
At the PD stage discovering **biomarkers** plays an important role as they are serving as measurable indicators of the biological processes that a drug influences.
In plain words, biomarkers are any measurable substance or parameter which might say you that a biological process has changed its behaviour, you basically track effectiveness of you interventionby measuring biomarkers.

Biomarkers can help validate that the drug is engaging with its intended target. For example, if a drug is designed to reduce cholesterol by inhibiting a specific enzyme, a drop in cholesterol levels would serve as a biomarker confirming target engagement. Other cardio biomarkers are cholesterol / myoglobin / creatine kinase (CK). For diabetes they are adiponectin / hemoglobin A1c, etc

Biomarkers are also used to monitor potential toxic effects or off-target interactions. For example, liver enzymes in the blood (like ALT and AST) might be monitored as biomarkers to detect early signs of liver toxicity.

## other important terms related to preclinical testing
- **bioavalability** - какой процент и скорость с которой API (Active ParmaI Ingredient) достигает места действия. обычно сложно померять концентрацию в нужном органе  - поэтому обычно меряют концентрацию в крови (для внутривенный считают **bioavailability = 100**)
- **bioequivalence** - изучают различные формы выпуска, способы доставки и тд и то как это влияет на эффективность лекарства


## Filling Investigational New Drug (IND) application 





----------------------------------------

# Clinical testing
Any drug development company has to complete  a **Investigational New Drug (IND)** applications based on they Pre-clinical testing and submit it to their local regulatory body (FDA etc) in order to enter clinical trial.

For the UK it is the **Medicines and Healthcare Products Regulatory Agency**,  for USA it is  the **Food and Drug Administration, FDA** and for Europe, it is the **European Medicines Agency (EMA)**.

Clinical trial phase might only be started after IND is approved. Approval depends on the results of pre-clinical testing if they are appealing to FDA.

Before we start explaining clinical trials development proces it would be good to explain some terminology

- **Sponsor**, this is an organization which pays for clinical study. This usually involvet a lot of money and it is done by a company who do drug develpment.
- Sponsor hires a **CRO** (Contract Research Organization) usualy a respectfull clinical site which becomer responsible for enrolling patients and doing actual clinical trials.
- **generics** - после истечения 20 лет, но 20 лает начинаются не с launch but from clinically?, small molecules очень легко скопировать в отличие от biologics - почти невозможно создать точную копию - и они навоюются biosimilars
- **biosimilars** - должны проходить дополнительный clinical testing - чтобы доказать что они работают
- **biosuperiors** - иногда biosimilars работают лучше чем оригинальное лекарство - тогда их назвают biosuperiors - их тоже надо тестировать клиники перед запуском


## Phase Zero: INS health check
Phase 0 trials are very small-scale studies that involve a few participants (typically fewer than 15). The primary goal is to gather preliminary data on the drug’s pharmacokinetics and ADME i.e. how the drug behaves in the body.

Participants are given subtherapeutic doses of the drug (doses lower than those expected to have a therapeutic effect) and researchers collect data to understand how the drug is metabolized and how it moves through the body.

As an outcome it is expected to get early insights into whether the drug behaves as expected in humans in terms of effect and side effects. This helps in making informed decisions about whether to proceed with further clinical development.


## Pahase I: safety, testing on healthy people
The goal is to determine **the highest dose** of a drug that can be safely administered to human without serious side affects.
Typically is done on 20-100 healthy volunteers with so-called **dose escalation** method i.e. by administering gradually increased dose till side effects are starts to apper. Iy might be done in two ways
- SAD - Single Ascending Dose studies - populating is diveded in several group and each grou have different dosage (ingle dose per participant, different doses across groups)
- MAD - Multiple Ascending dose - dosage is gradually increased for every person (Multiple doses per participant, with doses potentially increasing)
PK/PD are assesed.

As an outcome the safe dosage range and identifies any potential side effects. This phase is crucial for determining how the drug can be administered safely in later phases.


## Phase II: effectiveness in patients with disease
Phase 2 trials aim to assess the drug’s efficacy with typically 100-300 patients who have the disease or condition that the drug is intended to treat.

Is done in two stages
- phase 2a - find a dose level that has a desired effect of treating the disease
- phase 2 - this dose level is then used in phase 2b to confirm the efficacy

This is the most rigorous trials where single blinded (when pacient does not know if he is taking drug or placebo) or double blinded (when doctor also doe not know it) are applied. 
One of he problem on this stage is to enroll enough patients espesially if a rare disease is tested.

Successful Phase 2 trials show that the drug has a therapeutic effect and justifies further testing in larger populations.



## Pahase III: efficasy in large patient population
This stage lasts several years  with >1000 patients in several countries, so multiple test sites are required. These are large-scale studies that aim to confirm the drug’s efficacy, monitor side effects, and compare the drug to standard treatments. 

The drug is tested in a much larger and more diverse patient population.
Researchers compare the new drug to existing standard treatments or placebos to determine its relative efficacy.

On this stage a label expansion also possibe, i.e to test a drug agains other diseases.

If Phase 3 trials are successful, the data are used to submit a New Drug Application (NDA) or Biologics License Application (BLA) to regulatory agencies. The result of this application is positive, the drug is approved for market and sales begin.


## Phase IV: Launch and Post-Marketing Surveillance
It starts after NDA or BLA are approved and drug starts selling on the market.
pricing, brand name, package design must be selected

Phase 4 trials occur after a drug has been approved for market and are designed to monitor the drug’s long-term effectiveness and impact, as well as to detect any rare or long-term side effects.

Thousands of patients in real-world settings, often including those who were not part of earlier trial phases.

Post launch surveliance included:
- **pharmacovigilance** - constant observation of new drug after it goes live
- adverse events - looking for new unexpected side effect after drug applied for large population
- drug-drug interaction
- on that stage are also investigated **drug repurposing** and **drug combinations**



# AI in clinical
- de-risk and accelerate clinical trials






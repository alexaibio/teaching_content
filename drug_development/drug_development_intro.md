# Modern Drug Development Process in Brief

## The drug discovery process
Historically finding new medications to help cure diseases was originally driven either by chance or by the efforts of a single individual/lab who truly believed in their mission and dedicated a significant part of their life to finding a new drug. The discovery of novel drugs was rare, and these drugs often suffered from unexpected side effects or questionable effectiveness.

![Drug development cycle](img/drug_dev_cycle.jpg)

Two major advancements changed the landscape. First, modern clinical trials, particularly double-blind and placebo-controlled studies, were developed to rigorously prove effectiveness and measure side effects. Second, high-throughput screening (HTS) transformed the process of discovering new chemicals from a random endeavor into a systematic one. 

Today, there are two broad categories of drugs:
- Small molecules (commonly referred to as drugs), which are simple chemicals and they are synthesized by pharmaceutical companies.
- Large molecules or biologics, which are typically proteins or other biological macromolecules. These are not synthesized chemically but are produced by living cells—such as bacterial, yeast, or mammalian cells—by biotechnology companies.

The development of a market-ready drug usually takes up to 10 years and can cost up to a billion dollars.

Recently, significant efforts have been made by many companies to incorporate Artificial Intelligence (AI) techniques into the drug discovery process at various stages, with the goal of making it faster and more cost-effective.

It is also important to distinguish between the discovery of novel drugs and drug repurposing. The latter is usually much less expensive because the drug is simply repurposed for a new indication or dosage or packaging, allowing the company to skip the preclinical development stage and the Clinical Phase I safety stage altogether.

Modern Drug Development Cycle consists of three major stages
- Drug Discovery
- Preclinical development
- Clinical development


## 1: Drug discovery stage
Drug is never exists in isolation, so finding a drug essentially means finding a tripple disease-target-drug.

In general on a drug dicovery stage a drug discovery team must come up with several candidate triples **disease-target-drug** which then shall be hanged over to pre-clinical team for much more expensive testing, so the beter work is done on this stage the less money will be spent on the preclinical stage to rule out wrong candites.

### Disease
For a drug discovery company choosing one or several diseases (aka conditions, indications) to cure is usually a starting point. For example the company first decides to find a drug for lung cancer  and then go next step to target discovery and then to drug itself.

For a drug-repurposing company it might be other way round. Since they are trying to re-purpose the existing drug they might start from a drug then go back to find a target affected by this drug and then proceed to another disease, that is an idea behind repurposing.

### Target
After pinpointing the disease a target must be selected and that is where the real discovery process has actually started. 
Target is usually a protein or a gene, which might be targeted to affect biological process in a needed way. 
One might deside to look for completelly novel target or choose several existing targets from target databases and then try to find a novel drug for that target. 
Both of these method can be heavily augmented by artificial inteligence method, we will write about concrete methods in our futher posts. 
The target discovery is a large topic by itself and we will address it in the follwoed more detailed article.

### Drug 
Finding a drug started from a so-called **hit identification**, i.e. finding a chemical compounds (referred to as "hits") that interact with the target identified in the previous step. 

Binding or activity might not be strong or sufficient enough, so a next step, called **lead optimization** is nessesary. At this step Optimization of Activity, Reduction of Toxicity and Improvement of Drug-Like Properties might be performed.

Again, this is a step where AI can help a lot and again we will adress it in more detailed article.

At the end of drug discovery process we have at least one **LEAD**, i.e  a tripple of disease-target-drug which potentially can affect disease in a needed way.
But all those conclusions so far were done outside of real biological systems, at cell line level or even in-silico, now the next step would be to check if it in a real life settings, with animal models etc.



## 2: Preclinical development
At the begining of this stage we have at least one lead molecule which affect a disease by interacting with target.

Preclinical testing is mainly about **efficacy and safety (toxicity)**.
It includes **in-vitro testing** and **in-vivo** testing on animal models, i.e. usually mices with induced disease-like conditions.

Preclinical testing is mandatory, without it a regulatory authorities (FDA, etc) wont issue a permission to test it on humans.

As a result of the drug discovery stage we have one or several candidate tripplets disease-target-drug and the goal of preclinical testing is to prove that it is effective and safe enough to try it on humans.

So, preclinical testing is mainly about **efficacy and safety (toxicity)**. It includes **in-vitro testing** and **in-vivo** testing on animal models, i.e. usually mices with induced disease-like conditions.

Preclinical testing is mandatory, without it a regulatory authorities (FDA, etc) wont issue a permission to test it on humans.

Consequently, the result of preclinical testing must be filling of **Investigational New Drug (IND)** application.


There are three parts in IND applications: 
- **formulation development** - explaining the best way to prepare a drug in the preclinical phase for its intended clinical use in patients
- **pharmacology** (on animals) - 
  - PK (pharmacokinetics) and ADME (Absorption, Distribution, Metabolism, Excretion).
  - PD (pharmacodynamics) and safety 
- **toxicology** - he toxicology studies aim to look at the effects of longer-term drug exposure on the body, including repeat dose studies.



**Pharmacokinetics (PK)** refers to the study of how a drug moves through the body over time (what the body does to a drug). 

PK is typically divided into four key stages, summarized by the acronym ADME:
- **Absorption**: How the drug enters the bloodstream after administration. Administration might be done as oral, intravenous (injected directly into the bloodstream), or topical (applied to the skin) and absorption heavily depends on this route of administration.
- **Distribution**: This stage determines how much of the drug reaches the target site where it will have its intended effect.
- **Metabolism**: Metabolism typically transforms the drug into more water-soluble compounds that can be more easily excreted from the body. 
- **Excretion**: The process of eliminating the drug from the body, primarily through the kidneys (urine) or the liver (bile/feces). This stage determines how long the drug stays in the body and continues to have an effect.

The usual quantitative outcome of these studies is to define such quantities as concentration-time curve, Cmax (Maximum Concentration): The highest concentration of the drug observed in the blood after administration, Tmax (Time to Maximum Concentration), AUC (Area Under the Curve): Represents the total drug exposure over time;  etc


**Pharmacodynamics (PD)** focuses on understanding the effects of a drug on the body, what drug does to a body. More precisely, it is the relationship between drug concentration and its biological or therapeutic effects. 

It is done by more detailed understanding of the **Mechanism of Action (MoA)**: how the drug interacts with its biological target (e.g., receptors, enzymes). It usually requires revisiting primary target interactions as well as Identification  Off-Targets (additional proteins or receptors the drug interacts with, which could lead to side effects)


In quantitativy terms evaluating **Drug Potency and Efficacy** and Establish the **Effective Dose Range**
means elusidating IC50/EC50 Values (Concentration of the drug required to inhibit or activate 50% of its target - measure of drug potency) and quantitative data on the relationship between drug concentration and the magnitude of its effect, usually as 2D plot.

Once again, the result of Preclinical stage must be Filling Investigational New Drug (IND) application.


# 3: Clinical testing

Any drug development company has to complete  a **Investigational New Drug (IND)** applications based on they Pre-clinical testing and submit it to their local regulatory body (FDA etc) in order to enter clinical trial.

For the UK it is the **Medicines and Healthcare Products Regulatory Agency**,  for USA it is  the **Food and Drug Administration, FDA** and for Europe, it is the **European Medicines Agency (EMA)**.

Clinical trial phase might only be started after IND is approved. Approval depends on the results of pre-clinical testing if they are appealing to FDA.

Clinical phase is usually done in three phases.

**Phase I: testing on healthy people for safety**, the goal is to determine **the highest dose** of a drug that can be safely administered to human without serious side affects. As an outcome the safe dosage range and identifies any potential side effects. This phase is crucial for determining how the drug can be administered safely in later phases.

**Phase II: testing effectiveness in patients with disease**, aim to assess the drug’s efficacy with typically 100-300 patients who have the disease or condition that the drug is intended to treat.

This is the most rigorous trials where single blinded (when pacient does not know if he is taking drug or placebo) or double blinded (when doctor also doe not know it) are applied. 
One of he problem on this stage is to enroll enough patients espesially if a rare disease is tested.

Successful Phase 2 trials show that the drug has a therapeutic effect and justifies further testing in larger populations.

**Phase III: efficasy in large patient population**, The drug is tested in a much larger and more diverse patient population.
Researchers compare the new drug to existing standard treatments or placebos to determine its relative efficacy.

If Phase 3 trials are successful, the data are used to submit a New Drug Application (NDA) or Biologics License Application (BLA) to regulatory agencies. The result of this application is positive, the drug is approved for market and sales begin.

There is also Phase IV which is referred as Launch and Post-Marketing Surveillance. At this stage drug is already on marked and used in Real World Settings (RWS), so some more side-effects might be elusidated and phase 3 is designed to oversee that drug even no this stage.



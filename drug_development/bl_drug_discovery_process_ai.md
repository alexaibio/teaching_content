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
At this stage we we the disease and the target which can affect this disease. 
Now we need to find a 
This stage involves finding chemical compounds (referred to as "hits") that interact with the druggable target identified in the previous step. Hits are molecules that show some degree of binding or biological activity against the target. It might be

a small molecule
- we can find molecule that will bind to the target in-silico (AlphaFold)
- we can do it by HTS, start from compound library (~100 000) and see the effect

a biologic (might be **monoclonal antibodies: mAb or moAb**)
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
    
    


---------------------------------------------------

# Preclinical development
    
после discovery у нас есть хотя бы один lead molecule

preclinical testing is mainly about **efficacy and safety** (toxicity)


    - **in-vitro testing + in-vivo animal models**
    - preclinical - обязательно by regulatory authorities (FDA) - на их основании выдается разрешение на испытание на людях
    - **preclinical включает**
        - **PK - pharmacokinetics** - как оно движется по телу через ADME. Результат - **определение доз** для клиники / контролируется через концентрацию в организме - **что тело делает с лекарством**
        - **PD - pharmacodynamics** - биологический эффект лекарства в зависимости от концентрации / контролируется через выбранный биомаркер - **что лекарство делает с телом**
            - биомаркеры:
                - cardio = cholesterol / myoglobin / creatine kinase (CK)
                - diabetes - adiponectin / hemoglobin A1c
                - cancer - HER2 / ER / PR
        - **Acute toxicity** - выяснить вредный эффект от краткосрочного overdose, done in two mammalian species, effect observer in two weeks. Для ойенки результатов случайной передозировки, yfqnb medial lethal dose LD50 - dose which kills half of the animal - main measure of acute toxicity
        - **Chronic toxicity** - same, up to two years,
        - **Reproductive toxicity and teratogenicity** (возможность повреждать плод во время беременности)
        - **Immunitoxicity** -
        - **carcinogenicity**
        - **bioavalability** - какой процент и скорость с которой API (Active ParmaI Ingredient) достигает места действия. обычно сложно померять концентрацию в нужном органе  - поэтому обычно меряют концентрацию в крови (для внутривенный считают **bioavailability = 100**)
        - **bioequivalence** - изучают различные формы выпуска, способы доставки и тд и то как это влияет на эффективность лекарства

&nbsp;

&nbsp;


-------------------------------------
# **Сlinical development**
    
    - **IND application** (Investigational New Drug application)
        - после pre-clinical наступает время clinical trial - чтобы начать его нужно заполнить IND application - submitted to FDA
        - туда должны входить данные из pre-clinical + production info - как лекарство будет производиться
        - IND is a large milestone in the drug development!
        - in IND should be covered
            - animal pharmacology and toxicology studies - is it reasonable safe to try on human?
            - **manufacturing** information - быть уверенным что компания сможет производить и поставлять необходимое количество лекарств
            - clinical protocol and investigator information - detailed protocol for proposed clinical stadies, информация и квалификация of clinical investigators (врячей котореы будут вести trial)
    - **Clinical Trials**
        - intro
            - лекарство впервые испытывается на людях во время clinical trials - this is a major milestone
            - sponsor - эта та организация которая спонсирует clinical trial
            - sponsor uses **CRO** (Contract Research Organization) которая и будет выполнять clinical trial
            - volunteer are recruited
        - Phase Zero
            - первоначальное понимание как драг действует на тело и как тело реагирует на драг
            - фаза 0 не обязательна
            - введение очень малой дозы в 10-15 добровольцев
                - does the drug reach its intended target?
                - any adverse side effect for sub-therapeutics dose?
                - do cancer cells respond?
            - in general - phase zero helps to mitigate the risk of drug failing during costly clinical trials
        - **Phase 1 - **здоровый пациент****
            - goal - to determine **the highest dose** of a drug that can be safely administered to human without serious side affects
            - method - **dose escalation** - разным группам волонтеров дают все увеличивающуюся дозу пока не появится side effects. есть два варианта этого исследования
                - SAD - Single Ascending Dose studies - дозы повышаются в разных группах
                - MAD - Multiple Ascending dose - дозы повыщаются для каждого члена группы
                - PK / PD характеристики оцениваются и позволяют выяснить dose range
        - **Phase 2 - эффективность ****в больных пациентах****, randomized placebo-controlled study**
            - effectiveness in the target population is assessed
            - то есть если в фазе 1 оценивается яра работа в здоровых пациентах - то в фазе 2  в больных target disease
            - основная проблема - набрать больных пациантов, особенно если речь идет о rare disease
            - phase 2a - find a dose level that has a desired effect of treating the disease
            - phase 2 - this dose level is then used in phase 2b to confirm the efficacy
            - single blinded - когда пациент не знает там плацебо или лекарство
            - double blinded - когда также и доктор не знает
        - **Phase 3** - efficacy in** **large patient population****
            - lasts several years  with >1000 patients in several countries, so multiple test sites are required
            - monitoring for safety, side effects,
            - comparison to other treatments -are there benefits over competitors?
            - id phase 3 demonstrate favorable results the sponsor can begin seeking regulatory approval to launch drug on to the market
            - label expansion - проверка если помогает для других заболеваний тоже - не только для target
    - **Launch (Phase 4) - regulatory submission, approval, launch**
        - submission: pre-clinical and clinical studies, characteristic of drug and its future manufacturing and packaging
            - NDA (new drug application ) - for small molecule drug
            - BLA (biological licensing application) - for biologics
        - Launch - обычно до этой стадии проходит 10 лет и миллиард долларов
            - надо выбрать - pricing, brand name, package design, инструкция
            - robust supply chain, digital marketing campaign
        - Post-launch surveillance
            - **pharmacovigilance** (фармнадзор) - надзор за препаратом после его выпуска в обращение
            - adverse events - сюрпризы после выпуска
            - drug-drug interaction
            - on that stage are also investigated **drug repurposing** and **drug combinations**
- **Others**
    - Generics, Biosimilars and Biosuperiors
        - **generics** - после истечения 20 лет, но 20 лает начинаются не с launch but from clinically?
        - small molecules очень легко скопировать в отличие от biologics - почти невозможно создать точную копию - и они навоюются biosimilars
        - **biosimilars** - должны проходить дополнительный clinical testing - чтобы доказать что они работают
        - **biosuperiors** - иногда biosimilars работают лучше чем оригинальное лекарство - тогда их назвают biosuperiors - их тоже надо тестировать клиники перед запуском
- **CMC - ****chemistry, manufacturing and control**
    - **characterization - **определить методы оценки affinity for its target, purity, osmolarity etc
    - stability - тестинг для определения срока годности, взаимодействия с упаковкой, также стабильность при разной температуре чтобы определить условия хранения (frozen, refrigerated, room temperature)
    - Formulation - определение других веществ которые добавляются кроме active drug - для улучшения стабильности и safety.



# AI in clinical
- de-risk and accelerate clinical trials

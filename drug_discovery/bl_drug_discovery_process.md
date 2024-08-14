



-------------
# **Intro**

- small molecule - drugs - sythetised, pharmaceutical companies (синтезируются)
- large molecule biologics - вырачиваются в живых клетках - biotechnology companies



# **Drug Dev Cycle**

- ## **Discovery**
    
    - **target discovery/identification**
        
        - выбрать болезнь, look for biological **targets associated with it** (protein в организме или микробе) understand pathways
        - common targets: **enzymes**, **cell surface receptors**, intra-cellular receptors, ligand-gated ion channels, voltage gated ion channels, gene transcription factor
        - альтернативный подход - через фенотип - то есть делать скрининг лекарств на cell line or SmartCube - на поведении
        - Candidate targets may be selected based on a variety of experimental criteria. These criteria may include
          - [disease linkage](https://en.wikipedia.org/wiki/Disease_gene_identification) (mutations in the protein are known to cause a disease),
          - mechanistic rationale (for example, the protein is part of a regulatory pathway that is involved in the disease process), or
          - [genetic screens](https://en.wikipedia.org/wiki/Genetic_screen) in [model organisms](https://en.wikipedia.org/wiki/Model_organism).
          - COA - co-expression analysis?????

If a drug has already been identified for a target, that target is by definition druggable. If no known drugs bind to a target, then druggability is implied or predicted using different methods that rely on evolutionary relationships, 3D-structural properties or other descriptors
    - **target validation**
        
        - демонстрировать что этот target работает
            - литература,
            - in-silico (например смоделировать binding targets and their ligands)
            - gene editing - что случиться если ген** knock down** (уменьшить его активность) or **knock-out** (выключить совсем) / можно также сделать overexposes - для провокации
            - через Proteomics - подстраиваем активность белка а не гена - create **antibodies** directed **against target protein**
            - biomarkers - вещества или характеристики которые можно измерить / можно мерить их реакцию при воздействии на target
    - **hit identification - bind to the target**
        
        - теперь у нас есть место от которого зависит болезнь и нам надо найти hit - то чем можно это вылечить. Это может быть -
        - small molecule drugs
            - **find molecule that will bind to the target**
            - start from compound library (~100 000) - физические баночки - используются роботы
            - HTS - high throughput screening
            - compounds that demonstrate the intended activity - **hits**, hence hit identification
        - for biologics
            - manufactured by living systems like microorganisms or plant/animal cells
            - another class of biologics - **monoclonal antibodies ( ****mAb**** or ****moAb ****)** therapeutics generated using hybridoma technology
                - [Monoclonal](https://en.wikipedia.org/wiki/Monoclonal) antibodies can have monovalent affinity, binding only to the same [epitope](https://en.wikipedia.org/wiki/Epitope) (the part of an [antigen](https://en.wikipedia.org/wiki/Antigen) that is recognized by the antibody). In contrast, [polyclonal antibodies](https://en.wikipedia.org/wiki/Polyclonal_antibodies) bind to multiple epitopes and are usually made by several different antibody-secreting [plasma cell](https://en.wikipedia.org/wiki/Plasma_cell) lineages. [Bispecific monoclonal antibodies](https://en.wikipedia.org/wiki/Bispecific_monoclonal_antibodies) can also be engineered, by increasing the therapeutic targets of one monoclonal antibody to two epitopes.
    - **lead generation** - доказать что - bind and have the **desired biological effect**
        
        - evaluate **structural properties (QSAR?)**
            - indication of of bio-activity by demonstrate binding to a target
            - drug has structural properties позволяющие потом химикам улучшить свойства и potency
            - оценка свойств влияющих на bioavailability (процент который всасывается в кровь) - гидрофобность и полярность
            - presence of toxic groups
            - reversible/irreversible nature of interaction with the target (например снотворное(реверсибле) или антимикробный препарат)
        - **ADME** / **PK** - absorption, distribution, metabolism, excretion  / pharmakokinetics
            - conduct ADME/PK studies - другой способ identify lead molecules
                
            - то есть drug с наилучшим profile имеют лучший шанс добежать до конца
                
            - обычно эти исследования проводятся позже - но иногда можно и сейчас
                
            
    - **lead optimization**
        
        - прежде чем идти дальше нужно проверить на основные свойства которые могут сделать невозможным использование драга
        - это - solubility, efficacy, safety
        - lead molecule не всегда имеет эти свойства - но через lead optimization мы можем их добавить или найти другой вариант этого драга - обладающий нужными свойствами

&nbsp;

- ## **Preclinical development**
    
    - после discovery у нас есть хотя бы один lead molecule
    - preclinical testing is mainly about **efficacy and safety** (toxicity)
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

- ## **Сlinical development**
    
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

**дополнительно**

- **regulations**
    - GLP -
# PICOElementMapProject
## File descriptions
### Folders:
* Pickles: contains all pickle files, including counters and adjacency lists

### .ipynb
* Litcovid Data Processor.ipynb: processes parsed json files and stores in pickle files + csvs 
* Treatment PMIDS.ipynb: gets csv of treatment pmids
* Meeting demo: random stuff demonstrated at meetings

### .pickle:
* p/i/o_count.pickle: counter object
* edges.pickle: 

### .csv
* treatment_pmids.csv: all pmids labelled as treatment
* Litcovid_treatment_ents.csv: all entities


## Meeting notes

### Meeting 10/15
* parse sent-classification output and match subsection titles to json
* build synonym sets to group PICO elements
* look at graph output
* consider studies with same outcome (e.g. ICU admission) and consider separate entities
* statistical tests: chi square independence/homogeneity tests
* add meeting notes to github

### Meeting 10/22
* Preferred outcomes: mechanical ventilation, in-hospital mortality, tracheostomy, severe/severity/severity of covid-19
* concept mapping across general entity body
* manually define rules to compare/group element
* synonym set
* select a category with specific outcome; then compare relevant publications
* consider separators/descriptors of population (e.g. age)
* features include ranks, labels etc.
* similarity score between articles
    * treat PICO elements as tags
    * review granularity of tags vs. using as is; ensure lack of redundancies
    * tags requiring more context: age, severe, etc.
    * **confidence/ambiguity score**: sample to estimate score, assigning meaning/threshold to tag
    
    
#### TODO: 

*Jane:*
* **filter articles considering these preferred outcomes only**
* DONE: **get pickle files for Hao**
* DONE: **assign 10% of samples to everybody for severe only; each person gets a CSV file for**
    * assign 10% sample with ambiguous tags to develop heuristic to classify or derive confidence/ambiguity scores
* DONE: assigning proper subsection titles to json and re-run tian's parser
* DONE: **send PMID list to Fengyang**
* DONE: new functionalities:
    * group PMID's by given set of entities
    * get original sentence text easily
* DISCUSS: similarity score between articles
    * check ambiguous/context-less tags and deriving confidence/ambiguity scores
    * tag hierarchy
* fix synonym checker to merge similar tags
* manually investigate preferred outcomes, treatments

*Fengyang:*
* **get PMID filters for Jane!!**
* literature review for PICO multi-tagging system
* build framework for chi-square
    * Jane will provide a list of PMIDs for: 
* look at sample with ambiguous tags (e.g. "severe", "age", "aged") to develop heuristic to classify or derive confidence/ambiguity scores

*Hao:*
* use pickle files to improve synonym sets
* look at sample with ambiguous tags (e.g. "severe", "age", "aged") to develop heuristic to classify or derive confidence/ambiguity scores

### Meeting 10/28
* Summary
    * Discussed "severe multitagging"
    * Developed rule of thumb heuristics to identify "severe"
    * Showed new implementations/tools from Jane
    * Discussed limitations of chi-squared test and future action plans for Fengyang
    * Discussed direction of literature review for Fengyang
    * Created deliverables plan
* "Severe" identification heuristics
    * "Severe disease" goes in both
    * Drop "severe" tags not properly categorized
    * Rule of thumb: terms immediately following vs. closest term
 
* "Severe" subtag hierarchy
     * Cases of COVID-19: infections, severe disease, outcomes
     * Other diseases: pneumonia, severe disease
         * Complications
         * Events
     * Symptoms: severe acute respiratory failure, ARDS, acidosis, hypercoagulability
         * Syndrome
         * SARS
     * Course
     * Adverse effect
 * Develop multitagging system for ALL entities?
 * Suggestions from Dr. Weng:
     * same intervention/population -> different outcomes, etc.
     * categorize segments by intervention/population
     * independence amongst categories
     * what are treatments with same outcome
 * Ambiguous: critical

#### TODO: 

*Jane:*
* Severe tagger
* **Send aged/age, critical split**
* Fix section header thing
* **classify age/aged**
* DISCUSS: similarity score between articles
    * check ambiguous/context-less tags and deriving confidence/ambiguity scores
    * tag hierarchy
* fix synonym checker to merge similar tags
* manually investigate preferred outcomes, treatments

*Fengyang:*
* **classify age/aged, critical**
* literature review for PICO multi-tagging system:
    * Google Scholar, PubMed
    * Non-medical and medical tagging system
* TMR: run test for chi-square
    * build framework for chi-square


*Hao:*
* use pickle files to improve synonym sets
* Find heuristic for splitting sentence in BioBert
* **classify age/aged, critical**

### Meeting 11/4
* age:
    * subtag
        * median/mean age
        * age number/range
            * try to get range
        * age concept
    * get values (70+%)
        * filter by age particle
        * rules of thumb 
    * group articles into age group: "pediatric" (<18), "adult", "elderly" (65+)
        
* critical:
    * drop anything not critical illness
    * when searching, critical and severe should be bundled together
* embedding doc into vector space:
    * Doc2Vec
#### TODO: 

*Jane:*
* Severe tagger
* Fix section header thing
* DISCUSS: similarity score between articles
    * check ambiguous/context-less tags and deriving confidence/ambiguity scores
    * weighting system with frequency of subtags
    * tag hierarchy
* fix synonym checker to merge similar tags

*Fengyang:*
* excel sheet for literature review for PICO multi-tagging system:
* run test for chi-square using different values instead of frequency counts
    * comparing distributions of entity counts per article
*    


### Meeting 11/11
* Manually look at Dr. Weng's suggested outcome, comparing conclusions on a corpus-level
* Chat with Dr. Weng:
    * Summarize what we've been doing
    * Suggestions for subtags, further steps
* For same PMID, create document with only sentences containing outcome
    * Use Doc2Vec and compare via cosine similarity
    * In one group, for the same tag, combine all sentences across PMIDs
* Potential directions:
    * Textual entailment
    * Multi-document summarization
    
#### TODO: 

*Jane:*
* Augment severe tagger
* Fix section header thing
* Fix age tagger
* Look for coverage metrics (e.g. P@10, MAP, etc.)
* fix synonym checker to merge similar tags


*Fengyang:*
* literature review on whatever topics Dr. Weng suggests


### Meeting 11/18
* First fix participants, among those we can select drug, then we can consider 
* Outcomes: **mechanical ventilation, in-hospital mortality, severe/severity/severity of covid-19**, **tracheostomy**, 
* Interventions: **hydroxychloroquine, remdesivir, tocilizumab**, azithromycin, **convalescent plasma**, corticosteroid
* Participants: hypertension, severe, diabetes, elderly, female, pediatric, mechanical ventilation
* Grouping:
    * Children/adult/elderly
    * Medical conditions: hypertension, severe, diabetes,
    * Gender
* Similarity value:
    * Vector for each of the three types, both binary and count
* Clustering???
* Checking for:
    * Population representativeness
    * Negations
    * Contradiction, etc.
    * 20-30 articles each or so
    
#### TODO: 

*Jane:*
* Augment severe tagger
* Fix section header thing
* Fix age tagger
    * Can crossover
* Look for coverage metrics (e.g. P@10, MAP, etc.)
* fix synonym checker to merge similar tags


*Fengyang:*
* literature review on whatever topics Dr. Weng suggests

### Meeting 11/25
* Fengyang: "severe" -- focused on the tie between severe Covid and the old SARS virus
* Fix outcome/intervention: compare distribution of age group + characteristics 
* Fix outcome: compare interventions
* Clustering:
    * Consider general trend of overlapping population tags within a certain cluster??
    * 

*Jane:*
* Generate group of studies for Marguerite

*Fengyang:*
* Fix outcome/intervention: compare distribution of age group + characteristics (or vice versa)

*Hao:*
* Review group of studies

*Marguerite:*
* Review group of studies: tracheostomy


### Meeting 11/25


*Jane:*
* Pagerank
* Get 50 studies with adult/elderly, adult, and elderly, HCQ, in-shopistal mortality
* Get 50 studies with diabetes, HCQ, in-hospital mortality
* Get 50 studies with pregnancy, HCQ, in-hospital mortality

*Fengyang:*
* Get 50 studies with adult/elderly, adult, and elderly, HCQ, in-hospital mortality

*Hao:*
* Get 50 studies with diabetes, HCQ, in-hospital mortality
* Get 50 studies with pregnancy, HCQ, in-hospital mortality

*Marguerite:*
* Literature review: what are the questions and processes followed by other literature reviews assessing the body of Covid studies? What scope are they working


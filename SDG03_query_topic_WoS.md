# Search query for SDG 3 - Good health and well-being, Bergen topic-approach.

Ensure healthy lives and promote well-being for all at all ages.

**Current status**: This string is currently a finished version (1.0.0).

**Contents**

1. Full query in copy-pasteable format
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/1f8d927b-dd74-4fe9-9a7b-624b508ad821-57b51d0d/relevance/1 (no filters; all years)

## 2. General notes

This document contains search strings for finding publications related to the topics in SDG 3 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in SDG 3 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f22)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

During editing of this string (2021), we have consulted two other sets of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f29)</a> and <a id="Els">[Rivest et al. (2021)](#f30)</a>.

**Abbreviations**
* WHO - World Health Organization
* MeSH - Medical Subject Headings - https://www.ncbi.nlm.nih.gov/mesh/

## 3. Targets

### Target 3.1

> **3.1 By 2030, reduce the global maternal mortality ratio to less than 70 per 100,000 live births.**
>
> 3.1.1 Maternal mortality ratio
>
> 3.1.2 Proportion of births attended by skilled health personnel

The target is interpreted as covering research about the maternal mortality rate. The interpretation is limited to mortality, rather than care/health generally -  attendance of skilled health personnel is interpreted as one way to limit mortality, and should be covered if authors connect their work to this aim.

This query consists of 1 phrase.

#### Phrase 1

The elements of the phrase are: *mothers/birth* + *mortality* + *excluding livestock*. Originally, a second phrase was added for "survival", but this mostly added noise - many results were about babies rather than mothers, and others were about "maternal" effects in animals.

Some of the *mothers/birth* terms may find results concerning newborn mortality, this is difficult to avoid and may lead to some overlap with 3.2. Many works also talk about both maternal and neonatal mortality together. As both are in the same SDG this should not be an issue for SDG sets.

A double `NOT` expression is included to help remove results referring to mortality of livestock, but retain those referring to these animals as models for humans. Rats and mice are not in the `NOT` statement as these are usually animal models for humans.

```py
TS=
(
  (   
    ("pregnan*" OR "post partum" OR "postpartum" OR "peripartum" OR "obstetric$"
    OR "childbirth" OR "child-birth" OR "birth" OR "births"
    OR "premature deliver*" OR "preterm deliver*" OR "preterm labor" OR "preterm labour"
    OR "maternal" OR "mothers"
    )
    NEAR/15
        ("mortality" OR "death$")
  )
  NOT (("pigs" OR "cows" OR "sheep" OR "cattle" OR "poultry") NOT ("human" OR "model"))    
)
```

### Target 3.2

> **3.2 By 2030, end preventable deaths of newborns and children under 5 years of age, with all countries aiming to reduce neonatal mortality to at least as low as 12 per 1,000 live births and under‑5 mortality to at least as low as 25 per 1,000 live births**
>
> 3.2.1 Under‑5 mortality rate
>
> 3.2.2 Neonatal mortality rate

This target is interpreted to cover research about mortality for young children and newborns. Children "under five" is however extremely difficult to limit via terms since it is often referred to as childhood mortality - thus we include terms for children and infants generally.

This query consists of 2 phrases.

#### Phrase 1

The elements of the phrase are: *children/babies* + *mortality* + *excluding livestock*. `preterm` and `premature` are not used, as they generally (when used without reference to births/newborns) refer to "premature death".

```py
TS=
(
  (   
    ("child*" OR "infant$" OR "toddler$" OR "under-five$"
    OR "baby" OR "babies" OR "newborn$" OR "neonatal" OR "neonate$"
    OR "perinatal" OR "prenatal" OR "antenatal"
    )
    NEAR/15
        ("mortality" OR "death$" OR "stillbirth$" OR "still-birth$")
  )
  NOT (("pigs" OR "cows" OR "sheep" OR "cattle" OR "poultry") NOT ("human" OR "model"))    
)
```

#### Phrase 2

Phrase 2 finds publications using the opposite terminology of phrase 1 (i.e. mortality = survival). The elements of the phrase are: *children/babies* + *survival* +  *excluding livestock*. The term "survivor" is a bit tricky, as it is used about reducing mortality (e.g. "cancer survivors") but also in the context of abuse ("child abuse survivor"). Thus results around this topic may also be included; we did not consider them far enough from the interpretation to warrant using a NOT search that could potentially lose relevant results.

```py
TS=
(
  (   
    ("child*" OR "infant$" OR "toddler$" OR "under-five$"
    OR "baby" OR "babies" OR "newborn$" OR "neonatal" OR "neonate$"
    OR "perinatal" OR "prenatal" OR "antenatal"
    )
    NEAR/15
      ("surviv*")
  )
  NOT (("pigs" OR "porcine" OR "cows" OR "sheep" OR "cattle" OR "poultry" OR "newborn cell") NOT ("human" OR "model"))   
)
```


### Target 3.3

> **3.3 By 2030, end the epidemics of AIDS, tuberculosis, malaria and neglected tropical diseases and combat hepatitis, water-borne diseases and other communicable diseases.**
>
> 3.3.1 Number of new HIV infections per 1,000 uninfected population, by sex, age and key populations
>
> 3.3.2 Tuberculosis incidence per 100,000 population
>
> 3.3.3 Malaria incidence per 1,000 population
>
> 3.3.4 Hepatitis B incidence per 100,000 population
>
> 3.3.5 Number of people requiring interventions against neglected tropical diseases

This target could be interpreted two ways in the topic approach:
1. It covers research about the combating and ending of communicable and waterborne diseases
2. It covers all research about communicable and waterborne diseases
For the moment, we are using interpretation (1). Thus we interpret "ending epidemics", to include research on epidemics/pandemics, along with general works about transmission, prevalence, and risks.  We interpret "combating" to mean reducing occurrence and effects of these diseases, thus covering research about control, transmission, prevention, treatment, medicines, vaccines etc. 

This query consists of 3 phrases.

#### Phrase 1

This covers communicable diseases as a category. The elements of the phrase are: *communicable diseases + combating/epidemics/interventions*. The search terms here are difficult, as `communicable` will also find `non communicable`, thus this term is covered in its own phrase where a double `NOT` expression is used to remove publications mentioning non-communciable disease without also mentioning infectious, communicable and tropical diseases ("non communicable" seems to be the term causing the most problems; others, such as `non-infectious` seem to be used in papers about both, i.e. together with `infectious` - these are covered in phrase 2). This cuts the results for the last 5 years by about 75 %, compared to allowing "non-communicable" to be found.

```py
TS =
(
  (
    ("communicable disease$" OR "communicable illness*")
    NEAR/15
        ("prevent$" OR "preventing" OR "prevention" OR "prevented" OR "combat*" OR "fight*" OR "tackl*" OR "reduc*" OR "alleviat*" OR "mitigat*"
        OR "eradicat*" OR "eliminat*" OR "end" OR "ended" OR "ending"
        OR "treat" OR "cure" OR "cured" OR "vaccinate" OR "control"
        OR "epidemic$" OR "pandemic$" OR "outbreak$" OR "spread" OR "transmission" OR "occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"
        OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "treatment$" OR "intervention$" OR "therap*"
        )
  )
  NOT ("non communicable" NOT ("infectious disease$" OR "tropical disease$" OR "non communicable and communicable" OR "communicable and non communicable"))
)
``` 

#### Phrase 2

The elements of the phrase are: *communicable diseases + prevention/treatment*. In this phrase, specific diseases and groups of diseases are covered. The*disease* terms are the same as in phrase 3.

In the *communicable disease* terms, specific diseases were added from sources outlined below, plus a WHOs factsheet on leading causes of death in 2019 (<a id="WHOFStop10">[WHO, 2020c](#f23)</a>).
- The first section covers communicable and waterborne diseases as a category (see also Phrase 1).
- The second section covers specific communicable & vaccine-preventable diseases. `hepatitis`, `tuberculosis`, `HIV`, `malaria` are taken directly from the target. The term `aids` is combined with `prevent aids` as it is used as a verb. We then used WHO Global Health Observatory data for adding specific communicable (<a id="WHOGHO">[WHO, n.d. a](#f2)</a>) and vaccine-preventable diseases (<a id="WHOGHOb">[WHO, n.d. b](#f2a)</a>). Here, they are listed according to SDG target; those under target 3.3. were included. This also included the category sexually transmitted infections. Diseases were also added from a WHO list of epidemic and pandemic-prone diseases (<a id="WHOepipan">[Regional Office for the Eastern Mediterranean, n.d.](#f24)</a>). `SARS` covers also "SARS-CoV-2" (covid-19).
- The third section is for waterborne diseases. A definitive list of prioritised "waterborne diseases" was not found and the MeSH term has no specific diseases; as a way to improve the query, we have used 11 diseases/pathogens prioritised by the U.S. Centers for Disease Control and Prevention, Waterborne Diseases Prevention Branch (<a id="CDCwaterborne">[Centers for Disease Control and Prevention, 2021](#f13)</a>).
- The fourth section lists neglected tropical diseases, as mentioned in the target. The 20 diseases/disease groups currently prioritised by WHO in their 2021-2030 roadmap are included (p. 2, <a id="WHONTD">[WHO, 2020a](#f3)</a>).

A number of these diseases also occur in animals (e.g. Feline/Simian Acquired Immunodeficiency Syndrome, Canine hepatitis, Avian malaria, Bovine tuberculosis). We do not attempt to exclude them, as it is considered that work on them can inform human prevention/treatment, or prevent zoonotic transmission. `prevent*` is not used to reduce results generally talking about "preventable deaths", rather than prevention.


```py
TS =
(
  (
    (
      ("water borne" OR "waterborne" OR "water-borne" OR "water-related" OR "diarrhoea*" OR "diarrhea*"
      OR "contagious" OR "transmissible" OR "infectious"
      )
      NEAR/5
          ("disease$" OR "infection$" OR "epidemic$" OR "illness*")
    )
    OR "hepatitis"
    OR "acquired immune deficiency syndrome" OR "acquired immuno-deficiency syndrome"  OR "acquired immunodeficiency syndrome" OR "Human Immunodeficiency Virus" OR "HIV" OR "prevent aids"
    OR "tuberculosis"
    OR "malaria"
    OR "cholera"
    OR "meningitis"
    OR "influenza" OR "avian influenza" OR "H5N1"
    OR "rubella"
    OR "diphtheria"
    OR "japanese encephalitis"
    OR "measles"
    OR "mumps"
    OR "tetanus"
    OR "pertussis"
    OR "polio*"
    OR "yellow fever"
    OR "sexually transmitted disease$" OR "sexually transmitted infection$"
    OR "syphilis"
    OR "lower respiratory infection$"
    OR "coronavirus" OR "covid" OR "covid19" OR "middle east respiratory syndrome" OR "MERS" OR "severe acute respiratory syndrome" OR "SARS"
    OR "crimean-congo haemorrhagic fever" OR "viral haemorrhagic fever$"
    OR "ebola"
    OR "plague"
    OR "rift valley fever"
    OR "zika virus"

    OR "amebiasis"
    OR "cryptosporidiosis" OR "cryptosporidium infection$"
    OR "giardiasis" OR "giardia infection$"
    OR "shigellosis"
    OR "cronobacter infection$"
    OR "acanthamoeba"
    OR "balamuthia"
    OR "naegleria"
    OR "sappinia"
    OR "typhoid"

    OR "neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthias*" OR "hookworm$" OR "roundworm$" OR "whipworm$" OR "Ascaris lumbricoides" OR "Trichuris trichiura" OR "Necator americanus" OR "Ancylostoma duodenale"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
  )
  NEAR/5
      ("prevent$" OR "preventing" OR "prevention" OR "prevented" OR "combat*" OR "fight*" OR "tackl*" OR "reduc*" OR "alleviat*" OR "mitigat*"
      OR "eradicat*" OR "eliminat*" OR "end" OR "ended" OR "ending"
      OR "treat" OR "cure" OR "cured" OR "vaccinate" OR "control"
      )
)

```   

#### Phrase 3

The general structure is *communicable diseases + epidemics/interventions*. This phrase uses the same disease terms as phrase 2, but is separated because the *epidemic/intervention* can be combined with `AND` rather than needing `NEAR`.

```py
TS =
(
  (
    (
      ("water borne" OR "waterborne" OR "water-borne" OR "water-related" OR "diarrhoea*" OR "diarrhea*"
      OR "contagious" OR "transmissible" OR "infectious"
      )
      NEAR/5
          ("disease$" OR "infection$" OR "epidemic$" OR "illness*")
    )
    OR "hepatitis"
    OR "acquired immune deficiency syndrome" OR "acquired immuno-deficiency syndrome"  OR "acquired immunodeficiency syndrome" OR "Human Immunodeficiency Virus" OR "HIV" OR "prevent aids"
    OR "tuberculosis"
    OR "malaria"
    OR "cholera"
    OR "meningitis"
    OR "influenza" OR "avian influenza" OR "H5N1"
    OR "rubella"
    OR "diphtheria"
    OR "japanese encephalitis"
    OR "measles"
    OR "mumps"
    OR "tetanus"
    OR "pertussis"
    OR "polio*"
    OR "yellow fever"
    OR "sexually transmitted disease$" OR "sexually transmitted infection$"
    OR "syphilis"
    OR "lower respiratory infection$"
    OR "coronavirus" OR "covid" OR "covid19" OR "middle east respiratory syndrome" OR "MERS" OR "severe acute respiratory syndrome" OR "SARS"
    OR "crimean-congo haemorrhagic fever" OR "viral haemorrhagic fever$"
    OR "ebola"
    OR "plague"
    OR "rift valley fever"
    OR "zika virus"

    OR "amebiasis"
    OR "cryptosporidiosis" OR "cryptosporidium infection$"
    OR "giardiasis" OR "giardia infection$"
    OR "shigellosis"
    OR "cronobacter infection$"
    OR "acanthamoeba"
    OR "balamuthia"
    OR "naegleria"
    OR "sappinia"
    OR "typhoid"

    OR "neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthias*" OR "hookworm$" OR "roundworm$" OR "whipworm$" OR "Ascaris lumbricoides" OR "Trichuris trichiura" OR "Necator americanus" OR "Ancylostoma duodenale"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
  )
  AND
      ("epidemic$" OR "pandemic$" OR "outbreak$" OR "spread" OR "transmission" OR "occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"
      OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "cure" OR "treatment$" OR "drug$" OR "intervention$" OR "therap*"
      OR "antimalarial$" OR "antiviral$" OR "antibiotic$" OR "antiparasitic$" OR "antihelminthic$" OR "antihelmintic$"
      )
)

``` 

### Target 3.4

> **3.4 By 2030, reduce by one third premature mortality from non-communicable diseases through prevention and treatment and promote mental health and well-being.**
>
> 3.4.1 Mortality rate attributed to cardiovascular disease, cancer, diabetes or chronic respiratory disease
>
> 3.4.2 Suicide mortality rate

This target is interpreted to cover research about mortality from non-communicable diseases. In contrast to 3.3, here there is an explicit focus on mortality in the target, indicators and the High-level Political Forum thematic review for SDG 3 (<a id="HLPF">[ECESA plus members, 2017](#f21)</a>). We interpret it also to cover research about treatment for mental health disorders and promotion and services for well-being.

This query consists of 3 phrases.
* Phrase 1 focuses on the "non-communicable diseases" part.
* Phrases 2 and 3 focus on the "promote mental health and well-being" part.

#### Phrase 1

The elements of the phrase are: *non-communicable diseases + mortality*. We added diseases from the WHO factsheet on non-communicable diseases (<a id="WHOFSnoncomm">[WHO, 2018](#f4)</a>) and a WHO factsheet on leading causes of death in 2019 (<a id="WHOFStop10">[WHO, 2020c](#f23)</a>). Cancer terms were based on "The Cancer Dictionary" in the WHO Cancer Mortality Database (<a id="WHOcancer">[International Agency for Research on Cancer, 2019](#f5)</a>) and using nomenclature as explained by the U.S. National Cancer Institute SEER training modules (<a id="NIHcancer">[National Cancer Institute, n.d.](#f6)</a>).

```py
TS=
(
  (
    (
      ("non communicable" OR "noncommunicable" OR "non transmissible" OR "non infectious" OR "noninfectious")
      NEAR/5
          ("disease$" OR "illness*")
    )
    OR "cardiovascular disease$" OR "heart disease" OR "heart attack$" OR "stroke$"
    OR "diabetes"
    OR "chronic respiratory disease$" OR "asthma"  OR "emphysema" OR "chronic obstructive pulmonary disease$" OR "COPD" OR "chronic obstructive airway disease$" OR "chronic bronchitis"
    OR (("chronic") NEAR/3 ("lung" OR "pulmonary"))
    OR "cancer$" OR "*sarcoma" OR "sarcoma$" OR "*carcinoma" OR "carcinoma$" OR "*blastoma" OR "blastoma$" OR "myeloma$" OR "lymphoma$" OR "leukaemia" OR "leukemia" OR "mesothelioma$" OR "melanoma$"  
    OR (("malignant" OR "incurable") NEAR/3 ("neoplasm$" OR "tumour$" OR "tumor$"))
    OR "kidney disease$"
    OR "alzheimer*" OR "dementia"
    OR "cirrhosis"
  )
  NEAR/15
      ("mortality" OR "death$" OR "surviv*")
)

```  

#### Phrase 2

This phrase focuses on the prevention and treatment of non-communicable mental illnesses/diseases. The elements of the phrase are: *disease + prevention/treatment*.

Generic categories and specific conditions are included. `suicid*` was mentioned specifically in the indicators. We used WHO factsheets to add types of mental disorders (<a id="WHOFSmental">[WHO, 2019a](#f7)</a>). As the focus this phrase is illness, we did not include developmental disorders.

```py
TS=
(
  ("mental health disorder$" OR "mental illness*"
  OR "suicid*"
  OR "depression" OR "depressive disorder$"
  OR "bipolar affective disorder"
  OR "schizophrenia"
  OR "psychosis" OR "psychoses"
  )
  NEAR/15
      ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "alleviat*" OR "eradicat*" OR "eliminat*" OR "tackl*"
      OR "treat" OR "cure" OR "cured"
      OR "epidemic$" OR "occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"
      OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "cure" OR "treatment$" OR "drug$" OR "intervention$" OR "therap*"
      OR "outreach" OR "services" OR "support" OR "counseling" OR "counselling"
      )
)
```

#### Phrase 3

This phrase focuses on the promotion of and services for well-being. The elements of the phrase are: *well-being + promotion/services*.

`wellbeing` is used alone, rather than qualified with "mental" - well-being seems to be used to convey a sense of overall health, which should include the mental/psychosocial aspect. `quality of life` was tested, but this adds a lot of results which seem to be more medical (i.e.  quality of life could be improved after intervention x for condition y).

```py
TS=
(
  ("mental health" OR "well being" OR "wellbeing")
  NEAR/15
      ("promot*" OR "strengthen*" OR "improv*" OR "enhanc*"
      OR (("reduc*" OR "decreas*") NEAR/5 "problem$")
      OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "cure" OR "treatment$" OR "drug$" OR "intervention$" OR "therap*"
      OR "outreach" OR "services" OR "support" OR "counseling" OR "counselling"
      )  
)
```  

### Target 3.5

> **3.5 Strengthen the prevention and treatment of substance abuse, including narcotic drug abuse and harmful use of alcohol.**
>
> 3.5.1 Coverage of treatment interventions (pharmacological, psychosocial and rehabilitation and aftercare services) for substance use disorders
>
> 3.5.2 Alcohol per capita consumption (aged 15 years and older) within a calendar year in litres of pure alcohol

This target was interpreted to include research about the prevention and treatment of harmful uses of alcohol and drugs. It does not cover all use of alcohol/drugs. We also interpret this to be mainly limited to works about use, rather than e.g. controlling supply of illicit drugs.

This query consists of 1 phrase. The elements of the phrase are: *(harmful use + prevention/treating) OR (harmful use + treatment)*.  A wider NEAR distance is used compared to the action approach.

Terms were added from the National Institutes of Health "Commonly Used Drugs Charts" (although this is a USA-centric source we assume it will cover many types; <a id="NIHdrugs">[National Institute on Drug Abuse, 2020](#f14)</a>). Drug/substances were also expanded using MeSH terms:
* Under "opioid-related disorders" (D000079524), `heroin`, `morphine`, `opiate` and `opium` are listed.
* Under "substance-related disorders" (D019966), a number of specific substances are listed, including `amphetamine`, `cocaine`, `inhalent`, `tobacco` etc.

`addiction` and `dependence` were considered as terms that can indicate harmful use. A number of drugs are combined with these terms because either a) they can be used in non-abuse contexts as treatments, or b) there is a lot of research about their effects (e.g. "cocaine can reduce the heart's...").

`therapy OR therapies` rather than `therap*` was used to prevent results regarding the therapeutic uses of these drugs/substances. The broad term `services` is used due to the variety of services involved (social, specialist, alcoholism, treatment, residential...). `treatment$` should cover not only treatment, but also treatment centres. `prevent*` is not used to reduce results generally talking about "preventable deaths", rather than prevention.

```py
TS=
(
  ("binge drinking" OR "binge drinker$" OR "alcoholism" OR "excessive drinking" OR "problematic drinking"
  OR "substance use" OR "illicit drug$" OR "people who inject drugs" OR "PWID"
  OR "opioid epidemic"
  OR
    (
      ("drug$" OR "narcotic$" OR "narcotic$" OR "substance"
      OR "alcohol"
      OR "amphetamine$" OR "methamphetamine$" OR "MDMA" OR "ecstasy"
      OR "cocaine"
      OR "inhalant$" OR "amyl nitrite"
      OR "marijuana" OR "cannabis"
      OR "opioid$" OR "opiate$" OR "heroin" OR "morphine"
      OR "phencyclidine" OR "LSD" OR "psilocybin" OR "dimethyltriptamine"
      OR "khat"
      OR "tobacco"
      )
      NEAR/15
          ("abuse" OR "misuse" OR "dependence" OR "addict*" OR "overdose$"
          OR
            (
              ("use" OR "uses" OR "usage" OR "consumption")
              NEAR/3 ("harmful" OR "problematic" OR "excessive" OR "disorder$")    
            )
          )
    )
  )
  NEAR/5
      ("prevent$" OR "preventing" OR "prevention" OR "prevented" OR "combat*" OR "tackl*" OR "fight* against"
      OR "reduc*" OR "decreas*" OR "minimi*" OR "limit" OR "limiting" OR "alleviat*" OR "mitigat*"
      OR "eradicat*" OR "eliminat*" OR "end" OR "ended" OR "ending" OR "stop" OR "stopped" OR "stopping"
      OR "treat" OR "cure" OR "cured" OR "control"
      )
)
OR
TS=
(
  ("binge drinking" OR "binge drinker$" OR "alcoholism" OR "excessive drinking" OR "problematic drinking"
  OR "substance use" OR "illicit drug$" OR "people who inject drugs" OR "PWID"
  OR "opioid epidemic"
  OR
    (
      ("drug$" OR "narcotic$" OR "narcotic$" OR "substance"
      OR "alcohol"
      OR "amphetamine$" OR "methamphetamine$" OR "MDMA" OR "ecstasy"
      OR "cocaine"
      OR "inhalant$" OR "amyl nitrite"
      OR "marijuana" OR "cannabis"
      OR "opioid$" OR "opiate$" OR "heroin" OR "morphine"
      OR "phencyclidine" OR "LSD" OR "psilocybin" OR "dimethyltriptamine"
      OR "khat"
      OR "tobacco"
      )
      NEAR/15
          ("abuse" OR "misuse" OR "dependence" OR "addict*" OR "overdose$"
          OR
            (
              ("use" OR "uses" OR "usage" OR "consumption")
              NEAR/3 ("harmful" OR "problematic" OR "excessive" OR "disorder$")    
            )
          )
    )
  )
  NEAR/15
      ("medicine$" OR "cures" OR "cure" OR "treatment$" OR "intervention$" OR "therapy" OR "therapies"
      OR "outreach" OR "services" OR "support" OR "rehabilitat*" OR "aftercare" OR "counseling" OR "counselling"
      )
)
```

### Target 3.6

> **3.6 By 2020, halve the number of global deaths and injuries from road traffic accidents.**
>
> 3.6.1 Death rate due to road traffic injuries

This target is interpreted to cover research about deaths and injuries from road traffic accidents. Improvement to road/vehicle safety generally is not considered relevant unless it is connected to health - the injury/death focus is evident in the target and the High-level Political Forum thematic review for SDG 3 (<a id="HLPF">[ECESA plus members, 2017](#f21)</a>). Improving road safety generally is covered in SDG 11.2.

This query consists of 1 phrase. Originally, a second phrase was included about improving `survival` , however the relevant results are minimal; the majority discussing `survival` are not about road traffic safety (instead about e.g. biomedical, or  wildlife).

The elements of the phrase are: *traffic/road users + mortality/morbidity*

In the *traffic* terms, `vehicle OR driver OR car OR cars` are combined with `accident OR crash...` because these terms are used in a biomedical or general context not to do with traffic (e.g. "xyz works as a vehicle for delivery of the drug"; "car T cells"; "x is a driver of y"). `intersection$` was considered but removed as it mostly added noise from metaphorical use of intersection (e.g. between two subject areas).

```py
TS =
(
  (
      ("traffic" OR "road" OR "roads" OR "roadway$" OR "street$" OR "roundabout$" OR "highway$" OR "motorway$"
      OR "cycling lane$" OR "cycle path$" OR "bicycle lane$" OR "walkway$" OR "walking path$" OR "sidewalk$" OR "pavement$"
      OR "bicycle$" OR "motorcycle$" OR "motorbike$" OR "automobile$" OR "buses" OR "bus" OR "lorry" OR "lorries" OR "truck$" OR "HGV$" OR "SUV$"
      OR "pedestrian$" OR "cyclist$"
      OR "driving fatalities"
      OR (("vehicle$" OR "driver$" OR "driving" OR "car" OR "cars") NEAR/15 ("accident$" OR "crash*" OR "collision$" OR "traffic" OR "RTI" OR "RTIs"))
      )
      AND
          ("mortality" OR "death$" OR "fatalities" OR "fatal" OR "deadly"
          OR "morbidity" OR "injury" OR "injuries" OR "road trauma$" OR "RTI" OR "RTIs"
          )
  )
  NOT ("air traffic" OR "boat traffic")
)
```


### Target 3.7

> **3.7 By 2030, ensure universal access to sexual and reproductive health-care services, including for family planning, information and education, and the integration of reproductive health into national strategies and programmes**
>
> 3.7.1 Proportion of women of reproductive age (aged 15–49 years) who have their need for family planning satisfied with modern methods
>
> 3.7.2 Adolescent birth rate (aged 10–14 years; aged 15–19 years) per 1,000 women in that age group

This target is interpreted to cover research about:
* access to sexual health services and family planning
* access to education and information about sexual health and family planning
* reproductive health/sexual health and national strategies and programmes.

This query consists of 2 phrases.

#### Phrase 1

The elements of the phrase are: *reproductive health/education + access*

Originally, *reproductive health* terms were combined with *service/information* terms (`"support" OR "service$" OR "program*" OR "right$" OR "facility" OR "facilities" OR "hospital$" OR "clinic$" OR "treatment" OR "checkup$" OR "check up$" OR "healthcare" OR "care" OR "aftercare" OR "information" OR "education"`). However, a wide variety of terms are used, and sometimes no terms at all. When *reproductive health* terms are combined with *access* terms, the results are mostly discussing some sort of service/education/communication, so the *service/information* terms were dropped as an unnecessary restriction.

Terms such as `reproductive health` will cover `reproductive health care / health services` etc.. `abortion` is included as part of reproductive health, according to WHO ("Access to legal, safe and comprehensive abortion care, including post-abortion care, is essential for the attainment of the highest possible level of sexual and reproductive health"; (<a id="WHOabortion">[WHO, n.d. c](#f15)</a>).

Here, `right$` is included as "right to reproductive health" encompasses access to services/education/information about this. `health equity` also covers ideas around access (from "Equity is the absence of avoidable, unfair, or remediable differences among groups of people, whether those groups are defined socially, economically, demographically or geographically or by other means of stratification. "Health equity” or “equity in health” implies that ideally everyone should have a fair opportunity to attain their full health potential and that no one should be disadvantaged from achieving this potential" (<a id="WHOequity">[WHO, n.d. d](#f8)</a>). `Health for all` refers to a movement/strategy of WHO sometimes still referenced, and is wider than only the healthcare aspect, but involves the idea of bringing of health to everyone (<a id="WHOhealthforall">[WHO, 1981](#f16)</a>).

```py
TS =
(
  ("reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare"
  OR "family planning" OR "planned pregnanc*" OR "contracept*" OR "abortion$"
  OR (("reproduct*" OR "sex*" OR "STI") NEAR/5 ("education" OR "inform*" OR "health literacy"))
  )
  NEAR/15
      ("health equity" OR "equity in health*" OR "health for all"
      OR "access*" OR "right$" OR "coverage"
      OR "afford" OR "affordab*" OR "low cost" OR "free of charge" OR "free service$" OR "subsidi*"
      OR "barrier$" OR "obstacle$" OR "impediment$" OR "unaffordab*" OR "expensive"
      )
)       
```

#### Phrase 2

The elements of the phrase are: *reproductive health + national programmes*. Here we have included LMICs and LDCs as "synonyms" for national; this provides over double the number of relevant results, as works often refer to e.g. "...implementation of a reproductive health programme in Tunisia".

```py
TS =
(
  ("reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare"
  OR "family planning" OR "planned pregnanc*" OR "contracept*" OR "abortion$"
  OR (("reproduct*" OR "sex*" OR "STI") NEAR/5 ("education" OR "inform*" OR "health literacy"))
  )
  NEAR/15
    (
      ("policy" OR "policies" OR "initiative$" OR "framework$" OR "program*" OR "strateg*")
      NEAR/5
          ("national" OR "state" OR "federal"
          OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey"
          OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
          )
    )
)

```

### Target 3.8

> **3.8 Achieve universal health coverage, including financial risk protection, access to quality essential health-care services and access to safe, effective, quality and affordable essential medicines and vaccines for all**
>
> 3.8.1 Coverage of essential health services
>
> 3.8.2 Proportion of population with large household expenditures on health as a share of total household expenditure or income

This target is interpreted to include research about 1) universal health coverage and access to healthcare, 2) financial obstacles/hardship in healthcare, including access to essential medicines and vaccines

#### Phrase 1

This phrase covers universal health coverage. The elements of the phrase are: *universal health coverage*.

```py
TS =
(
  ("universal health coverage" OR "universal healthcare" OR "universal health care")
)

```

#### Phrase 2

This phrase covers access to healthcare, essential medicines and vaccines. The elements of the phrase are: *health care/medications + access/affordability/quality*

`treatment` is not used alone, as there are technical biomedical works about e.g. barrier treatments. Under *access* terms, we have included `health equity` and `vaccine equity`, as we consider it to cover the idea of "medicines and vaccines for all".

```py
TS =
(
  ("health care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care" OR "health coverage"
  OR "family planning" OR "reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare"
  OR "vaccine$" OR "immuni$ation"
  OR (("essential" OR "basic" OR "life saving" OR "necessary" OR "emergency") NEAR/3 ("medicines" OR "medication$" OR "treatment*" OR "therap*"))
  OR "treatment access" OR "access to treatment$"
  )
  NEAR/15
      ("health equity" OR "equity in health*" OR "health care equity" OR "equity in healthcare" OR "health for all" OR "vaccine equity"
      OR "access*" OR "barrier$" OR "obstacle$"
      OR "afford" OR "affordab*" OR "low cost" OR "inexpensive" OR "free service$" OR "free of charge" OR "voucher$"
      OR "unaffordab*" OR "high price$" OR "costly" OR "debt" OR "financial risk$" OR "financial burden$" OR "financial hardship" OR "household expenditure$" OR "medical expenditure$" OR "medical expenses" OR "medical bill$" OR "medical cost$" OR "out of pocket"
      OR "microinsurance"
      OR "quality medicines" OR "quality care" OR "quality of care" OR "quality health care"
      )
)
```

### Target 3.9

> **3.9 By 2030, substantially reduce the number of deaths and illnesses from hazardous chemicals and air, water and soil pollution and contamination**
>
> 3.9.1 Mortality rate attributed to household and ambient air pollution
>
> 3.9.2 Mortality rate attributed to unsafe water, unsafe sanitation and lack of hygiene (exposure to unsafe Water, Sanitation and Hygiene for All (WASH) services)
>
> 3.9.3 Mortality rate attributed to unintentional poisoning

The target is interpreted to cover research about deaths and illnesses and pollution/contamination of water, air or soil with chemicals/substances or pathogens. In light of indicator 3.9.2, we also include research about deaths and illnesses and poor sanitation (e.g. contamination in the water source, or spread of disease between people due to lack of WASH facilities).

We were slightly unsure whether food poisoning/contaminated food should be included - it is not air, soil or water, but is related to hygiene/sanitation. So far, it is included. The High-level Political Forum thematic review for SDG 3 (<a id="HLPF">[ECESA plus members, 2017](#f21)</a>) mentions food in reference to WASH:
>"These services need to be accompanied by adequate hygiene practices such as handwashing after defecation or before food preparation and intake..."

This query consists of 2 phrases. The phrases are similar, but phrase 2 includes terms which need to be limited to humans.

#### Phrase 1

The elements of the phrase are: *contamination/toxins* + *disease/mortality*.

In the disease/mortality terms, only terms for mortality are included. `survival` is not - there are few results and they often concern animals.

Specific types of air pollution were added from WHO factsheets on ambient air pollution (<a id="WHOambientairpoll">[WHO, 2021a](#f22)</a>) and household air pollution  (<a id="WHOhouseairpoll">[WHO, 2021b](#f25)</a>). `air pollution` will find both ambient and indoor/household air pollution. Note that `pollution` alone is covered in phrase 2.

`poisoning*` reflects a disease/mortality/health outcome, thus is included with the *disease/mortality* terms. This improves the results by vastly increasing recall of those about reducing carbon monoxide poisoning. `unintentional OR accidental NEAR/3 poisoning$` is additionally included in the *contamination/toxins* terms; thus the string will find e.g. "reducing accidental poisonings", "preventing unintentional child poisoning" or "treating accidental drug poisonings".

The combination of gases with `NEAR/15 "pollution" OR "poisoning$"` is necessary because there are medical papers that discuss gases in terms of diagnosis or treatment (e.g. diffusion lung capacity of CO). The chemical abbreviations for the gases (e.g. `SO2`) are not used, as they result in technical articles where sorbents or fuel cells can be "poisoned".

`hygiene` is not used alone as there are many results about oral hygiene which are probably too broad (not to do with pollution/contamination). `sanitation` is also limited here, to remove animal results, and included more broadly in phrase 2.


```py
TS =
(
  ("air pollution" OR "PM2.5" OR "PM10" OR "particulate matter" OR "ozone"
  OR
    (
      ("nitrogen dioxide" OR "sulfur dioxide" OR "sulphur dioxide" OR "carbon monoxide" OR "volatile organic compounds")
      NEAR/15 ("pollution" OR "poisoning$")
    )
  OR "smoke pollution" OR "secondhand smok*" OR "second hand smok*" OR "involuntary smoking" OR "passive smoking"
  OR
    (         
      ("drinking water" OR "potable water" OR "water source$")
      NEAR/3 ("unsafe" OR "safe" OR "contaminated" OR "contamination" OR "pollut*" OR "clean")
    )
  OR "poor hygiene" OR "good hygiene" OR "hand hygiene" OR "personal hygiene" OR "hygiene practice$" OR "hygiene intervention$"
  OR "handwashing"
  OR "poor sanitation" OR "*adequate sanitation" OR "good sanitation" OR "sanitation facilities"
  OR "water, sanitation and hygiene"
  OR
    (
      ("food" OR "foods")
      NEAR/3 ("unsafe" OR "contaminated" OR "contamination" OR "sanitation")
    )
  OR "food poisoning$" OR "foodborne pathogens"
  OR ("poisoning$" NEAR/3 ("unintentional" OR "accidental"))
  )
  NEAR/15
      ("mortality" OR "death$" OR "illness*" OR "disease$" OR "morbidity" OR "poisoning$")
)      

```

#### Phrase 2

The elements of the phrase are: *pollutants/contamination + disease/mortality + humans*.

This phrase was created as certain pollutants/contamination terms often give results for animals; thus they are combined with terms for humans. Certain diseases are also included in these terms for humans, because they are nearly always used in the context of humans and relevant for this topic.

Specific chemicals were added from the WHO list of chemicals of major public health concern (<a id="WHOchem">[WHO, 2020b](#f11)</a>). Although the list specifies "highly hazardous pesticides", pesticides generally are searched for (research on limiting the health effects of all pesticides is considered relevant). `lead` must be searched for as part of a phrase, due to its use as a verb. Additional terms were added from the SDG topic page for chemicals and waste (<a id="SDGKPchem">[Sustainable Development Goals Knowledge Platform, n.d.](#f20)</a>). `contamination` is limited to `water contamination` and `soil contamination` (+ variants) to limit to the environment. Contamination of drinking water is covered in phrase 1 (here `water` alone is sufficient, due to the *human* terms). `heavy metals` as a general term is not included - many results seemed to be toxicity in plants, despite the *human* terms.

`poisoning$ OR poisoned` and `*toxicity` (covers gene/neuro/gonadotoxicity) were added to the mortality terms, as, in combination with the human terms, they are mostly used in the context of human illnesses. `fluorosis`, is a disease from excess fluoride.


```py
TS =
(
  (
    ("hazardous chemical$" OR "hazardous material$" OR "hazardous substance$" OR "hazardous waste$"
    OR "pollution"
    OR "soil contamination" OR "contamination of soil$" 
    OR "water contamination" OR "contamination of water"
    OR "arsenic"
    OR "asbestos"
    OR "benzene"
    OR "cadmium"
    OR "dioxin$"
    OR "mercury"
    OR "fluoride"
    OR "pesticide$"
    OR "lead poison*" OR "lead *toxicity" OR "lead mediated *toxicity" OR "lead induced *toxicity" OR "lead exposure" OR "lead carcinogen*" OR "blood lead"
    OR "radioactive waste$"
    OR "persistent organic pollutant$"
    OR "sanitation"
    )
    NEAR/15
        ("mortality" OR "death$" OR "illness*" OR "disease$" OR "morbidity"
        OR "*toxicity" OR "poisoning$" OR "poisoned" OR "fluorosis"
        )
  )
  AND
      ("humans" OR "humanity" OR "human" OR "people" OR "person$"
        OR "children" OR "child" OR "under fives" OR "infant$" OR "toddler$" OR "babies" OR "teenager$" OR "adolescent$" OR "girls" OR "boys"
        OR "elderly" OR "adult$" OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys"
        OR "rural" OR "urban" OR "city" OR "cities" OR "town$" OR "village$" OR "countr*" OR "nation$" OR "develop* state$"
        OR "patient$" OR "hospital*"
        OR "premature death$" OR "premature mortality"
        OR "neglected tropical disease$" OR "diarrhoea*" OR "diarrhea*"
      )
)

```

### Target 3.a

> **3.a Strengthen the implementation of the World Health Organization Framework Convention on Tobacco Control in all countries, as appropriate**
>
> 3.a.1 Age-standardized prevalence of current tobacco use among persons aged 15 years and older

This target is interpreted to cover research about tobacco use and production, or implementation of the WHO FCTC. WHO FCTC is a treaty from 2003 which aims to reduce tobacco use, via reducing supply and demand. There are several strands of tobacco control measures, including protecting public health policy from industry influence, tax measures, regulation of contents of tobacco products, regulation of packaging and labelling, warnings about risks, bans on advertising and sales to minors, support for those with addictions, support for alternatives for those who grow tobacco, and reductions in illicit trade of tobacco (<a id="WHOFCTC">[Regional Office for Europe, n.d.](#f16)</a>)

This query consists of 3 phrases.

#### Phrase 1

This phrase finds works referring to the FCTC.

```py
TS = ("Framework convention on tobacco control" OR "WHO FCTC")
```

#### Phrase 2

This phrase finds works about reduction and preventative measures (e.g. tax, policies) and tobacco. The elements of the phrase are: *tobacco + reduction/control*

We do not limit terminology to tobacco "use", as the FCTC also refers to tobacco control and reduction in supply, advertising, packaging regulation etc. `tobacco OR smoking OR cigarette$` will cover many terms here (e.g. cigarette packaging, smoking cessation, tobacco use/consumption/advertising).

`reduc* tobacco` etc. will find both reducing tobacco use and production. It is added as a phrase as `reduc*` + `tobacco` alone is too broad (e.g. "tobacco reduces lung function" - not relevant). Phrase 3 deals with tobacco production in more depth.

```py
TS =
(
  (
    (
      ("tobacco" OR "smoking" OR "cigarette$")
      NEAR/5
          ("reduc*" OR "control" OR "ban" OR "bans" OR "banning" OR "prohibiting" OR "prohibit"
          OR "legislation" OR "policy" OR "policies" OR "regulat*" OR "law" OR "strateg*" OR "intervention$"
          OR "tax" OR "taxes" OR "taxation"
          OR "health warning$"
          OR "smoking cessation" OR "quitting" OR "services" OR "cessation service" OR "cessation program*" OR "alternative$"
          )
    )
  OR "reduc* tobacco" OR "reduc* smoking" OR "decreas* tobacco"
  OR "reduce dependence on"
  )
  AND ("tobacco")
)
```

#### Phrase 3

This phrase covers research about alternatives to tobacco production. The elements of the phrase are: *tobacco farming + alternatives*.

```py
TS=
(
  ("tobacco farm*" OR "tobacco production" OR "tobacco growing" OR "tobacco grower$")
  AND
    ("diversif*" OR "alternative crop$" OR "crop substitution"
    OR "alternative livelihood$" OR "alternative sustainable livelihood$"
    )
)
```


### Target 3.b

> **3.b Support the research and development of vaccines and medicines for the communicable and non‑communicable diseases that primarily affect developing countries, provide access to affordable essential medicines and vaccines, in accordance with the Doha Declaration on the TRIPS Agreement and Public Health, which affirms the right of developing countries to use to the full the provisions in the Agreement on Trade-Related Aspects of Intellectual Property Rights regarding flexibilities to protect public health, and, in particular, provide access to medicines for all**
>
> 3.b.1 Proportion of the target population covered by all vaccines included in their national programme
>
> 3.b.2 Total net official development assistance to medical research and basic health sectors
>
> 3.b.3 Proportion of health facilities that have a core set of relevant essential medicines available and affordable on a sustainable basis

This target is interpreted to cover research about:
* The development of medicines/vaccines for diseases in developing countries or for diseases "primarily affecting" them. For the query, we have interpreted this as neglected tropical diseases. For other diseases it is harder to decide if they are neglected or who they primarily affect. (phrase 1).
* Access to affordable essential medicines and vaccines on a broad scale in accordance with Doha/TRIPS (phrase 2).

This query consists of 2 phrases.

#### Phrase 1

The elements of the phrase are: *vaccine/medicine development + developing countries*. Note that here, `development` is combined within phrases (e.g. `development aid OR development fund`) because it is also a part of "vaccine development".

```py
TS =
(
  (
    ("develop*" OR "research*" OR "R&D" OR "novel" OR "new")
    NEAR/5 ("medicine$" OR "medication$" OR "therapy" OR "therapies" OR "therapeutic$" OR "vaccin*" OR "drug$" OR "cures" OR "treatment$")
  )
  AND
    ("neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthias*" OR "hookworm$" OR "roundworm$" OR "whipworm$" OR "Ascaris lumbricoides" OR "Trichuris trichiura" OR "Necator americanus" OR "Ancylostoma duodenale"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
    OR "least developed countr*" OR "least developed nation$"
    OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
    OR "less developed countr*" OR "less developed nation$"
    OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
    OR "underserved countr*" OR "underserved nation$"
    OR "deprived countr*" OR "deprived nation$"
    OR "middle income countr*" OR "middle income nation$"
    OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
    OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
    OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
    OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
    OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
    OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish"  OR "turkey"
    )
)
```

#### Phrase 2

This phrase concerns access to essential medicines and vaccines. The TRIPS agreement is the Agreement on Trade-Related Aspects of Intellectual Property Rights for all members of the WTO. The Doha declaration was an interpretative statement for TRIPS, added later in 2001, which covers several aspects of its implementation. This includes "compulsory licensing", which can be used to produce medicines without the agreement of the patent holder under certain circumstances. About health, from <a id="WTOdoha">[World Trade Organization, n.d.](#f17)</a>:
> "In the declaration, ministers stress that it is important to implement and interpret the TRIPS Agreement in a way that supports public health — by promoting both access to existing medicines and the creation of new medicines.[...]. It emphasizes that the TRIPS Agreement does not and should not prevent member governments from acting to protect public health."

The elements of the phrase are: *(agreements/IPR + medicines + access) OR vaccine equity*. `patents` is used in the plural as when singular it tends to have specific/biomedical uses. `vaccine inequity` is included as a  term that often refers to inequity in access to vaccines on a global scale (particularly in reference to covid19).

```py
TS =
(
  ("Doha declaration" OR "compulsory licens*" OR "patents" OR "intellectual property" OR "TRIPS agreement")
  AND
    ("pharmaceuticals" OR "medicine$" OR "vaccine$" OR "immuni$ation" OR "essential drug$" OR "medication$"
    OR (("essential" OR "life saving" OR "emergency" OR "health" OR "medical") NEAR/3 ("treatment*" OR "therap*"))
    OR "treatment access" OR "access to treatment$"
    )
  AND
    ("access" OR "accessibility"
    OR "affordab*" OR "low cost" OR "inexpensive" OR "free of charge" OR "unaffordab*" OR "expensive"
    )
)
OR TS=("vaccine equity" OR "vaccine inequity")
```

### Target 3.c

> **3.c Substantially increase health financing and the recruitment, development, training and retention of the health workforce in developing countries, especially in least developed countries and small island developing States**
>
> 3.c.1 Health worker density and distribution

This target is interpreted to cover research about training and retention of the health workforce in developing countries (phrase 1). It also covers research about health financing in these countries (phrase 2).

This query consists of 2 phrases.

#### Phrase 1

The elements of the phrase are: *retention/training + health workers + countries*

Types of health worker were supplemented from the subcategories under the MeSH category "Health Personnel" (MeSH ID D006282). `training` and `education` are separated out as there are many results about "training to improve outcomes..." rather than improving the training itself.

```py
TS =
(
  (
    (
      ("recruitment" OR "professional development" OR "retention" OR "capacity building" OR "capacity development"
      OR "increase training" OR "improv* training" OR "enhanc* training"
      OR "increase education" OR "improv* education" OR "enhanc* education"
      OR "train more" OR "recruit more" OR "increase trained" OR "increase the number of"
      OR "human capital flight" OR "brain drain" OR "emigration" OR "turnover" OR "intention to leave"
      )
    )
    NEAR/15
        (
           (
             ("health" OR "healthcare" OR "medical")
             NEAR/3 ("workforce" OR "professional$" OR "worker$" OR "personnel" OR "practitioner$" OR "human resources" OR "student$")
           )
           OR "nurse$" OR "doctor$" OR "physician$"
           OR "Anesthetist$" OR "Audiologist$" OR "Dental Staff" OR "Dentist$" OR "Doula$" OR "Emergency Medical Dispatcher$" OR "Health Educator$" OR "Health Facility Administrator$" OR "Infection Control Practitioner$" OR "Medical Chaperone$" OR "Medical Laboratory Personnel" OR "Nutritionist$" OR "Therapist$" OR "Optometrist$" OR "Pharmacist$" OR "Allergist$" OR "Anesthesiolog*" OR "Cardiolog*" OR "Dermatolog*" OR "Endocrinolog*" OR "Gastroenterolog*" OR "General Practic*" OR "Geriatrician$" OR "gynecologist$" OR "Hospitalist$" OR "Nephrolog*" OR "Neurolog*" OR "Oncolog*" OR "Ophthalmolog*" OR "Otolaryngolog*" OR "midwives" OR "Pathologist$" OR "Pediatric*" OR "Physiatrist$" OR "Pulmonolog*" OR "Radiolog*" OR "Rheumatolog*" OR "surgeon$" OR "Urologist$"
       )
  )
  AND
      ("least developed countr*" OR "least developed nation$" OR
      "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
      OR "less developed countr*" OR "less developed nation$"
      OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
      OR "underserved countr*" OR "underserved nation$"
      OR "deprived countr*" OR "deprived nation$"
      OR "middle income countr*" OR "middle income nation$"
      OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
      OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
      OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey"      
      )
)
```

#### Phrase 2

The elements of the phrase are: *financing + health sector + countries*. 

```py
TS =
(
  (
    ("financing" OR "invest" OR "investment$" OR "investing" OR "funding" OR "funds"
    OR "health spending" OR "health care spending" OR "health budget" OR "public spending" OR "government spending"
    OR "financial assist*" OR "economic assist*" OR "financial support" OR "financial resources"
    OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
    OR "ODA" OR "cooperation fund$" OR "development spending"
    OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance" OR "finance" OR "grant$"))
    )
    NEAR/15
        ("health sector" OR "health financing" OR "health budget" OR "health spending"
        OR "health service$" OR "healthcare" OR "health care" OR "medical care"
        OR "medical research" OR "health research" OR "health R&D" OR "medical R&D"
        )   
  )
  AND
    ("least developed countr*" OR "least developed nation$" OR
    "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
    OR "less developed countr*" OR "less developed nation$"
    OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
    OR "underserved countr*" OR "underserved nation$"
    OR "deprived countr*" OR "deprived nation$"
    OR "middle income countr*" OR "middle income nation$"
    OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
    OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
    OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
    OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
    OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
    OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey"           
    )
)
```

### Target 3.d

> **3.d Strengthen the capacity of all countries, in particular developing countries, for early warning, risk reduction and management of national and global health risks**
>
> 3.d.1 International Health Regulations (IHR) capacity and health emergency preparedness
>
> 3.d.2 Percentage of bloodstream infections due to selected antimicrobial-resistant organisms

This target is interpreted to refer to research about health emergency preparedness, particularly in reference to the IHR. From <a id="WHOGHO">[The Global Health Observatory (n.d.)](#f18)</a>:
>"Under the IHR, States Parties are obliged to develop and maintain minimum core capacities for surveillance and response, including at points of entry, in order to early detect, assess, notify, and respond to any potential public health events of international concern. [...]. The 13 core capacities are: (1) Legislation and financing; (2) IHR Coordination and National Focal Point Functions; (3) Zoonotic events and the Human-Animal Health Interface; (4) Food safety; (5) Laboratory; (6) Surveillance; (7) Human resources; (8) National Health Emergency Framework; (9) Health Service Provision; (10) Risk communication; (11) Points of entry; (12) Chemical events; (13) Radiation emergencies."

There are also 19 technical areas from the Joint External Evaluation tool, which in addition to the 13 above include antimicrobial resistance, immunization, "national laboratory system", biosafety and biosecurity, "emergency preparedness", "emergency response operations", linking public health and security authorities, medical countermeasures and personnel deployment (<a id="WHOJEE">[WHO 2019b](#f19)</a>). A number of search terms are taken from this document.

This query consists of 1 phrase. The elements of the phrase are: *health emergencies + preparedness*

`national action plan` is a term used in relation to antimicrobial resistance. `emergency response` covers emergency response plans, etc. `health risk` is a very general term, so is here limited to national and global health risks, as stated in the target. `health emergency` is more unambiguously about emergency situations, so is not limited. The `NOT` statement is required to eliminate results for e.g. crop epidemics.

```py
TS =
(
  (
    ("national health risk$" OR "international health risk$" OR "global health risk$"
    OR "pandemic$" OR "epidemic$" OR "outbreak$"
    OR "medical disaster$" OR "health emergency" OR "health emergencies"
    OR "radiation emergenc*" OR "radiation event$"
    OR "chemical event$" OR "chemical emergenc*"
    OR "zoonotic event$" OR "zoonotic emergenc*"
    OR "food safety" OR "foodborne event$"
    OR "biosecurity event$" OR "biosecurity emergenc*"
    OR "antimicrobial resistan*" OR "antibiotic resistan*" OR "antifungal resistan*"
    )
    NEAR/15  
      ("capacity" OR "early warning*" OR "surveillance" OR "monitoring system$"
      OR "laboratory reporting" OR "laboratory infrastructure" OR "laboratory quality" OR "laboratory system$"
      OR "preparedness" OR "medical preparedness" OR "disaster planning" OR "national health emergency framework" OR "emergency risk assessment$"
      OR "risk reduction" OR "risk management" OR "risk communication"
      OR "emergency management" OR "emergency response" OR "personnel deployment" OR "security authorities"
      OR "vaccination program*" OR "vaccination framework$" OR "immuni$ation program*"
      OR "legislation" OR "policy" OR "policies" OR "financing"
      OR "international health regulations" OR "national focal point$" OR "national action plan*"
      )
  )
  NOT
      ("blight" OR "plant pathogen$" OR "plant disease$")
)
```

### Works mentioning the SDG

This phrase finds research which mentions this SDG. We include this as we consider works mentioning the SDG as relevant, and want to ensure they are found. It includes terms for the goal, and excludes specialist terms that may use the `SDG` acronym or use `health` in a non-human way.

```py
TS=
("SDG 3" OR "SDGs 3" OR "SDG3" OR "sustainable development goal$ 3"
OR ("sustainable development goal$" AND "goal 3")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 3")
    NEAR/50 ("health")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  OR (("soil health" OR "ecosystem health" OR "coastal health" OR ("ocean$" NEAR/5 "health")) NOT ("human health"))
  )
```

## 4. Contributions

* v2019.12: Marta Lorenz, Caroline S. Armitage, Susanne Mikki

* v1.0.0 Caroline S. Armitage (Oct 2021-Oct 2022)

* Internal review: Marta Lorenz, Håkon Magne Bjerkan (March 2022); Håkon Magne Bjerkan (minor review Oct 2022)

Specialist input: Awaiting

## 5. Footnotes

<a id="f29"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f13"></a> Centers for Disease Control and Prevention. (2021). *Waterborne Disease Prevention Branch*. https://www.cdc.gov/ncezid/dfwed/waterborne/ [Accessed 15.10.2021] [↩](#CDCwaterborne)

<a id="f21"></a> ECESA plus members. (2017). *2017 HLPF Thematic Review of SDG3: Ensure healthy lives and promote well-being for all at all ages*. United Nations. https://sustainabledevelopment.un.org/content/documents/14367SDG3format-rev_MD_OD.pdf [accessed 12.11.2021] (#HLPF)

<a id="f5"></a> International Agency for Research on Cancer. (2019). *The Cancer Dictionary*. World Health Organization. http://www-dep.iarc.fr/WHOdb/WHOdb.htm [accessed 15.11.2019] [↩](#WHOcancer)

<a id="f6"></a> National Cancer Institute. (n.d.). *Cancer Classification*. National Institutes of Health. https://training.seer.cancer.gov/disease/categories/classification.html [accessed 15.11.2019] [↩](#NIHcancer)

<a id="f14"></a> National Institute on Drug Abuse. (2020, August). *Commonly Used Drugs Charts*. National Institutes of Health. https://www.drugabuse.gov/drug-topics/commonly-used-drugs-charts [Accessed 26.10.2021] [↩](#NIHdrugs)

<a id="f24"></a> Regional Office for the Eastern Mediterranean. (n.d.). *Epidemic and pandemic-prone diseases*. World Health Organization. http://www.emro.who.int/pandemic-epidemic-diseases/health-topics/related-health-topics.html [Accessed 18.11.2021] [↩](#WHOepipan)

<a id="f16"></a> Regional Office for Europe. (n.d.). *WHO Framework Convention on Tobacco Control (WHO FCTC)*. World Health Organization. https://www.euro.who.int/en/health-topics/disease-prevention/tobacco/publications/key-policy-documents/who-framework-convention-on-tobacco-control-who-fctc [accessed 10.11.2021].[↩](#WHOFCTC)

<a id="f30"></a> Rivest, Maxime; Kashnitsky, Yury; Bédard-Vallée, Alexandre; Campbell, David; Khayat, Paul; Labrosse, Isabelle; Pinheiro, Henrique; Provençal, Simon; Roberge, Guillaume; James, Chris. (2021). *Improving the Scopus and Aurora queries to identify research that supports the United Nations Sustainable Development Goals (SDGs) 2021* V3. [Dataset]. doi: 10.17632/9sxdykm8s4.3 [↩](#Els)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f20"></a> Sustainable Development Goals Knowledge Platform. (n.d.). *Chemicals and waste*. https://sustainabledevelopment.un.org/topics/chemicalsandwaste [accessed 12.11.2021] [↩](#SDGKPchem)

<a id="f18"></a> The Global Health Observatory. (n.d.). *Average of 13 International Health Regulations core capacity scores, SPAR version*. World Health Organization. https://www.who.int/data/gho/data/indicators/indicator-details/GHO/-average-of-13-international-health-regulations-core-capacity-scores-spar-version [accessed 11.11.2021] [↩](#WHOGHO)

<a id="f22"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f16"></a> World Health Organization. (1981). *Global Strategy for health for all by the year 2000*. "Health for all" series, 3. http://apps.who.int/iris/bitstream/handle/10665/38893/9241800038.pdf [↩](#WHOhealthforall)

<a id="f4"></a> World Health Organization. (2018). *Noncommunicable diseases*. [Fact sheet]. https://www.who.int/en/news-room/fact-sheets/detail/noncommunicable-diseases [accessed 15.11.2019] [↩](#WHOFSnoncomm)

<a id="f7"></a> World Health Organization. (2019a). *Mental disorders*. [Fact sheet]. https://www.who.int/en/news-room/fact-sheets/detail/mental-disorders [accessed 29.11.2019] [↩](#WHOFSmental)

<a id="f19"></a> World Health Organization. (2019b). *WHO Benchmarks for International Health Regulation (IHR) Capacities*. https://apps.who.int/iris/handle/10665/311158 [↩](#WHOJEE)

<a id="f3"></a> World Health Organization. (2020a). *Ending the neglect to attain the Sustainable Development Goals: a road map for neglected tropical diseases 2021–2030*. https://apps.who.int/iris/handle/10665/338565  [↩](#WHONTD)

<a id="f11"></a> World Health Organization. (2020b, June 20). *10 chemicals of public health concern.*. [Photo story]. https://www.who.int/news-room/photo-story/photo-story-detail/10-chemicals-of-public-health-concern [accessed 15.11.2021]  [↩](#WHOchem)

<a id="f23"></a> World Health Organization. (2020c, Dec 9). *The top 10 causes of death*. [Fact sheet]. https://www.who.int/news-room/fact-sheets/detail/the-top-10-causes-of-death [accessed 18.11.2021]  [↩](#WHOFStop10)

<a id="f22"></a> World Health Organization. (2021a). *Ambient (outdoor) air pollution*. [Fact sheet]. https://www.who.int/news-room/fact-sheets/detail/ambient-(outdoor)-air-quality-and-health [accessed 12.11.2021] [↩](#WHOambientairpoll)

<a id="f25"></a> World Health Organization. (2021b). *Household air pollution and health*. [Fact sheet]. https://www.who.int/news-room/fact-sheets/detail/household-air-pollution-and-health [accessed 12.11.2021] [↩](#WHOhouseairpoll)

<a id="f2"></a> World Health Organization. (n.d. a). *Global Health Observatory data repository: By theme*. http://apps.who.int/gho/data/node.home [accessed 15.10.2021]

<a id="f2a"></a> World Health Organization. (n.d. b). *Global Health Observatory data repository: By category: Vaccine-preventable communicable diseases*. http://apps.who.int/gho/data/node.main.170?lang=en [accessed 15.10.2021].[↩](#WHOGHO)

<a id="f15"></a> World Health Organization. (n.d. c). *Abortion*. [Fact sheet]. https://www.who.int/health-topics/abortion [accessed 29.10.2021].[↩](#WHOabortion)

<a id="f8"></a> World Health Organization. (n.d. d). *Health Equity*. https://www.who.int/topics/health_equity/en/ [accessed 29.11.2019] [↩](#WHOequity)

<a id="f17"></a> World Trade Organization. (n.d.). *The Doha Declaration explained*. https://www.wto.org/english/tratop_e/dda_e/dohaexplained_e.htm [accessed 11.11.2021] [↩](#WTOdoha)
